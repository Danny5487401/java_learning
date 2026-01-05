<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [JVM (Java Virtual Machine Java虚拟机)](#jvm-java-virtual-machine-java虚拟机)
  - [文件格式](#文件格式)
    - [JAR（Java Archive，Java 归档文件）](#jarjava-archivejava-归档文件)
    - [WAR(Web Application Archive )](#warweb-application-archive-)
  - [ide 配置](#ide-配置)
    - [1  IntelliJ IDEA](#1--intellij-idea)
    - [2 vscode](#2-vscode)
  - [JVM JRE JDK](#jvm-jre-jdk)
    - [JDK 工具](#jdk-工具)
  - [java 文件运行过程](#java-文件运行过程)
    - [java 编译过程](#java-编译过程)
    - [Java虚拟机加载Java类](#java虚拟机加载java类)
    - [java 对象内存布局](#java-对象内存布局)
    - [JVM GC](#jvm-gc)
    - [JVM 启动参数详解](#jvm-启动参数详解)
      - [设置堆内存](#设置堆内存)
  - [参考](#参考)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# JVM (Java Virtual Machine Java虚拟机)

Java虚拟机，是Java程序的运行环境（Java二进制字节码.class的运行环境）。
VM 本质上也是一个应用程序，启动以后加载执行 Java 字节码文件。


## 文件格式

### JAR（Java Archive，Java 归档文件）
与平台无关的文件格式，它允许将许多文件组合成一个压缩文件，为 J2EE 应用程序创建的jar文件是 EAR 文件（企业 jar文件），jar文件格式以流行的 ZIP 文件格式为基础。
与 ZIP 文件不同的是，jar文件不仅用于压缩和发布，而且还用于部署和封装库、组件和插件程序，并可被像编译器和 JVM 这样的工具直接使用。在 jar中包含特殊的文件，如 manifests 和部署描述符，用来指示工具如何处理特定的 jar。


### WAR(Web Application Archive )

一个web程序进行打包便于部署的压缩包，里面包含我们web程序需要的一些东西，其中包括web.xml的配置文件，前端的页面文件，以及依赖的jar。

Web存档(war)文件包含Web应用程序的所有内容。它减少了传输文件所需要的时间。

## ide 配置

### 1  IntelliJ IDEA 

### 2 vscode 
https://code.visualstudio.com/docs/languages/java



## JVM JRE JDK
![img.png](jvm_jre.png)

* JRE: Java Runtime Environment（Java运行时环境）
* JDK：Java Development Kit（Java开发工具包）



Java分为三个体系：

- JavaSE(J2SE)(Java2 Platform Standard Edition，java平台标准版）
- JavaEE(J2EE)(Java 2 Platform,Enterprise Edition，java平台企业版)
- JavaME(J2ME)(Java 2 Platform Micro Edition，java平台微型版)。


JRE = JVM + 类库

JDK = 包括了 Java 运行时的环境（JRE）、解释器（Java）、编译器（javac）、Java 归档（jar）、文档生成器（Javadoc）等工具.
由于Eclipse等IDE具有自己的编译器，所以只需要JRE就可以了

### JDK 工具

 JPS，用于展示 Java 进程信息（列表


jstat 用来监控 JVM 内置的各种统计信息，主要是内存和 GC 相关的信息。

jmap 主要用来 Dump 堆内存。当然也支持输出统计信息。官方推荐使用 JDK 8 自带的 jcmd 工具来取代 jmap，但是 jmap 深入人心.


jstack 工具可以打印出 Java 线程的调用栈信息（Stack Trace）。一般用来查看存在哪些线程，诊断是否存在死锁等。

## java 文件运行过程

![img.png](java_process.png)
Java 虚拟机将运行时内存区域划分为五个部分，分别为方法区、堆、PC 寄存器、Java 方法栈和本地方法栈。

从虚拟机视角来看，执行 Java 代码首先需要将它编译而成的 class 文件加载到 Java 虚拟机中。加载后的 Java 类会被存放于方法区（Method Area）中。实际运行时，虚拟机会执行方法区内的代码。


### java 编译过程

从硬件视角来看，Java 字节码无法直接执行。因此，Java 虚拟机需要将字节码翻译成机器码。

常见的编译型语言如C++，通常会把代码直接编译成CPU所能理解的机器码来运行。
而Java为了实现“一次编译，处处运行”的特性，把编译的过程分成两部分，首先它会先由javac编译成通用的中间形式——字节码，然后再由解释器逐条将字节码解释为机器码来执行。
所以在性能上，Java通常不如C++这类编译型语言。

为了优化Java的性能 ，JVM在解释器之外引入了JIT（Just In Time Compiler 即时编译器)：当程序运行时，解释器首先发挥作用，代码可以直接执行。
随着时间推移，即时编译器逐渐发挥作用，把越来越多的代码编译优化成本地代码，来获取更高的执行效率。


java代码首先要通过前端编译器编译成.class字节码文件，然后再按一定的规则加载到JVM（java 虚拟机）内运行。 
有三种运行方式，解释模式（javac）、编译模式（C1 JIT、C2 JIT）、混合模式（javac+（C1 OR C2））

解释模式下，一边执行字节码一边解释执行；
编译模式下，字节码编译为机器码后执行；
混合模式下，正常情况下使用解释执行，但是针对经常执行的代码，会采用JIT技术进行编译执行。


Hotspot中有两个即时编译器，分别为Client Compiler（C1 JIT)和Server Compiler(C2 JIT)，
C1 又叫做 Client 编译器，面向的是对启动性能有要求的客户端 GUI 程序，采用的优化手段相对简单，因此编译时间较短。
C2 又叫做 Server 编译器，面向的是对峰值性能有要求的服务器端程序，采用的优化手段相对复杂，因此编译时间较长，但同时生成代码的执行效率较高。

从JDK 9开始，Hotspot VM中集成了一种新的Server Compiler，Graal编译器。


### Java虚拟机加载Java类

从 class 文件到内存中的类，按先后顺序需要经过加载、链接以及初始化三大步骤。

加载，是指查找字节流，并且据此创建类的过程。

链接，是指将创建成的类合并至 Java 虚拟机中，使之能够执行的过程。

类加载的最后一步是初始化，便是为标记为常量值的字段赋值，以及执行 < clinit > 方法的过程


### java 对象内存布局


### JVM GC


![img.png](eden_from_to.png)

JVM 将堆空间分成新生代（young）和老年代（old）两个区域，创建对象的时候，只在新生代创建，当新生代空间不足的时候，只对新生代进行垃圾回收，这样需要处理的内存空间就比较小，垃圾回收速度就比较快。


年轻代又会分为Eden和Survivor区。Survivor 也会分为FromPlace和ToPlace，toPlace 的 survivor 区域是空的,每次垃圾回收都是扫描 Eden 区和 From 区，将存活对象复制到 To 区，然后交换 From 区和 To 区的名称引用，下次垃圾回收的时候继续将存活对象从 From 区复制到 To 区。
当一个对象经过几次新生代垃圾回收，也就是几次从 From 区复制到 To 区以后，依然存活，那么这个对象就会被复制到老年代区域。


当老年代空间已满，也就是无法将新生代中多次复制后依然存活的对象复制进去的时候，就会对新生代和老年代的内存空间进行一次全量垃圾回收，即 Full GC。
所以根据应用程序的对象存活时间，合理设置老年代和新生代的空间比例对 JVM 垃圾回收的性能有很大影响，JVM 设置老年代新生代比例的参数是 -XX:NewRatio。




垃圾回收器有四种:


1. 第一种是 Serial 串行垃圾回收器，这是 JVM 早期的垃圾回收器，只有一个线程执行垃圾回收。

2. 第二种是 Parallel 并行垃圾回收器，它启动多线程执行垃圾回收。
如果 JVM 运行在多核 CPU 上，那么显然并行垃圾回收要比串行垃圾回收效率高。在串行和并行垃圾回收过程中，当垃圾回收线程工作的时候，必须要停止用户线程的工作，
否则可能会导致对象的引用标记错乱，因此垃圾回收过程也被称为 stop the world，在用户视角看来，所有的程序都不再执行，整个世界都停止了。

3. 第三种 CMS 并发垃圾回收器，在垃圾回收的某些阶段，垃圾回收线程和用户线程可以并发运行，因此对用户线程的影响较小。Web 应用这类对用户响应时间比较敏感的场景，适用 CMS 垃圾回收器。

4. 最后一种是 G1 垃圾回收器，它将整个堆空间分成多个子区域，然后在这些子区域上各自独立进行垃圾回收，在回收过程中垃圾回收线程和用户线程也是并发运行。
G1 综合了以前几种垃圾回收器的优势，适用于各种场景，是未来主要的垃圾回收器。


大类分成两种类型，一种是响应速度快，一种是吞吐量高。通常情况下，CMS 和 G1 回收器的响应速度快，Parallel Scavenge 回收器的吞吐量高。

```shell
# java -version
openjdk version "1.8.0_171"
OpenJDK Runtime Environment (build 1.8.0_171-8u171-b11-0ubuntu0.16.04.1-b11)
OpenJDK 64-Bit Server VM (build 25.171-b11, mixed mode)
# jcmd 7 VM.flags
7:
-XX:CICompilerCount=12 -XX:InitialHeapSize=2107637760 -XX:MaxHeapSize=32210157568 -XX:MaxNewSize=10736369664 -XX:MinHeapDeltaBytes=524288 -XX:NewSize=702545920 -XX:OldSize=1405091840 -XX:+UseCompressedClassPointers -XX:+UseCompressedOops -XX:+UseParallelGC
```
到 jdk8 为止，默认的垃圾收集器是 Parallel Scavenge 和 Parallel Old.
从 jdk9 开始，G1 收集器成为默认的垃圾收集器 目前来看，G1 回收器停顿时间最短而且没有明显缺点，非常适合 Web 应用。



在 jdk8 中测试 Web 应用，堆内存 6G，新生代 4.5G 的情况下，Parallel Scavenge 回收新生代停顿长达 1.5 秒。G1 回收器回收同样大小的新生代只停顿 0.2 秒

垃圾收集事件（Garbage Collection events）可以分为三种类型：

- Minor GC（小型 GC）: 年轻代 GC”（Young GC)
- Major GC（大型 GC）: 清理老年代空间（Old Space）的 GC 事件。
- Full GC（完全 GC）: 清理整个堆内存空间的 GC 事件，包括年轻代空间和老年代空间。





### JVM 启动参数详解
```shell
$ java                                                                     

用法: java [-options] class [args...]
           (执行类)
   或  java [-options] -jar jarfile [args...]
           (执行 jar 文件)
```

- [options] 部分称为 “JVM 选项”,对应 IDE 中的 VM options, 可用 jps -v 查看。
- [args] 部分是指 “传给main函数的参数”, 对应 IDE 中的 Program arguments, 可用 jps -m 查看


JVM 的启动参数, 从形式上可以简单分为：

* 以-开头为标准参数，所有的 JVM 都要实现这些参数，并且向后兼容。
* 以-X开头为非标准参数， 基本都是传给 JVM 的，默认 JVM 实现这些参数的功能，但是并不保证所有 JVM 实现都满足，且不保证向后兼容。
* 以-XX:开头为非稳定参数, 专门用于控制 JVM 的行为

```shell
# 查看默认的所有系统属性
java -XshowSettings:properties -version
Property settings:
    awt.toolkit = sun.lwawt.macosx.LWCToolkit
    file.encoding = UTF-8
    file.encoding.pkg = sun.io
    file.separator = /
    gopherProxySet = false
    java.awt.graphicsenv = sun.awt.CGraphicsEnvironment
    java.awt.printerjob = sun.lwawt.macosx.CPrinterJob
    java.class.path = .
    java.class.version = 52.0
    java.endorsed.dirs = /Users/python/.sdkman/candidates/java/8.0.472.fx-zulu/zulu-8.jdk/Contents/Home/jre/lib/endorsed
    java.ext.dirs = /Users/python/Library/Java/Extensions
    # ...
```

常见配置
```shell
# 设置堆内存
-Xmx4g -Xms4g 
# 指定 GC 算法
-XX:+UseG1GC -XX:MaxGCPauseMillis=50 
# 指定 GC 并行线程数
-XX:ParallelGCThreads=4 
# 打印 GC 日志
-XX:+PrintGCDetails -XX:+PrintGCDateStamps 
# 指定 GC 日志文件
-Xloggc:gc.log 
# 指定 Meta 区的最大值
-XX:MaxMetaspaceSize=2g 
# 设置单个线程栈的大小
-Xss1m 
# 指定堆内存溢出时自动进行 Dump
-XX:+HeapDumpOnOutOfMemoryError 
-XX:HeapDumpPath=/usr/local/
```




#### 设置堆内存
JVM 总内存=堆+栈+非堆+堆外内存。

助记的话：
- Xmx:  memory maximum  最大堆大小
- Xms： memory startup 初始堆大小
- Xmn: memory nursery/new 年轻代大小.等价于 -XX:NewSize,使用 G1 垃圾收集器 不应该 设置该选项，在其他的某些业务场景下可以设置。官方建议设置为 -Xmx 的 1/2 ~ 1/4。
- Xss: stack size 每个线程的堆栈大小.例如 -Xss1m 指定线程栈为 1MB，与-XX:ThreadStackSize=1m等价





## 参考
- [大白话带你认识 JVM](https://javaguide.cn/java/jvm/jvm-intro.html)
- [后端技术面试 38 讲 03丨Java虚拟机原理：JVM为什么被称为机器（machine）？](https://time.geekbang.org/column/article/168945)
- [深入拆解Java虚拟机](https://learn.lianglianglee.com/%e4%b8%93%e6%a0%8f/%e6%b7%b1%e5%85%a5%e6%8b%86%e8%a7%a3Java%e8%99%9a%e6%8b%9f%e6%9c%ba/03%20%20Java%e8%99%9a%e6%8b%9f%e6%9c%ba%e6%98%af%e5%a6%82%e4%bd%95%e5%8a%a0%e8%bd%bdJava%e7%b1%bb%e7%9a%84.md)
 