#### GNU Radio 是什么它有什么用途？
GNU Radio 是免费开源的软件开发工具套件。它提供构建软件无线电所需的信号运行和处理的模块，用它可以在唾手可得的低成本的外部射频（RF）硬件和通用微处理器上、或无硬件的模拟环境中实现软件定义无线电。这套套件广泛用于业余爱好者，学术机构和商业机构用来研究和构建无线通信系统。
#### 什么是软件无线电？
维基百科（Wikipedia page）对此给予了一个满意的答案。一句话，软件无线电是将所有的信号处理的工作交由软件来处理，而非传统方法那样由专职硬件承担。这样做的明显优点是软件构建的部件在系统中很容易被替换，同一（软件）部件可被用以构建众多无线系统，也可被用在各种传输标准中；也就是说，一套软件无线电系统可用于各种不同的应用中！
#### GNU Radio 到底能干什么？
GNU Radio 可以进行各类信号处理。可以使用它编写应用程序从数据流中获取数据或将数据传输到数据流中，然后使用硬件将其发射出去。GNU Radio 具有滤波器、通道编码、同步单元、均衡单元（equalizer）、解调器、声音合成机（vocoder）、解码器（decoder）、等很多单元（使用 GNU Radio 术语，这些被称作功能块 - blocks),这些单元也都是无线电系统中的常见部件单元。更重要的是，它还具有连接这些功能模块的方法及管理在这些功能块间传输数据的策略。对 GNU Radio 进行扩充也十分容易；如若发现所缺失的特定功能块，便可快速生成并将其添加到系统中。

源于 GNU Radio 

Since GNU Radio is software, it can only handle digital data. Usually, complex baseband samples are the input data type for receivers and the output data type for transmitters. Analog hardware is then used to shift the signal to the desired centre frequency. That requirement aside, any data type can be passed from one block to another - be it bits, bytes, vectors, bursts or more complex data types.

GNU Radio 的应用主要是用 Python 编程语言来编写的。但是其核心信号处理模块是 C++ 在带浮点运算的微处理器上构建的。因此，开发者能够简单快速的构建一个实时、高容量的无线通信系统。
#### 必须通过编程来使用 GUN Radio 吗?
这无疑是最佳途径。尽管如此，无需编程也还是能做些事情的。首先，它提供 [GNU Radio Companion](http://gnuradio.microembedded.com/gnuradiocompanion)，一个同 Simulink 相似的图形化用户界面。通过对图形的简单的拖和拉便可生成各种信号处理应用程序。其次，GNU Radio 自带一组现成的[工具及功能程序](https://wiki.gnuradio.org/index.php/Main_Page#Using-the-included-tools-and-utility-programs)（[tools and utility programs](https://wiki.gnuradio.org/index.php/Main_Page#Using-the-included-tools-and-utility-programs)）。这些工具可以担当大多数基本操作，比如记录射频信号并对其进行频谱分析。对此充满幻想，不妨阅读一下 [如何着手 GNU Radio](http://gnuradio.microembedded.com/howtouse)?

但是无论如何，如若想要扩展 GUN Radio（比如，添加新的功能），编写代码便是不可避免的工作。构建比较精巧复杂的应用时 GUN Radio Companion 便很难胜任，Python 便是首当其冲的选择。关联性能优劣的代码自然是 C++ 的角色。
#### GNU Radio 的版权执照?
GNU Radio 遵从 GNU GPL V3.0. 所有,其代码归 FSF - Free Software Foundation （自由软件基金）所有。
#### 人们使用 GNU Radio 都做了些什么?
在安装成功 GNU Radio 之后，系统便自带很多例程。诸如，数字化传输数据，接收模拟信号等等的工具。有人将历程发布到第三方项目库管理系统比如 CGRAN 上。也有人将其发布到[项目列表](http://gnuradio.microembedded.com/othercode)（list of projects）上。
#### 数字信号处理、基带、同步 ... 这些概念的涵义是什么？
满脑都是这些问题，可以肯定在使用 GNU Radio 的过程中遇到了诸多困难。具备很多信号处理的理论知识是能够编写信号处理及无线通信的软件的前提。尽管如此还是那句老话，不要被困难所弃累！抓本书开始阅读，写一些代码看看会发生什么事情。在此一个小小的建议：在没有完全理解诸如复合基带（complex baseband）之类的概念之前不要求助邮件列表 :-)。

### 欢迎来到 GNU Radio 社区
#### 序言
GNU Radio 是免费开源的软件开发工具套件。它提供信号运行和处理的模块，用它可以在唾手可得的低成本的外部射频（RF）硬件和通用微处理器上实现软件定义无线电、或无硬件的模拟环境。这套套件广泛用于业余爱好者，学术机构和商业机构用来研究和构建无线通信系统。

GNU Radio 的应用主要是用 Python 编程语言来编写的。但是其核心信号处理模块是 C++ 在带浮点运算的微处理器上构建的。因此，开发者能够简单快速的构建一个实时、高容量的无线通信系统。

尽管其主要功用不是用来做仿真器，GNU Radio 在没有射频 RF 硬件部件的境况下还可用作对预先存储或（信号发生器）生成的数据进行信号处理的算法研究的平台。

GNU Radio 遵从 GNU GPL V3.0. 所有，其代码归 FSF - Free Software Foundation （自由软件基金）所有。
#### 着手
以前从未接触过 GNU Radio，下面这些页面将帮助如何运行安装 GNU Radio、及展示如何着手这个软件无线电工具的第一步。
* [GNU Radio 是什么、为何需要它？](http://gnuradio.microembedded.com/whatisgr) - 读读这篇文章，如果对 GNU Radio 项目一无所知。 
* [安装指导](http://gnuradio.microembedded.com/installinggr) - 这篇文件阐述安装 GNU Radio 所涉及的所有。
    * [下载专区](http://gnuradio.microembedded.com/download) - 径直获取源代码。
    * [创建指导](http://gnuradio.microembedded.com/buildguide) - 适于专家（高手）：如何基于源码构建 GNU Radio。
* [GNU Radio 常见问题](http://gnuradio.microembedded.com/faq) - 认真地读读这个。在提出任何问题之前请先认真地、好好地读读这篇文章。

#### 文档
两本 GNU Radio 手册：一本是 C++ API 另一本是 Python API 。文档的大部分内容来自于使用 Doxygen 对公共头文件的注释的标记。这些（来自于头文件的注释的标记）内容是构成这两本手册的基础。Python 文档通过 [Sphinx](http://www.sphinx-doc.org/en/master/) 提取 Doxygen 的文档及 Python 文档中规范化的注解的内容。
* [C++ Manual](https://www.gnuradio.org/doc/doxygen/index.html) - 内容包含所有的模块。
    * [老旧文档](https://wiki.gnuradio.org/index.php/Main_Page)
* [Python Manual](https://www.gnuradio.org/doc/sphinx/index.html) - 内容包含所有的模块。
    * [老旧文档](https://wiki.gnuradio.org/index.php/Main_Page)
#### 社区及交流
这是一个供大家介入 GNU Radio 的友善社区。下面几点促使大家相互联系。
* [提问及报告错误](http://gnuradio.microembedded.com/reportingerrors) - 帮助大家是我们的宗旨，但希望大家能试图自己帮助自己。
* [邮件列表](http://gnuradio.microembedded.com/mailinglists)- 这是大家的核心交流区，介入之前提请阅读上篇（的注意事项）。
* [如何染指](http://gnuradio.microembedded.com/howtogetinvolved) - 想搭手项目事宜，或简单地想成为社区的一部分？敬请阅读！
* [IRC 聊天室](http://gnuradio.microembedded.com/irc) - 一个更实时的交互交流区，欢迎大家在 Freenode 使用 #gnuradio 加入我们的聊天室。
* [其它 GNU Radio 社区](http://gnuradio.microembedded.com/morecommunity) -  更多形式的 GNU Radio 的网络社区及其它
* [开发者在线](http://gnuradio.microembedded.com/developerscalls) - 对大家开放的开发者的每月 VoIP 交流会议。
* [GNU Radio 交流大会](http://gnuradio.microembedded.com/gnuradioconference)
    * [GRCon2012](http://www.trondeau.com/gnu-radio-conference-2012/)
    * [GNU Radio Conference 2011](http://www.trondeau.com/gnu-radio-conference-2011/), a real-life developers and enthusiast meeting
#### 开发 GNU Radio 
使用 GNU Radio 是让人感到很有趣的事情，但是真正的爱好者来自于对 GNU Radio 新的部件的开发或现实地在改进其源代码。如果想染指这些，那请先读读下面的文章。
* [社区贡献](http://gnuradio.microembedded.com/development)
* [GNU Radio 代码规范指导](http://gnuradio.microembedded.com/coding_guide_impl)（Coding and style guidelines for GNU Radio）
* [模块构架指导](http://gnuradio.microembedded.com/blockscodingguide)（Block structure guide）
* [如何编写 GNU Radio 信号处理功能块 - How to Write a GNU Radio Signal Processing Block](http://gnuradio.microembedded.com/howto-write-a-bloc)
* [如何对 GNU Radio 进行 Octave 分析 - How to use Octave or Matlab with GNU Radio](http://gnuradio.microembedded.com/octave)
* [不同版本的 API 及源代码之间的区别](http://gnuradio.microembedded.com/changesets)
* [如何用 Git 跟踪你自己的代码](http://gnuradio.microembedded.com/developingwithgit)
* YouTube feed from Ettus Research [featuring demos and howtos](https://www.youtube.com/user/ettusresearch/feed) for using GNU Radio and USRPs.
#### 关联硬件
硬件并非 GNU Radio 的必须部分，它（GNU Radio)其实就是一个纯粹的软件库。尽管如此，在一个能够进行实际的接收和发射信号的硬件平台上开发无线及信号处理的代码的工作不是令人更感到有趣吗？GNU Radio 支持好几种软件无线电平台。

最常用的便是 [通用软件无线电平台 USRP](http://www.microembedded.cn/) 。
* [关联硬件](http://gnuradio.microembedded.com/hardware) - 可运行 GNU Radio 的所有类型的硬件的预览。
    * [UHD 中文维客](http://kb.microembedded.com/uhdwikistart)
* [USRP1](http://gnuradio.microembedded.com/usrp)
* [USRP2 介绍](http://gnuradio.microembedded.com/usrp2)
* [子板清单](http://gnuradio.microembedded.com/list_of_usrp_daughterboards)
#### 更多资讯及第三方延伸
网络上可以发现更多。在下面可以找到讲义、代码及其它。
* GNU Radio 全面的文档网络 - 第三方的 GNU Radio 应用及扩展。
* [建议读物](http://gnuradio.microembedded.com/suggestedreading) - 一组非 GNU Radio 读物诸如：信号处理、无线工程和软件开发的引导读物。
* [其它服务器上的 GNU Radio 代码](http://gnuradio.microembedded.com/othercode)
* [第三方贡献的文档及例程](http://gnuradio.microembedded.com/externaldocumentation)
* [用户群](http://gnuradio.microembedded.com/ourusers)
* [涉及 GNU Radio 的学术文章](http://gnuradio.microembedded.com/academicpapers)
* [国内外商业性的支持及培训机构](http://gnuradio.microembedded.com/support)
* [展示](http://gnuradio.microembedded.com/presentations)
* [开源基站](http://openbts.microembedded.com/wikistart) - 一个开源 GSM 接口。这是一个独立的项目有其自己的邮件列表。
* [预录信号源](http://gnuradio.microembedded.com/sampledata) - 如若没有 USRP，可以使用预录信号进行离线分析。
#### 新闻
更多的新闻、以及官方的 GNU Radio 的博客请到：[can be found here](http://gnuradio.squarespace.com/).

###### source: http://gnuradio.microembedded.com/  注：Welcome to GNU Radio!（原文出处，翻译整理仅供参考!）

###### source: http://gnuradio.microembedded.com/whatisgr
