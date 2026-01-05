# nexus( Nexus Repository Manager ）

它是一个强大的仓库管理器，极大地简化了内部仓库的维护和外部仓库的访问。



## Nexus私服的优点
1.节省外网带宽：大量对中央仓库的重复请求会消耗带宽，利用私服代理外部仓库，可以避免重复的公网下载降低带宽的压力。

2.加速maven的构建：maven通过内网从私服拉取所需构件（私服存在此构件的情况下），获取构件的速度大大加快，从而加快打包构件的速度。

3.部署第三方构件：开发人员自己封装的一些jar包（工具类），可以部署到私服，以便内部开发人员的maven项目使用。

4.提高稳定性：当公网网络不稳定的时候，如果使用远程仓库，maven的构建也会变得不稳定。如果在私服存在所需的构件，即使没有公网，maven的构件也会顺利进行。

5.降低中央仓库的负荷：使用私服，避免了从中央仓库的重复下载，可以减轻中央仓库的负荷。


## Repository

仓库分为三种：Proxy、hosted、group


### Proxy
代理中央Maven仓库，当PC访问中央库的时候，先通过Proxy下载到Nexus仓库，然后再从Nexus仓库下载到PC本地。


### Hosted
Hosted是宿主机的意思，用于将第三方的Jar或者我们自己的jar放到私服上。

Hosted有三种方式，Releases、SNAPSHOT、Mixed

Releases: 一般是已经发布的Jar包

Snapshot: 未发布的版本

Mixed：混合的

###  Group
能把多个仓库合成一个仓库来使用



## 参考

- https://help.sonatype.com/en/ce-onboarding.html
- https://github.com/sonatype/docker-nexus3
- [Nexus3 功能介绍](https://blog.csdn.net/bbj12345678/article/details/115299019)
