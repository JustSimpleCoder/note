## 微服务理解 ##

**前置基础:网络协议 TCP/IP 网络7层**

### 注册发现 ###

- 注册服务地址&可调用的方法
- client Stub / service Stub

### 网络协议 & 连接 ###

- gRPC  基于 http2
- RESET 
- RMI ~ (Dubbo) ?
- RABBITMQ

### 扩展服务 ###

- 监控
- 熔断
- 负载

### 数据一致性 ###
- 实现模式
    - 靠事件模式 
    - 补偿模式
    - Sagas长事务模式
    - TCC
    - 最大努力通知模式

- 使用的协议
    - paxos
    - raft