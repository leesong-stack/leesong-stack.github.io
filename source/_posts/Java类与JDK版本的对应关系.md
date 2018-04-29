---
title: Java类与JDK版本的对应关系
date: 2018-04-27 20:55:57
tags:
	- Java
	
categories: 技术
---

> Java的源文件经过编译后，得到对应的的class文件，它是一个二进制文件，其中前四个字节是 **magic** 位，第 5-8 字节为 **minor** 和 **major**，下面是这个类文件版本与JDK的对应关系：


|    jdk    |   major  |   minor  |
| :-------: | :-------:| :------: |
|    1.0	|    45    |  	3     |
|  	 1.1	|    45    |    3	  |
|  	 1.2	|  	 46	   | 	0	  |
|  	 1.3	|  	 47	   |    0	  |
|  	 1.4	|  	 48	   |	0	  |
|  	 1.5	|  	 49	   |	0	  |
|  	 1.6	|  	 50	   |	0	  |
|  	 1.7	|  	 51	   |	0	  |
|    1.8    |    52    |    0     |

在我们引入第三方jar包的时候，有时会遇到如下类似的错误：

java.lang.UnsupportedClassVersionError: PR/Sort : Unsupported major.minor version 52.0
或  ...\xxxx.jar(org/xxx/xxx/xxx.class) 类文件具有错误的版本 50.0，应为 49.0

> **注：**这个错误是提示你，这个引入的类是在高版本jdk上编译的，而你现在使用的是低版本的jdk
小技巧：在class文件所在目录，可以使用 **javap** 命令查看版本号，如：
javap -verbose AGateway，会显示以下内容，找到 major version：

```java

public abstract class org.smslib.AGateway extends java.lang.Object

  SourceFile: "AGateway.java"

  InnerClass:

     #56= #29 of #54; //QueueManager=class org/smslib/AGateway$QueueManager of class org/smslib/AGateway

     #58= #10 of #54; //Statistics=class org/smslib/AGateway$Statistics of class org/smslib/AGateway

     public #60= #59 of #54; //GatewayAttributes=class org/smslib/AGateway$GatewayAttributes of class org/smslib/AGateway

     public final #62= #61 of #54; //AsyncEvents=class org/smslib/AGateway$AsyncEvents of class org/smslib/AGateway

     public final #64= #63 of #54; //GatewayStatuses=class org/smslib/AGateway$GatewayStatuses of class org/smslib/AGateway

     public final #66= #65 of #54; //Protocols=class org/smslib/AGateway$Protocols of class org/smslib/AGateway

     public final #136= #135 of #266; //MessageClasses=class org/smslib/InboundMessage$MessageClasses of class org/smslib/InboundMessage

     public final #170= #169 of #269; //DeliveryStatuses=class org/smslib/StatusReportMessage$DeliveryStatuses of class org/smslib/StatusReportMessage

  minor version: 0

  major version: 51

  Constant pool:
  ...

``` 

> 除此之外，还可以将class文件用文本编辑器以16进制格式打开，查找 **minor** 和 **major**

![](/images/jdk_major.minor.jpg)




