## New computer

-  software
	360 / chorme / java / vim / git / Google pinyin / SmartGit / wechat / phpstudy / vscode /sublime

- config

```
	GIT SSH-KEY
  	ssh-keygen -t rsa -C "youremail@example.com"
```

```
	JAVA_HOME
```


```

//mac ~/.bash_profile


JDK8=/Library/Java/JavaVirtualMachines/jdk1.8.0_211.jdk/Contents/Home/

JAVA_HOME=$JDK8
PATH=$JAVA_HOME/bin:$PATH:.
export JAVA_HOME
export PATH
export CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$CLASSPATH
GRADLE_HOME=/usr/local/Cellar/gradle/5.4.1/bin/gradle
export GRADLE_HOME
export PATH=$PATH:$GRADLE_HOME/bin


export GO111MODULE=on
export GOPROXY=https://goproxy.io
export PATH="/usr/local/opt/libxml2/bin:$PATH"

export PATH="/Users/yaobin/.phpbrew/php/php-7.3.8/bin:$PATH"
export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles
export HOMEBREW_NO_AUTO_UPDATE=true


```

```

-javaagent:/Users/yaobin/Project/software/jetbrains-agent.jar
http://fls.jetbrains-agent.com

```