## ES ##


### routing key ###

- 和集群有关. (元信息和主节点一致)   元信息: cluster-name: name ,  Nodes: 1 ... 2... 3
- 创建文档可以指定routing来指定分片

```
POST twitter/_doc?routing=kimchy
{
    "user" : "kimchy",
    "post_date" : "2009-11-15T14:12:12",
    "message" : "trying out Elasticsearch"
}
```
