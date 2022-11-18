<!--
 * @Author: Jerome 841682441@qq.com
 * @Date: 2022-11-17 22:28:56
 * @LastEditors: Jerome 841682441@qq.com
 * @LastEditTime: 2022-11-18 13:54:28
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

**脚本语言是为了缩短传统的编写-编译-链接-运行过程而创建的计算机编程语言，在很多方面，高级编程语言和脚本语言之间相互交叉，二者之间没有明确的界限。**
**一个脚本可以使得原本要用键盘进行的交互式操作自动化。一个Shell脚本主要由原本需要在命令行输入的命令组成，或者在一个文本编辑器中，用户可以使用脚本把常用的操作组合成一组序列。主要用来书写这种脚本的语言叫做脚本语言。**
**很多脚本语言实际上已经超过简单的用户命令序列的指令，还可以编写更复杂的程序。**
***

#### 3 Shell环境

Shell和JavaScript、PHP变成一样，只需要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以了。

    #！     这是一个标记符号，作用是告诉系统其后路径指定的
            程序就是解释次脚本文件的Shell程序。


#### 4 第一个Shell脚本

打开文本编辑器，用vi/vim命令来创建文件，新建一个文件/test.sh，/注意扩展名为.sh。

    #！/bin/bash
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

#### Shell变量
定义变量时，变量名不加美元符号($,在PHP语言中需要)

    your_name="runoob.com"

**注意：** 
(1)变量名和等号之间不能有空格。
(2)命名只能使用英文字母，数字或者下划线，首个字符不能以数字开头。
(3)不能使用标点符号。
(4)不能使用bash里的关键字。

除了显式地直接赋值，还可以用语句给变量赋值，如：

    for file in 'ls/etc`
    或
    for file in ${ls/etc}

以上语句将/etc下目录的文件名循环出来。

**使用变量**
使用一个定义过的变量，只需要在变量前加美元符号即可，如：

    your_name="zhangsan"
    echo $your_name
    echo ${your_name}

变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界，比如下面这种情况：

    for skill in Ada Coffee Action Java; do
        echo "I am good at ${skill}Script"
    done

如果不给skill变量加花括号，写成echo "I am good at $skillScipt",解释器就会把\$skillScript当成一个变量，其值为空，因此最好给每个变量都加上或括号，这是一个良好的编程习惯。

**只读变量**
使用readonly命令可以将命令变为只读变量，只读变量的值不能被改变。

    name="zhangsan"
    readonly name
    name="lisi" #执行此步骤程序会报错

**删除变量**
使用unset命令可以删除变量

    unset variable_name

变量被删除后不能再次使用。unset命令不能删除只读变量。

**变量类型**
运行shell时，会同时存在三种变量：
1)局部变量：在脚本或者命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
2)环境变量：所有程序包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要时shell脚本可以定义环境变量。
3)shell变量：shell变量是由shell程序设置的特殊变量。shell变量中一部分是环境变量，一部分是局部变量，这些变量保证了shell的正常运行。

**Shell字符串**
字符串是shell编程中最常用也最有用的数据类型，可以用单引号，双引号，也可以不使用引号。

**单引号**
单引号字符串的限制：
单字符串的任何字符都会原样输出，单引号字符串中的变量是无效的；
单引号字符串中不能出现单独一个的单引号(对单引号使用转义符后也不行)，但是可以成对出现，作为字符串拼接使用。

**双引号**
双引号的优点：
1)双引号里可以有变量
2)双引号里可以出现转义字符

**拼接字符串**

**获取字符串长度**

    string="abcd"
    echo ${#string}     #输出 4

**提取子字符串**

    string="runoob is a great site"
    echo ${string:1:4}  #输出unoo
注意：第一个字符的索引值为0。

**查找子字符串**
查找字符i或者o的位置(哪个字符先出现就计算哪个)：

    string="runoob is a great site"
    echo `expr index "$string" io`      # 输出 4

注意：以上脚本中`是反引号，而不是单引号'。

**Shell注释**

以\#开头的行就是注释，会被解释器忽略。
如果遇到大量代码需要临时注释起来，但每一行加\#太过费力，所以可以把这一段需要注释的代码使用一对花括号括起来，定义为一个函数，由于没有地方会调用这个函数，这块代码不会被执行。所以就达到了注释的作用。

#### Shell传递参数
我们可以在执行Shell脚本的时候，向脚本传递参数，脚本内获取参数的格式为：$n。其中n代表着一个数字，1位执行脚本的第一个参数，2位执行脚本的第二个参数，以此类推。


#### Shell流程控制
和Java、PHP等语言不一样，sh的流程控制不可为空。

**if else**
**fi**

if语句语法格式：

    if condition
    then
        command1
        command2
        ...
        commandN
    fi

写成一行(适用于终端命令提示符):

    if [$(ps -ef | grep -c "ssh") -gt ]; then echo "true"; fi

***
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
使用@或者\*可以获取数组中的所有元素。

    #!/bin/bash

    my_array[0]=A
    my_array[1]=B
    my_array[2]=C
    my_array[3]=D

    echo "数组的元素为：${my_array[*]}"
    echo "数组的元素为：${my_array[@]}"


    #!/bin/bash

    declare -A site
    site["google"]="www.google.com"
    site["taobao"]="www.taobao.com"
    site["runoob"]="www.runoob.com"

    echo "数组的元素为：${site[*]}"
    echo "数组的元素为：${site[@]}"

在数组前加上一个感叹号!可以获取数组的所有键。

    declare -A site
    site["google"]="www.google.com"
    site["taobao"]="www.taobao.com"
    site["runoob"]="www.runoob.com"

    echo "数组的键为：${!site[*]}"
    echo "数组的键为：${!site[@]}"

__获取数组的长度__
获取数组长度的方法与获取字符串长度的方法相同，实例如下：

    #!/bin/bash
    
    my_array[0]=A
    my_array[1]=B
    my_array[2]=C
    my_array[3]=D

    echo "数组元素个数为：${#my_array[@]}"
    echo "数组元素个数为：${#my_array[*]}"
    