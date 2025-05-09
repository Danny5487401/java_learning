
## maven 
Maven是一个项目管理工具，它包含了一个对象模型。一组标准集合，一个依赖管理系统。和用来运行定义在生命周期阶段中插件目标和逻辑。


Maven的核心功能是合理叙述项目间的依赖关系，通俗点 就是通过pom.xml文件的配置获取jar包不用手动的去添加jar包

## 配置


settings.xml 中包含类似本地仓储位置、修改远程仓储服务器、认证信息等配置。

- settings.xml 是 maven 的全局配置文件。
- pom.xml 文件是本地项目配置文件。


pom.xml > user settings > global settings



仓库就是存放jar包的地方，即我们前面说的通过pom.xml中通过设置索引来到仓库中寻找jar包
仓库分为：本地仓库，第三方仓库，中央仓库

![img.png](repository.png)

获取jar包的过程:
优先从本地仓库查找，如果本地仓库没有该jar包，如果配置了私服，就从私服中查找，私服中没有就从中央仓库中查找，然后下载到本地仓库，下次使用就可以直接从本地仓库中查找，没有配置私服则，直接从中央仓库中查找


## Maven项目结构

一个使用Maven管理的普通的Java项目，它的目录结构默认如下：

a-maven-project
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   └── test
│       ├── java
│       └── resources
└── target


项目的根目录a-maven-project是项目名，它有一个项目描述文件pom.xml，存放Java源码的目录是src/main/java，存放资源文件的目录是src/main/resources，
存放测试源码的目录是src/test/java，存放测试资源的目录是src/test/resources，
最后，所有编译、打包生成的文件都放在target目录里。这些就是一个Maven项目的标准目录结构


## mvn 命令


## 参考
- https://github.com/apache/maven
- [Maven 教程之 settings.xml 详解](https://cloud.tencent.com/developer/article/1522574)
- [Java-Maven详解](https://www.cnblogs.com/liugp/p/16221170.html)