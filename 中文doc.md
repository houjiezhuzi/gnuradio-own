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
这无疑是最佳途径。尽管如此，无需编程也还是能做些事情的。首先，它提供 GNU Radio Companion，一个同 Simulink 相似的图形化用户界面。通过对图形的简单的拖和拉便可生成各种信号处理应用程序。其次，GNU Radio 自带一组现成的工具及功能程序（tools and utility programs）。这些工具可以担当大多数基本操作，比如记录射频信号并对其进行频谱分析。对此充满幻想，不妨阅读一下 如何着手 GNU Radio?

但是无论如何，如若想要扩展 GUN Radio（比如，添加新的功能），编写代码便是不可避免的工作。构建比较精巧复杂的应用时 GUN Radio Companion 便很难胜任，Python 便是首当其冲的选择。关联性能优劣的代码自然是 C++ 的角色。
#### GNU Radio 的版权执照?
GNU Radio 遵从 GNU GPL V3.0. 所有,其代码归 FSF - Free Software Foundation （自由软件基金）所有。
#### 人们使用 GNU Radio 都做了些什么?
在安装成功 GNU Radio 之后，系统便自带很多例程。诸如，数字化传输数据，接收模拟信号等等的工具。有人将历程发布到第三方项目库管理系统比如 CGRAN 上。也有人将其发布到项目列表（list of projects）上。
#### 数字信号处理、基带、同步 ... 这些概念的涵义是什么？
满脑都是这些问题，可以肯定在使用 GNU Radio 的过程中遇到了诸多困难。具备很多信号处理的理论知识是能够编写信号处理及无线通信的软件的前提。尽管如此还是那句老话，不要被困难所弃累！抓本书开始阅读，写一些代码看看会发生什么事情。在此一个小小的建议：在没有完全理解诸如复合基带（complex baseband）之类的概念之前不要求助邮件列表 :-)。
