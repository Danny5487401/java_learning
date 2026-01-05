<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [gradle](#gradle)
  - [参考](#%E5%8F%82%E8%80%83)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# gradle


Gradle是一个构建工具。Gradle是一种基于Groovy语言的自动化构建工具,它结合了Ant的配置方式和Maven的依赖管理功能,使用基于Groovy的特定领域语言(DSL)来声明项目设置,增强了灵活性和可扩展性。

![gradle_all.png](gradle_all.png)


## 生命周期

### 1）Initialization初始化阶段

通过settings.gradle 判断有哪些项目需要初始化，加载所有需要初始化的项目的build.gradle文件 并为每个项目创建project对象

### 2）Configuration配置阶段


执行各项目下的build.gradle脚本，完成project的配置，并且构造Task任务依赖关系图以便在执行 阶段按照依赖关系执行Task中的配置代码

### 3）Execution执行阶段

通过配置阶段的Task图，按II贿执行需要执行的任务中的动作代码，就执行任务中写在doFirst或 doLast中的代码


## 配置

### build.gradle

![img.png](build_gradle.png)


```groovy
// https://github.com/apache/kafka/blob/f745dfdcee2b9851204ddbbcd423626ab87294bc/build.gradle
```


sourceCompatibility: 指定使用哪个版本的JDK语法来编译源代码



#### 仓库配置 (Repositories)
在Gradle中，仓库的配置顺序很重要，因为Gradle会按照配置的顺序从上到下依次搜索所需的jar包。一旦找到所需的依赖，Gradle将停止搜索，继续进行构建.

1. 本地文件系统仓库：通过file协议指定本地磁盘目录作为仓库，这种方式不常用。

2. Maven本地仓库：mavenLocal()配置允许Gradle在本地Maven仓库中查找依赖。

3. 第三方镜像仓库：例如Alibaba和Bstek，这些是公共的Maven仓库镜像，通常用于加速依赖下载，特别是在某些地区访问Maven中央仓库速度较慢时。

4. Maven中央仓库：mavenCentral()配置允许Gradle查找默认的Maven中央仓库，这是最常用的远程仓库之一。

5. Google仓库：google()配置允许Gradle查找Google的远程仓库，这通常包含了一些Android开发常用的库。

#### allprojects和subprojects配置
在Gradle中，allprojects和subprojects允许你为多个项目（包括根项目和所有子项目）统一配置一些构建设置。

- allprojects：对根项目以及所有子项目进行统一配置。
- subprojects：仅对所有子项目进行统一配置


#### ext（extension）属性
允许用户在Project和Task对象中定义自定义属性。这些属性可以在构建脚本中读取和设置，也可以通过代码块一次性定义多个属性。

```groovy

ext {
  gradleVersion = versions.gradle
  minJavaVersion = 8
  buildVersionFileName = "kafka-version.properties"

  defaultMaxHeapSize = "2g"
  defaultJvmArgs = ["-Xss4m", "-XX:+UseParallelGC"]
  
}
```


#### Buildscript
buildscript块用于定义Gradle构建过程中所需的依赖，这些依赖通常是一些插件或库，它们对于执行构建脚本是必要的。buildscript必须位于build.gradle文件的最前端


## 基本概念

### project
一个project代表一个正在构建的组件（jar/war），当开始构建时，gradle会基于build.gradle实例化出一个Project对象，并通过project来调用其成员。



### Task
Gradle中内置了一些任务，比如build、clean等，也可以自定义任务



## 命令

### gradlew（gradle wrapper）

对gradle的命令进行了包装.gradlew与gradlew.bat: gradlew为Linux下的shell脚本，gradlew.bat是Windows下的批处理文件

```shell
# 查看帮助信息
(⎈|sandbox:default)➜  kafka git:(f745dfdcee) ./gradlew --help

To see help contextual to the project, use gradlew help

USAGE: gradlew [option...] [task...]

-?, -h, --help                     Shows this help message.
-a, --no-rebuild                   Do not rebuild project dependencies.
-b, --build-file                   Specify the build file. [deprecated]
--build-cache                      Enables the Gradle build cache. Gradle will try to reuse outputs from previous builds.
--no-build-cache                   Disables the Gradle build cache.
#  ...

```


```shell
# 查看所有任务
(⎈|sandbox:default)➜  kafka git:(f745dfdcee) ./gradlew tasks --all

> Configure project :
Starting build with version 3.9.1 (commit id f745dfdc) using Gradle 8.10.2, Java 11 and Scala 2.13.15
Build properties: maxParallelForks=8, maxScalacThreads=8, maxTestRetries=0

> Task :tasks

------------------------------------------------------------
Tasks runnable from root project 'kafka'
------------------------------------------------------------

Build tasks
-----------
assemble - Assembles the outputs of this project.
clients:assemble - Assembles the outputs of this project.
connect:assemble - Assembles the outputs of this project.
connect:api:assemble - Assembles the outputs of this project.
# ....


# 清除build文件夹
(⎈|sandbox:default)➜  kafka git:(f745dfdcee) ./gradlew clean



```







## 参考

- https://docs.gradle.org/current/userguide/getting_started_eng.html
- [Gradle 进阶学习 之 build.gradle 文件](https://cloud.tencent.com/developer/article/2414880)