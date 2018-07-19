### 使用USRP和GNU Radio实现GPS位置伪造
#### 测试环境
```
内核：Linux PC 3.13.0-92-generic
OS：Ubuntu 14.04 Desktop x86
Python：2.7.6
GNU Radio：3.7.2.1
USRP：原装Ettus N210 + SBX-40
UHD：UHD_003.005.005-0-unknown
GNU C++：4.8.2 
```
#### 前言
前一阵子为了研究，单位给我配了一个USRP，有了这个USRP我就想好好利用起来，正好最近流行Pokemon GO，中国区的GPS又被封锁了，我就决定尝试一下通过物理方式来伪造一下GPS定位。按照惯例，现在github上看看有没有人已经做好了相关工作，一查，果然有个项目gps-sdr-sim正合我意。这个项目是一个日本人写的，我看其博客也正好测试了Pokemon GO，他博客里面讲了一些有关GPS和SDR的知识，对此感兴趣可以看看[他的博客](https://blog.goo.ne.jp/osqzss)。
#### 安装gps-sdr-sim
按照github该项目主页上的说明安装即可：

打开一个放源码包的目录，这里就以~/Applications/为例。
```Shell
cd /home/$USERNAME/Applications
git clone https://github.com/osqzss/gps-sdr-sim.git
cd /gps-sdr-sim
sudo make
```
只要有GCC应该就能安装成功，安装成功后可以在gps-sdr-sim目录下看到gps-sdr-sim这个程序。
#### gps-sdr-sim原理
