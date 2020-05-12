## 基础了解一下 (Tcp + 粘包处理) ## 

**花了1天的时间调试 bufio 的数据 , 一直收不到数据 ! 最终因为没有使用 writer.Flush() [依然不理解,demo实例中不使用flush也可以收到数据]**

- ### json & time

```

type Message struct {
	Method  string          `json:"method"`
	Content string          `json:"content"`
	Time    config.JsonTime `json:"time"`
}


type JsonTime time.Time

func (j *JsonTime) UnmarshalJSON(data []byte) error {

	location, e := time.ParseInLocation("\""+TimeFormat+"\"", string(data), time.Local)
	*j = JsonTime(location)
	return e
}

func (j JsonTime) MarshalJSON() ([]byte, error) {
	data := make([]byte, 0)
	data = append(data, '"')
	data = time.Time(j).AppendFormat(data, TimeFormat)
	data = append(data, '"')
	return data, nil
}


```

- ### chanel & timer
	
```

func sendClientMessage(conn net.Conn, client Client) {

	keepTime := time.NewTicker(time.Second * 3)
	dataWriter := bufio.NewWriter(conn)
	for {

		select {
		case msg := <-client.mc:
			fmt.Println(msg)
			m := data.Message{Method: "ALL", Content: msg, Time: config.JsonTime(time.Now())}
			e := data.WritePackage(dataWriter, m)
			if e != nil {
				fmt.Println(e)
			}
			dataWriter.Flush()

		case <-keepTime.C:

			m := data.Message{Method: "connect", Content: "~hi~", Time: config.JsonTime(time.Now())}
			e := data.WritePackage(dataWriter, m)
			if e != nil {
				fmt.Println(e)
				return
			}
			dataWriter.Flush()

		}
	}

}

```

- ### socket & bufio

	* 大小端
	* net.Dail  // net.Listen  +  listen.Accept
	* package

```


type Package struct {
	Size    uint16
	Content []byte
}

func WritePackage(writer io.Writer, message Message) error {

	jsonStr, err := json.Marshal(message)

	if err != nil {
		return err
	}

	p := Package{Size: uint16(len(jsonStr)), Content: jsonStr}

	var buffer bytes.Buffer

	if err := binary.Write(&buffer, binary.LittleEndian, p.Size); err != nil {
		return err
	}

	if _, err := buffer.Write(p.Content); err != nil {
		return err
	}

	out := buffer.Bytes()

	if _, err := writer.Write(out); err != nil {
		return err
	}
	return nil

}

func ReadPackage(reader io.Reader) (p Package, e error) {

	var buffer = make([]byte, 2)
	_, e = io.ReadFull(reader, buffer)
	if e != nil {
		return
	}
	newReader := bytes.NewReader(buffer)
	if e = binary.Read(newReader, binary.LittleEndian, &p.Size); e != nil {

		return
	}
	p.Content = make([]byte, p.Size)
	_, e = io.ReadFull(reader, p.Content)
	return
}


```


## 微服务 ##

- etcd
- consul
- kong
- zipkin