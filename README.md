# FQ-BalanceCar

# 一、硬件介绍
主控芯片用的是100脚的STM32F103VET6，陀螺仪用的是MPU6050，电机驱动用的是TB6612，蓝牙是汇承的HC05邮票孔封装的，WIFI用的是济南有人科技的USR-WIFI232-S，小车底盘用的是平衡小车之家的某一款带编码器的（不是我买的，同学的），电池用的是一节7.2的镍镉电池，液晶用的是中景园电子1.3寸IIC接口的OLED，开关用的是三脚纽子开关，电池接口用的是T插，电阻电容这些用的基本上是0603封装，编码器5V降压用的是ASM1117-5.0，3.3V降压用的是SP6203，拨码开关用的是4P贴片式2.54mm角距的，按键是两脚贴片，microusb接口用的是5针 7.2四脚插板牛角母座，超声波是某宝上几块钱烂大街的那种，蜂鸣器是有源的，编码器是小车底盘自带的，电池电压检测是电阻分压之后通过电压跟随器接入MCU内部AD测量的。

# 二、主控板资源介绍

STM32F103VET6主控芯片；两个microusb口，第一个是MCU的串口1，可作为普通的串口收发数据，通过调节板上BOOT选项，也可将其作为ISP下载程序接口；第二个是SWD硬件仿真接口；蓝牙模块，与MCU的串口2连接；WIFI模块，与MCU的串口3相连；一块1.3寸IIC协议的液晶接口；超声波接口；双电机驱动；六轴陀螺仪；电池电压检测；4个用于调试的LED；4个独立式按键；一组4P的拨码开关；有源蜂鸣器；两个6P带AB相编码器的电机接口。

# 三、软件介绍

这份配套的软件，也算是我一点一点黏贴拼凑实测出来的，模块分的很清楚。再来说一下个人的感觉吧，网上资料一大堆，但是大多都是只有程序，没有对应的较为完整电路原理图。很少见到软硬件全部开源并且能够对应的资料。所以就带来这样一个后果，我们用别人的程序，我们自己画的电路。举个例子，某宝上卖这个的程序我看过，个人觉得，如果不搭配他的硬件，想用自己的硬件而直接把他的软件工程拿过来修改的话，很烦很乱基本上是扯淡。因为里面东西牵涉太多，你第一次做并不知道哪些是无关紧要哪些是必不可少的，比如蓝牙的遥控部分，超声波部分啊等等这些在他完整版的工程里面都是写好的，再者我们肯定是先调直立环，然后在调试速度环和方向环，所以你把他完整版的工程拿过来用，你告诉我怎么删减或者怎么注释掉速度环、方向环和一些锦上添花的功能模块呢？还有很多地方都是寄存器直接配置，我完全看不懂不知道怎么修改，一头雾水。所以最好的办法就是，参照别人的程序，一点一点自己粘贴然后修改底层搭建自己的工程。或者你也可以把自己的电路画的跟别人的一样，避免修改别人的底层，这样你粘贴过来甚至都不用改就能用了。

最后简单展示一下分享的资源，至于源文件全部在最后。

这是电路原理图：
![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9zdGF0aWMuZHkyMDguY24vb18xZGVyY2RrNTMxOGFmMW5mazF2dDM1b2cxZXAxYS5wbmc)

这是PCB图：
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9zdGF0aWMuZHkyMDguY24vb18xZGVyY2ZtM205aW0xYjBkMXFlMDEwbjRxcHVhLnBuZw)

这是打样好的PCB：

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9zdGF0aWMuZHkyMDguY24vb18xZGVyY2hjbjExbXRrOHI3MWE1NGZlNzRwa2EucG5n)
这是程序框架图：
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9zdGF0aWMuZHkyMDguY24vb18xZGVyY2syc2FxbXExb2hyanR2MThucjZrdWEucG5n)

这是最后搭建好的实物图：
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9zdGF0aWMuZHkyMDguY24vb18xZGVyY2tqbm0xMTJjMWl1bjE1NGoxZHVsMWRyZmEucG5n)

原文：
[https://blog.csdn.net/qq_37449342/article/details/94571624?utm_medium=distribute.pc_feed.none-task-blog-personrec_tag-6.nonecase&dist_request_id=1328741.28592.16169294695837457&depth_1-utm_source=distribute.pc_feed.none-task-blog-personrec_tag-6.nonecase](https://blog.csdn.net/qq_37449342/article/details/94571624?utm_medium=distribute.pc_feed.none-task-blog-personrec_tag-6.nonecase&dist_request_id=1328741.28592.16169294695837457&depth_1-utm_source=distribute.pc_feed.none-task-blog-personrec_tag-6.nonecase)