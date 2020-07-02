# nas挖坑日记

> 在B站UP主司波图的安利下，我也算入了nas的坑。作为一名性价比玩家，肯定是不会买群晖的，有考虑过威联通的453bm，但据说要出新款了，所以暂时先diy。

### 价格

某宝和咸鱼购买，配件列表

| cpu    |           g3260t           | 45   |
| ------ | :------------------------: | ---- |
| 内存   |     威刚拆机2g ddr3 x2     | 34   |
| 硬盘   | 图吧玩家自用西数蓝盘500gx3 | 150  |
| 准系统 |    闲鱼hp prodesk 600g1    | 220  |
| 视频线 |          dp转vga           | 2.5  |
| 系统盘 |        全新闪迪16g         | 25   |
| sata线 |         sata3.0 x8         | 18   |
|        |                            | 495  |

###### 参考视频

[400元神机gt320t](https://www.bilibili.com/video/BV18E411o79E)



### 需求

> 这次nas的需求：
>
> 1.整理杂乱的影视文件，添加封面等信息
>
> 2.局域网smb或者nfs文件共享
>
> 3.外网访问



### htpc选择（htpc即影音软件）

第一点需求可以用kodi或者jellyfin实现，这俩不同的是，kodi的影音文件存在本地，jellyfin存在服务器（docker里的镜像）。

###### kodi

kodi适合电视盒子专用nas,他是通过smb/nfs共享协议来读取的。

###### jellyfin

jellyfin适合外网访问，比如会在外网访问。jellyfin也可以实现安卓ios访问（需要公网ip）。或者家庭电视访问，一般电视都会有smb/nfs协议，通过共享协议读取视频。若需要读取服务器的封面，则可以在电视安装kodi,kodi里有jellyfin for kodi得插件，通过插件，可以在电视端同步jellyfin服务器的封面信息。

###### 现状

总体来说jellyfin用途更广一点，但因为我没有公网ip,所以别的设备读取不到。目前也没有电视的需求。所以打算nas装docker jellyfin插件，然后电脑ping 内网ip加端口访问控制台，在电脑播放。

###### jellyfin外网访问

[jellyfin别的设备或者外网访问的视频](https://www.bilibili.com/video/BV1AE411k7hr)

注意：没有公网ip也不能外网访问，不要搞花生壳蒲公英frp之类的穿透，又贵又慢。说要安装监控索去跟运营商要ipv4公网ip。

测试是不是公网ip,看路由器中的ip地址，与百度搜素，我的Ip，前两组是否一致，不一致，那就是大路由dhcp分配的内网Ip地址。

> dhcp:即内网自动分配ip地址的协议



### 系统的选择-omv

> 不想折腾，所以弃用黑群晖。
>
> freenas以后有空再玩，选择开源的omv系统。

[omv系统安装](https://www.bilibili.com/video/BV1FJ411s7xR)

[hp准系统](https://www.bilibili.com/video/BV16z4y1R758)

[omv与htpc](https://www.bilibili.com/video/BV1Ge41147B9)



注意：安装（omv）linux，系统不推荐安装在nvme或者usb上，因为这两者在盘符识别时总是在sata之后，若安装系统后，又加入新硬盘，就会导致系统盘符发生变化，此时需要update-grub里更新引导，对于硬盘经常变化的nas来说，这个操作太过频繁。

系统盘一般放在第一个sata口，或者保证该口之前的接口不再增减硬盘。



### docker

> 不选择群晖威联通之类的方案，就是因为可以用docker实现他们系统的大部分套件，所以docker的使用很重要，玩好docker，需要内存不能太小，cpu也不能太弱。



[docker入门](https://www.bilibili.com/video/BV1eE411i7qy)

[docker image的地址](hub.docker.com)



##### docker结构

docker与虚拟机在结构上是类似的，只是docker要更轻量。

![image-20200702101004975](https://gif-clark-cui.oss-cn-beijing.aliyuncs.com/blog/image-20200702101004975.png)

除了固定物理层和系统层外，虚拟机有一个模拟环境比如vmware,而docker是一个docker damon或者docker enginee。

docker里会有container，是一个容器，而image则是应用和应用的配置环境。



##### container的映射

重启不会删除docker里container配置和文件,但每一次针对Container的修改都会，所以需要对container里的文件做文件映射。



##### docker的网络设置

docker里container的网络设置有3种，bridge/host/custome

1. bridge会生成内网ip，需要做主系统映射才能访问
2. Host会让主系统ip和docker ip同样，不需要映射
3. custome会在主路由内生成一个内网ip，与主系统ip同级，所以不需要映射。custome是网卡模式，有几张网卡就有几个custome。

### 硬盘

###### 现状

成本考虑，目前暂用二手拆机西数蓝盘。

###### 综合考虑

避免叠瓦盘，比如很贵的西数红盘，据说希捷酷狼也是叠瓦盘，可以选择希捷银河企业盘。