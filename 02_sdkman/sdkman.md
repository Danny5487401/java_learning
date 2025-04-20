# github.com/sdkman/sdkman-cli






## 特性
- 全套JAVA支持  
为Java，Groovy，Scala，Kotlin和Ceylon等JVM安装软件开发工具包。 Ant，Gradle，Grails，Maven，SBT，Spark，Spring Boot，Vert.x以及其他许多支持。


- APIs
使用开放的Broker REST API可以轻松地编写新的客户端。供应商可以通过安全的供应商API发布自己的版本。
- 轻量
只需要有curl \ zip/unzip就可以在bash中通过命令使用.还可和ZSH一起使用.


```shell
# 查看版本
➜  ~ sdk version

SDKMAN!
script: 5.19.0
native: 0.7.4 (macos aarch64)
```
子命令 github.com/sdkman/sdkman-cli-native 用 rust 重写。

```shell
# 查看配置
(⎈|kubeasz-test:kafka)➜  java_learning git:(master) ✗ cat ~/.sdkman/etc/config 
sdkman_auto_answer=false
sdkman_auto_complete=true
sdkman_auto_env=false
sdkman_beta_channel=false
sdkman_checksum_enable=true
sdkman_colour_enable=true
sdkman_curl_connect_timeout=7
sdkman_curl_max_time=10
sdkman_debug_mode=false
sdkman_insecure_ssl=false
sdkman_native_enable=true
sdkman_selfupdate_feature=true
```


## 查看支持的软件 Candidates
```shell
(⎈|kubeasz-test:kafka)➜  ~ sdk list
================================================================================
Available Candidates
================================================================================
q-quit                                  /-search down
j-down                                  ?-search up
k-up                                    h-help

--------------------------------------------------------------------------------
Apache ActiveMQ (Classic) (5.17.1)                  https://activemq.apache.org/

Apache ActiveMQ® is a popular open source, multi-protocol, Java-based message
broker. It supports industry standard protocols so users get the benefits of
client choices across a broad range of languages and platforms. Connect from
clients written in JavaScript, C, C++, Python, .Net, and more. Integrate your
multi-platform applications using the ubiquitous AMQP protocol. Exchange
messages between your web applications using STOMP over websockets. Manage your
IoT devices using MQTT. Support your existing JMS infrastructure and beyond.
ActiveMQ offers the power and flexibility to support any messaging use-case.

                                                          $ sdk install activemq
--------------------------------------------------------------------------------
Ant (1.10.14)                                            https://ant.apache.org/
```

## java 管理

```shell
(⎈|kubeasz-test:kafka)➜  ~ sdk list java
....
 Zulu          |     | 24.fx        | zulu    |            | 24.fx-zulu
               |     | 24.0.1.fx    | zulu    |            | 24.0.1.fx-zulu
               |     | 24.0.1       | zulu    |            | 24.0.1-zulu
               |     | 24           | zulu    |            | 24-zulu
               |     | 23.0.2.fx    | zulu    |            | 23.0.2.fx-zulu
               |     | 23.0.2       | zulu    |            | 23.0.2-zulu
               |     | 21.0.7.fx    | zulu    |            | 21.0.7.fx-zulu
               |     | 21.0.7       | zulu    |            | 21.0.7-zulu
               |     | 21.0.6.fx    | zulu    |            | 21.0.6.fx-zulu
               |     | 21.0.6       | zulu    |            | 21.0.6-zulu
               |     | 17.0.15.fx   | zulu    |            | 17.0.15.fx-zulu
               |     | 17.0.15      | zulu    |            | 17.0.15-zulu
               |     | 17.0.14.fx   | zulu    |            | 17.0.14.fx-zulu
               |     | 17.0.14      | zulu    |            | 17.0.14-zulu
               |     | 11.0.27.fx   | zulu    |            | 11.0.27.fx-zulu
               |     | 11.0.27      | zulu    |            | 11.0.27-zulu
               |     | 11.0.26.fx   | zulu    |            | 11.0.26.fx-zulu
               |     | 11.0.26      | zulu    |            | 11.0.26-zulu
               |     | 8.0.452.fx   | zulu    |            | 8.0.452.fx-zulu
               |     | 8.0.452      | zulu    |            | 8.0.452-zulu
               |     | 8.0.442.fx   | zulu    |            | 8.0.442.fx-zulu
               |     | 8.0.442      | zulu    |            | 8.0.442-zulu
================================================================================
Omit Identifier to install default version 21.0.7-tem:
    $ sdk install java
Use TAB completion to discover available versions
    $ sdk install java [TAB]
Or install a specific version by Identifier:
    $ sdk install java 21.0.7-tem
```


已安装的Java版本的二进制文件可以在*SDKMAN！*的主目录中找到，该目录默认为~/.sdkman/candidates/java
```shell
(⎈|kubeasz-test:kafka)➜  ~ ls ~/.sdkman/candidates/java
21.0.7-zulu current
```




## 参考
- https://sdkman.io/install
