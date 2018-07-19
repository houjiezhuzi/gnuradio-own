### Ubuntu14.04下GNU Radio的安装以及USRP N210配置
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
#### GNU Radio安装
##### 使用apt-get安装组件
```Shell
sudo apt-get install gnuradio
```
##### 测试GNU Radio安装情况
打开GNU Radio
```Shell
sudo gnuradio-companion
```
成功打开GNU Radio的话代表GNU Radio安装成功。
![usep1](/images/usrp_1.png)
注意：最好使用su -命令来切换到root账户再打开GNU Radio，不然会出现一些环境变量的错误提示。
#### USRP配置
我使用的是原装的Ettus USRP N210设备，是千兆网口连接的型号，一定要记得使用千兆网卡和千兆网线，一开始我使用了百兆的USB网卡连接之后并没有成功，具体是不是因为这个原因我也不太清楚，但是最好还是按照设备的规格来找适配的连接硬件。因为在使用USRP的时候一般还需要联网，所以最好配双网卡，一张网卡连接外网一张网卡连接USRP设备。

注意：配置的时候外网的配置不变，和USRP连接的网络配置路由那一栏留空。
#### 连接
使用网线把USRP和PC通过网线直连连接在一起，接通USRP电源。
#### 配置网络
因为USRP N210是将PC和自己直连，所以我们要配置好内网的环境。根据官网的说明，N210的内网IP出厂默认的是192.168.10.2，所以我们就要将我们的PC配置成192.168.10.1，好让PC和USRP处于同一个网段。
```
1.点击最上方靠右的网络连接标志，点Edit Connection按钮（这里根据语言的不同选择对应的选项）。
2.选择对应网卡的连接，点击Edit按钮。（注意：对应网卡的名称可以通过右上角的菜单看到。）
3.点击IPv4 Settings选项卡，吧Method从DHCP状态改成Manual，即手动配置IP。
4.在下面地址栏添加一个新的地址：192.168.10.1-255.255.255.0-留空，点保存，DNS服务器可以不填。
```
[这里写图片描述](/images/usrp_2.png)

注意：这里配置的时候记得选择连接USRP的网卡，不要配错了。
#### 测试连接
配好网络后应该就会有提示网络已经连接，如果没有试试刷新一下网络连接。打开终端，ping USRP的地址ping 192.168.10.2，如果ping通了就代表连接成功了。
[这里写图片描述](/images/usrp_3.png)
#### 测试USRP驱动情况
连接上了USRP还没有完成工作，还需要USRP的驱动UHD是不是匹配的，如果不匹配的话需要按照教程把和PC配对的固件烧录到USRP中。

在终端中输入命令sudo uhd_usrp_probe，驱动成功的话会显示形如这样的信息：
