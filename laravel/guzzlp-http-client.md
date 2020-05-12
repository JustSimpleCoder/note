


- 文档 https://guzzle-cn.readthedocs.io/zh_CN/latest/quickstart.html

- demo 如下

```

$client = new Client(['base_uri' => 'http://bc.x', 'connect_timeout' => 1]);
$client2 = new Client(['base_uri' => 'http://bc.x']);

$beginTime = Carbon::now();
$promise = [
    "a1" => $client->getAsync('/api/test/xx2', ['timeout' => 0.1])
        ->then(function (ResponseInterface $res) {
            return $res;
        }, function () {
            return null;
        }),
    "a2" => $client2->getAsync('/api/test/xx?a=2', ['timeout' => 1.1]),
    "a3" => $client2->getAsync('/api/test/xx?a=3', ['timeout' => 1.1]),
];

$result = Promise\unwrap($promise);
$result = Promise\settle($promise)->wait();
dump(BaseUtilService::costTime($beginTime));
dump($result);

```

- 二维数组排序

```
public static function twoVArraySort(array $data, string $key, string $sort = 'ASC')
{
    try {
        $sortKey = array_column($data, $key);
        $sortType = $sort === 'ASC' ? SORT_ASC : SORT_DESC;
        array_multisort($sortKey, $sortType, $data);
    } catch (\Exception $e) {
    }

    return $data;
}
```