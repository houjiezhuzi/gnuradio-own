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
前一阵子为了研究，单位给我配了一个USRP，有了这个USRP我就想好好利用起来，正好最近流行Pokemon GO，中国区的GPS又被封锁了，我就决定尝试一下通过物理方式来伪造一下GPS定位。按照惯例，现在github上看看有没有人已经做好了相关工作，一查，果然有个项目[gps-sdr-sim](https://github.com/kaniel/gps-sdr-sim)正合我意。这个项目是一个日本人写的，我看其博客也正好测试了Pokemon GO，他博客里面讲了一些有关GPS和SDR的知识，对此感兴趣可以看看[他的博客](https://blog.goo.ne.jp/osqzss)。
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
这个项目的原理是gps-sdr-sim能根据指定的卫星信息文件、坐标信息、采样频率等参数输出二进制的信号文件，将这个二进制文件导入到USRP或者bladeRF之类的无线电射频设备上就可以实现GPS的伪造。
#### 卫星信息：
必备，可以在[nasa官网](ftp://cddis.gsfc.nasa.gov/gnss/data/daily/)下载到最新的信息文件，项目源码中已经包括了一个旧的信息文件brdc3540.14n也可以使用。
download: ftp://cddis.gsfc.nasa.gov/gnss/data/daily/
#### 坐标信息：
坐标信息有三种方式输入：
```
1.固定坐标
2.NMEA流文件
3.用户定义文件
```
其中，NMEA和用户定义文件是一系列的时间和坐标，可以伪造移动的GPS位置，具体的使用我还没有测试，我就先使用固定的坐标作为测试。
#### 采样频率：
采样频率相当于二进制文件每个坐标产生的频率，默认的是2600000Hz，但是USRP中，10000000Hz除以使用的采样频率必须是整数，不然就会出错，所以使用USRP的时候***我使用的是2500000Hz***。这个采样率过大或者过估计都会有问题，过小可能导致信号不稳定，过大可能在传输过程中会出现传输速度跟不上采样率，这样发出来的信号也是不稳定的。
#### 二进制文件格式：
输出的二进制文件有三种格式，分别有1-bit、8-bit、16-bit，默认使用的是16-bit的。但是USRP中，支持的是8-bit的二进制文件，所以一定要把***这个参数改成8-bit***，不然不成功。一开始早就在这个地方走了不少弯路，用了16-bit的输出的信号客户端设备根本识别不了，白忙活了一整天我都开始怀疑人生了。后来我用GNU Radio打开项目里面的输出的py文件，查看各个blocks，才发现第一个blocks是byte转short，而byte是8bits的，所以才搞明白是这里出了问题。
#### 频率：
这个是输出的信号的中心频率，默认是美国官方的GPS L1信号频段***1575420000Hz***，按照默认即可，如果不是默认的可能通用的GPS客户端设备不能收到信号。我不太清楚其他国家的GPS卫星的频段是多少，而且这里用的是NASA的卫星信息，估计伪造其他国家的GPS在这个卫星信息上也得重新修改一下，所以我就没有深入尝试。
#### 二进制信号持续时间：
这个参数决定了信号的持续时间，但是其实输出的时候是循环输出的，所以如果使用固定坐标的话不用太长。默认的是300s，这个时间越大生成的二进制文件也会越大，经过测试，固定坐标情况下30s多一点点就可以完成定位，所以使用60s以上应该都没有问题。但是为了保险起见，我这里保留了默认的***300s***。
#### gps-sdr-sim参数
```Shell
Usage: gps-sdr-sim [options]
Options:
  -e <gps_nav>     卫星信息文件(必须)
  -u <user_motion> 用户定义的坐标文件 (动态的位置信息)
  -g <nmea_gga>    NMEA坐标文件 (动态的位置信息)
  -l <location>    坐标，维度-经度-海拔，例如： 30.286502,120.032669,100
  -t <date,time>   模拟的开始时间 YYYY/MM/DD,hh:mm:ss
  -d <duration>    持续时间 [秒] (最大: 300)
  -o <output>      二进制文件的输出位置 (默认: gpssim.bin)
  -s <frequency>   采样频率 [Hz] (默认: 2600000)
  -b <iq_bits>     二进制文件格式 [1/8/16] (默认: 16)
  -v               更多细节信息
```
#### 产生二进制文件
项目页面上给了三种不同的输入坐标信息的方式：
```Shell
> gps-sdr-sim -e brdc3540.14n -u circle.csv
> gps-sdr-sim -e brdc3540.14n -g triumphv3.txt
> gps-sdr-sim -e brdc3540.14n -l 30.286502,120.032669,100
```
因为我们使用的是固定坐标和USRP的配置，所以我使用命令：
```Shell
> ./gps-sdr-sim -e brdc3540.14n -l [坐标] -s 2500000 -b 8
```
经过一段时间，就可以生成一个达到2.1G的二进制文件。
![t](/docs_zh/images/uhd_1.png)
提示：坐标信息可以在Google地图上左键点击你想要的位置查看到并输入。
![2](/docs_zh/images/uhd_2.png)
#### 导入USRP
注意：导入之前请确定USRP的工作情况，USRP的配置可以参考[Ubuntu14.04下GNU Radio的安装以及USRP N210配置](https://blog.csdn.net/sinat_26599509/article/details/51993813)。

导入USRP使用的是GNU Radio，其中项目中的py文件就是调用了GNU Radio的API，将二进制文件通过byte读入然后转成short，然后再从short转成complex输出到USRP Sink中。命令如下：
```Shell
> gps-sdr-sim-uhd.py -t gpssim.bin -s 2500000 -x 0
```
其中-s参数代表采样率，-x代表增益。

正常的情况下可以看到输出一个一个字母U，每一个U代表一次传输速度的不稳定，理想的情况是只有一个字母U，如果字母U出现的频率太快了说明采样率太高了。
![3](/docs_zh/images/uhd_3.png)
#### 测试结果
注意：定位过程需要一段时间，30s到一分钟，要耐心等待。
![4](/docs_zh/images/uhd_4.png)
![5](/docs_zh/images/uhd_5.jpg)
![6](/docs_zh/images/uhd_6.jpg)
#### 参考
```
gps-sdr-sim
```
