### USRP配置与测试
安装完gnuradio和UHD之后，我们用USRP连接PC来做一些测试。却会遇到一些奇怪的问题，现将配置步骤记录如下
#### 实验平台
|环境 | 详情|
|-----|-----|
|电脑 |华硕n550|
|系统 | Ubuntu12.04|
|gnuradio | gnuradio-3.7.5|
|uhd |	UHD-Mirror-release_003_005_002|
|USRP 型号 |	HMUN210(北京海曼无限信息技术有限公司)|
#### 连接USRP至PC
```
以下操作均对 USRP 型号为HMUN 210来操作
```
为了保证USRP能够成功地连接至PC：
* 1.要保证PC端已成功的安装所需的软件（包括 GNU Radio和UHD或者其他能够控制USRP的软件）
* 2.保证射频子板已经正确安装至USRP母版（一般来说，买来的USRP已经封装好了）
* 3.在使用USRP时，要确保USRP和PC之间的物理连接已经正确建立。（对于USRP2或者USRP-N，应保证PC端所使用的以太网能支持千兆的传输速率，并且使用千兆网线传输，买来的HMUN210里面送了一根千兆的网线，用那个就可以了。当USRP2或者USRP N-SERIES设备端网口绿灯点亮时，说明USRP设备和PC端的网络连接已经成功建立。）
#### 配置USRP
由于UHD使用了UDP作为以太网通信协议，因此使用UHD和USRP2或者USRP N-Series时，应更改PC端IP地址。UHD 下USRP默认的IP地址为192.168.10.2.因此PC机对应网口的IP地址应配置如下

|网络配置 | 配置详情|
|----|--------|
|IP | 192.168.10.1|
|Mask(子网掩码） | 255.255.255.0|
|Gate | 192.168.10.2|

配置完成后，此时的有线网络应该可以与USRP连接上了，读者可以在终端中试试如下命令
```Shell
$ ping 192.168.10.2
```
如果有数据传输，就说明PC已经与USRP网络连接上了。
#### 更改FPGA程序
USRP N-Series 只能以UHD作为驱动，其FPGA比特流文件和firmware固件在gnuradio和UHD安装的时候已经安装好了，大家可以输入以下命令找到 usrp_n210_fw.bin 和 usrp_n210_r4_fpga_bin
```Shell
$ locate usrp_n210_fw.bin 
$ locate usrp_n210_r4_fpga_bin
```
笔者的这两个文件都在/usr/local/share/uhd/images/ 目录下。UHD 提供的SD卡刷写程序为 usrp_n2xx_net_burner_gui.py，找到这个文件，在终端中以管理员权限运行该程序
```Shell
 $./usrp_n2xx_net_burner_gui.py
 ```
 会有如下这个界面
 
 ![1](/images/usrp_s_1.png)
 
 其中，firmware Image选取usrp_n210_r4_fpga_bin，FPGA image选取 usrp_n210_fw.bin，Network Address的 IP地址填的是USRP的IP地址，也就是 192.168.10.2 ，点击Burn Images 即可。
#### 基本测试
在GNU Radio和UHD中，均提供了若干个程序可以用来测试USRP和PC之间的连接。在运行程序时请以管理员权限执行。
#### 基于GNU Radio 的测试
我们可以运行 usrp_rx_cfile.py 这个程序。
>注意：笔者运行凡是usrp开头的python文件，都会遇到 from gnuradio import usrp importerror cannot import name usrp,百度谷歌后觉得可能是usrp这个文件夹在用脚本文件编译的时候没有把usrp编译，导致报这个错误，具体解决办法还希望大神能够指导指导
#### 更新：2016-1-12 12:00
>对于上面问题所说的凡是usrp开头的python文件 都会遇到 from gnuradio import usrp importerror cannot import name usrp 。查了资料和问了一些大神，是因为最新版的gnuradio3.7.5已经用uhd文件将usrp 文件替换掉了，所以在安装完成之后，已经没有usrp这样的文件夹了，取而代之的是uhd文件夹。
至于usrp一些的demo文件，比如usrp_fft.py已经被uhd_fft.grc替换了。所以我们可以直接运行uhd_fft.grc.我们可以先看下uhd 下面有那些文件。输入
```Shell
$ cd /usr/local/share/gnuradio/examples/uhd 
$ ls
 ```
 在这里我们可以看到uhd文件夹下的文件。
 ![2](/images/usrp_s_2.png)
 我们可以跟以前的老版本的gnuradio下面usrp文件对比以下，可以发现，除了前面的usrp和uhd名字不一样，后面的很多文件都很相似。
 ![3](/images/usrp_s_3.png)
 所以，我们如果要做测试的话，需要使用最新版本的demo来做测试，因为自己的电脑装的是最新的gnuradio，而如果用老版本的demo来做测试的话，很多的modlue都更新了，运行的时候就会报import error。
 
 现在，让我们来运行以下uhd_fft.grc这个文件，先进入这个文件所在的路径，直接输入 $ uhd_fft能够显示出这个界面，就说明usrp安装成功了
 ![4](/images/usrp_s_4.png)
 上面的一些参数，我还是新手，也不太清楚（以后还是多多学习）
 #### 基于UHD的测试
 我们可以直接在终端中输入以下命令，即可打印出usrp的一些参数。
 ```Shell
 $ sudo uhd_find_device
 ```
 我们也可以输入以下命令,能够运行成功表明UHD和usrp安装成功了。
 ```Shell
 $sudo uhd_fft
 ```
 #### 总结
 第一次使用USRP时，先检查硬件配置是否设置成功，然后设置PC的IP地址，更新固件。
