
### Laravel  ###


作者自述-深入理解Laravel框架 : https://my.oschina.net/zgldh/blog/389246

- 单一原则
	* 业务计算 和 db 存储分离
	* 业务抽象分离
- 开放封闭原则
	* 实现者变动时, 调用者不需要变动. 
- 里式替换原则
	* 被子类的实例替换,而不影响程序的正确性
- 接口隔离原则
	* 接口中的空方法, 违背了接口隔离. 定义细精致的接口
- 依赖翻转原则
	* 高级别的代码不依赖低级别的代码


### 框架中的 redis 分布式锁 ###

```
public function add($key, $value, $minutes)
{
    $lua = "return redis.call('exists',KEYS[1])<1 and redis.call('setex',KEYS[1],ARGV[2],ARGV[1])";

    return (bool) app('redis')->eval(
        $lua, 1, $key, $value, (int) max(1, $minutes * 60)
    );
}
```