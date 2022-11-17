<!--
 * @Author: Jerome 841682441@qq.com
 * @Date: 2022-11-17 22:28:56
 * @LastEditors: Jerome 841682441@qq.com
 * @LastEditTime: 2022-11-17 23:54:59
 * @FilePath: \自学知识\shell脚本语言.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
### Shell教程

Shell是一个用C语言编写的程序，它是用户使用Linux的桥梁，Shell既是一种命令语言，又是一种程序设计语言。
Shell是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。

shell是一个命令行解释器，是linux内核的一个外壳,负责外界与linux内核的交互。shell是包裹在操作系统外层的一道程序，就好像是操作系统的壳，shell（壳）的名称也由此而来。shell接收用户或者其他应用程序的命令, 然后将这些命令转化成内核能理解的语言并传给内核, 内核执行命令完成后将结果返回给用户或者应用程序。当你打开一个terminal(终端)时，操作系统会将terminal和shell关联起来，当我们在terminal中输入命令后，shell就负责解释命令。

shell广义上可以指操作系统和用户接口的界面，图形界面也是一种shell。因为图形界面的本质也是实现“把人类用户的操作意图转述个内核”。

终端上所有命令都需要一个东西翻译解析一下，计算机才能理解并执行。这个翻译解析的东西叫SHELL解释器，RedHat和CentOS默认SHELL解释器叫：bash。

***

#### 1 Shell脚本

Shell脚本(shell script)是一种为Shell编写的脚本程序。
虽然经常说的shell通常指的是shell脚本，但是shell和shell scipt并不是一个概念。

#### 2 终端和shell的关系

我们在使用Linux的时候经常会遇到终端和Shell的概念，在Ubuntu上通过点击鼠标，点击"Open Terminal"可以打开一个终端。此时就可以在终端中输入Linux命令。

##### 2.1 终端

终端(Computer terminal)，是与计算机系统相连的一种输入输出设备。通俗来说，终端其实就是人与机器交互的接口
。
人和机器是两个相互独立的实体。当人使用机器时，必须借助某种接口(interface)才能与机器交流信息。台式机的接口包括显示器、键盘、鼠标、扬声器、麦克风等。CPU、内存、硬盘、光驱、显卡、网卡等其他硬件属于主机(host)。Unix和Linux把这种使得人和机器可以交互的接口称为终端。

终端具有两个基本功能：向主机输入信息和向外部输出信息。所以终端可以分为输入设备和输出设备。台式机的输入设备通常包括键盘、鼠标、麦克风，输出设备包括显示器、扬声器等。

linux上面终端（terminal）（就是你输入指令的那个黑色框框）就是一个仿真终端，你可以把它当作一个模拟的输入设备。作用是提供一个命令的输入输出环境，在linux下使用组合键ctrl+alt+T打开的就是终端（ctrl+D可以关闭终端）。

##### 2.2 Shell与终端的关系

Shell是一个程序，一个二进制可运行可执行的程序。
两者之间区别：终端本身并不会负责解析命令，它只是一个界面，负责人机交互的一个接口而已，真正处理命令的是shell。终端只负责提供一个输入命令的交互界面而已，在里面运行的命令是专门的命令执行程序shell来完成的。

终端的主要作用是接受用户输入命令和字符，探后提交给shell，并且将命令执行完的结果反馈给用户。shell负责将命令翻译，在系统执行完之后将结果返回给终端。
shell和终端的关系就是shell是一个程序，一个二进制可运行可执行的程序，终端命令执行时会自动调用shell程序，每次打开终端的时候，终端程序都会调用shell。终端调用shell程序成功后，终端就会显示如下的信息：

    [root@localhost ~] #

其中root代表的是用户名，host指的是登录到的主机，~表示当前目录，$表示的是命令提示符(如果登录用户是root就显示为#)，表示等待输入命令。

#### 3 Shell环境

Shell和JavaScript、PHP变成一样，只需要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以了。

    #！     这是一个标记符号，作用是告诉系统其后路径指定的
            程序就是解释次脚本文件的Shell程序。


#### 4 第一个Shell脚本

打开文本编辑器，用vi/vim命令来创建文件，新建一个文件/test.sh，/注意扩展名为.sh。

    #！bin/bash
    echo "Hello World!"

___#!是约定标记，他告诉系统该脚本需要使用什么解释器来执行，也即使用哪一种Shell。___

echo命令用于向窗口输出文本。

**运行脚本有两种办法：**
1.作为可执行程序
/将上述代码保存为test.sh，并cd到相应目录

    chmod 777 ./test.sh
    ./test.sh

2.作为解释器参数

    /bin/bash test.sh
    /bin/php test.php


#### Shell数组

数组中可以存放多个值。Bash Shell只支持一维数组。初始化时不需要定义数组大小(与PHP类似)。
与大多数编程语言类似，数组元素的下表由0开始。
Shell数组用括号来表示，元素用“空格”符号分隔开，语法格式如下：

    array_name=(value1 value2 value3 ... valuen)

实例1：

    #!bin.bash
    
    my_array=(A B "C" D)

我们也可以使用下标来定义数组：

    array_name[0]=value0
    array_name[1]=value1
    array_name[2]=value2

读取数组
读取数组元素值的一般格式是：

    ${array_name[index]}

##### 关键数组

Bash支持关联数组，可以使用任意的字符串、或者整数作为下表来访问数组元素。
关联数组使用declare命令来声明，语法格式如下：

    declare -A array_name

-A选项就是用于声明一个关联数组。
关联数组的键是唯一的。

    declare -A site=(["google"]="www.google.com" ["runoob"]="www.runoob.com" ["taobao"]="www.taobao.com")

    declare -A site
    site["google"]="www.google.com" 
    site["runoob"]="www.runoob.com" 
    site["taobao"]="www.taobao.com"

访问关联数组元素可以使用指定的键，格式如下：

    array_name["index"]

##### 获取数组中的所有元素
