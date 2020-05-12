### Apollo ###
 
```
composer require multilinguals/apollo-client
```

```
// create command
//@todo config
$serverIp = 'ip~~~~~';
$appId = "id~~~";
$namespaces = ['application'];

$apollo = new ApolloClient($serverIp, $appId, $namespaces);
$apollo->save_dir = base_path('config');

//@todo try
do {
    $err = $apollo->start(function () {
        Artisan::call("config:cache");
    });
    if ($err) {
        dump($err);
    }
} while ($err);

```

```

//使用   
dump(config('apolloConfig.application.configurations'));

```