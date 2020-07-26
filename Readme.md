# 安卓apk逆向入门
## 环境
#### 说明
1. dex2jar-tools是用来转换 .dex 到 .jar 的  
2. JD-GUI是用来查看转换后的 .jar 的,用来分析代码  
3. JDK里有keytools可以生成签名  
4. JDK里的jarsigner可以给apk签名  
#### 下载网址
1. [JRE1.8 官网](https://www.oracle.com/java/technologies/javase-jre8-downloads.html)  
2. [JDK1.8 官网](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)  
3. [APKtool 官网](http://ibotpeaches.github.io/Apktool/install/)  
4. [JD-GUI 官网](http://jd.benow.ca/)  
5.  [dex2jar-tools-2.1.zip](https://raw.githubusercontent.com/TenmaSennpai/Android_Reverse/master/dex2jar-tools-2.1.zip) 
#### 安装要点
1. JRE和JDK需要加入PATH，一般是系统变量PATH  
2. APKtools的安装严格按官网来，这样后续会比较方便  
3. dex2jar-tools必须要安装2.1及以上的版本，支持Android N  
## 步骤
#### 命名说明
myapp1.apk 为要被逆向的apk名称  
test1.apk 为逆向后生成的apk名称  
demo.keystore 为生成的签名文件名称
#### 准备
准备一个apk文件，比如 myapp1.apk  
把apk移动到桌面，并解压，比如

    C:\Users\Kyaru\Desktop\myapp1
#### 转换
cd到dex-tools目录，powershell运行命令：

    .\d2j-dex2jar.bat C:\Users\Kyaru\Desktop\myapp1\classes.dex
（注：通常要转换好几个classes.dex）
#### 查看代码
打开JD-GUI，将转换好的全部.jar拖入JD-GUI开始分析
#### 反编译apk
cd到myapp1.apk所在目录，powershell运行命令：

    apktool d -o myapp1.apk
#### 更改代码
根据之前的分析，将反编译的smail等更改
#### 编译apk
cd到myapp1.apk所在目录，powershell运行命令：

    apktool b C:\Users\Kyaru\Desktop\release\myapp1 -o test1.apk
#### 生产签名文件
cd到test1.apk所在目录，powershell运行命令：

    keytool -genkey -alias demo.keystore -keyalg RSA -validity 40000 -keystore demo.keystore
#### 给apk签名： 
cd到test1.apk所在目录，powershell运行命令：

    jarsigner -verbose -keystore demo.keystore test1.apk demo.keystore
## 参考网址
[1]. [简单的Android逆向教程 - 52.pojie.cn](https://www.52pojie.cn/forum.php?mod=viewthread&tid=822434)  
[2]. [Smail基础教程 - blog.csdn.net](https://blog.csdn.net/yuanguozhengjust/article/details/80493963)  
[3]. [dex2jar-tools-2.0报错解决办法 - cnblog.com](https://www.cnblogs.com/onelikeone/p/7594177.html)
