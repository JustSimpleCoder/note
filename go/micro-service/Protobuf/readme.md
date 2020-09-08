### 基本信息 ###

- 与语言无关的数据格式 二进制的格式, 高性能的需求. 优:性能,向后兼容. 缺:不可读.
- 依赖.porto 文件 (基本语法) 

```
syntax = "proto3" ;

message PeopleRequest{
	string name = 1 ;
	int32 age = 2 ;
	repeated string span = 3;  // 注释
}

message PeopleResponse{
	int32 error = 1 ;
	string message = 2 ;
}
// double float int32 uint32 .. bool string bytes
// 会设置默认值  message 结构体多层的消息类型 ( 也可以嵌套)
// 

```

- 服务的定义
```
service SearchService[服务名] {

	rpc Search[方法名] (message_struct) return (message_struct)
}

```

- 命令
```

环境变量
export GOROOT
export GOPATH=/Users/xxxx/go
export GOBIN=
export PATH=$PATH:${GOPATH//://bin:}/bin
//go build -o 指定bin


protoc --proto_path=IMPORT_PATH --go_out=./*.proto

protoc --go_out=./ *.proto 

protoc --go_out=plugins=grpc:./ *.proto 

```


### 安装 ###

/Users/yaobin/go/src/github.com/golang/protobuf/protoc-gen-go/protoc-gen-go 

