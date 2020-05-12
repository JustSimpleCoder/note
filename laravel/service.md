## service 登录验证和中间件验证 ##

### 添加中间件 路由 & 配置 ###

```
//  /app/Http/Kernel.php 
// add 
//'CheckManager' => \App\Http\Middleware\CheckManager::class,

class CheckManager
{

    public function handle($request, Closure $next)
    {
    	if (?true){
    		return [];
    	}

    	return $next($request);
    }


```


### 登录服务 Auth 修改 ###

```
// config/auth.php 
[
 'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],

        'newApi' => [
            'driver' => 'ApiUserService',
        ],
    ],
];

// new 
class ApiUserService
{
    public static function auth(Request $request){
    	retrun ["uid"=>1];
    }
}

//use

Auth::guard('newApi')->user();


```