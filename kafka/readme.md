
### 如果让我总结 php Kafka 如何使用？ ###

- Kafka 组成、原理 
- Kafka 解决那些问题
- php rdkafka 的使用



#### 组成 ####

- broker kafka的消息存储节点
- zookeeper 负责管理 broker 的服务。 分布式、订阅&发布等
- producer/consumer（Group） 生产者&消费者（组)
- topic 消息的存储的queue名
- partition topic存储的位置

#### 解决问题 ####

- 消息中间件、数据信息同步

#### php rdkafka ####
1. 安装扩展、目前只找到 linux 版本 windows DLL 无效 [安装地址 https://arnaud-lb.github.io/php-rdkafka/phpdoc/rdkafka.setup.html](https://arnaud-lb.github.io/php-rdkafka/phpdoc/rdkafka.setup.html)
2. 使用示例 [https://arnaud-lb.github.io/php-rdkafka/phpdoc/rdkafka.examples.html](https://arnaud-lb.github.io/php-rdkafka/phpdoc/rdkafka.examples.html) 
3. Class 理解整理 [https://arnaud-lb.github.io/php-rdkafka/phpdoc/](https://arnaud-lb.github.io/php-rdkafka/phpdoc/)

	- 设置 broker
	- 设置 TopicConfig （读取开始位置、偏移量存储等）
	- 消息体处理

```
	// 生产消息
	$rk = new RdKafka\Producer();
	$rk->setLogLevel(LOG_DEBUG);
	$rk->addBrokers("10.15.4.237:19092,10.15.4.238:19092,10.15.4.239:19092");
	$topic = $rk->newTopic("test");
	for ($i = 0; $i < 2; $i++) {
    	$topic->produce(RD_KAFKA_PARTITION_UA, 0, "Message $i");
	}
```

```

	// 消费	
	$rk = new RdKafka\Consumer();
	$rk->setLogLevel(LOG_DEBUG);
	$rk->addBrokers("10.15.4.237:19092,10.15.4.238:19092,10.15.4.239:19092");
	
	
	
	$topicConf = new RdKafka\TopicConf();
	$topicConf->set('auto.commit.enable', 0);
	$topicConf->set('auto.commit.interval.ms', 100);
	$topicConf->set('request.required.acks', 1);
	$topicConf->set('offset.store.method', 'file');
	//$topicConf->set('auto.offset.reset', 'smallest');
	
	$topic = $rk->newTopic("test",$topicConf);
	//$topic->consumeStart(0, RD_KAFKA_OFFSET_END  );
	$topic->consumeStart(0, RD_KAFKA_OFFSET_STORED  );
	//$topic->consumeStart(0, RD_KAFKA_OFFSET_BEGINNING  );
	while (true) {
		// 详情见官方demo
	}
```





 