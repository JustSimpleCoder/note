### Cobra ###

**命令创建,可以快速创建项目想要支持的命令** 

- 使用Demo 运行命令 main.go 如下

```
cobra add YourCommand

go run main.go YourCommand

```

```
package main

import (
    "test-cobra/cmd"
)

func main() {
    cmd.Execute()
}

```

