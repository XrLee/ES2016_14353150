## This is my README.md##
# DOL#

## Description##

> The distributed operation layer ([DOL](http://www.tik.ee.ethz.ch/~shapes/dol.html)) is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.

## How to install##

首先介绍几个工具吧

[make工具简介](http://blog.chinaunix.net/uid-9314244-id-2004686.html)

- 在Linux和Ubuntu环境中，make工具主要被用来进行工程编译和程序链接
- Makefile文件：告诉make以何种方式编译源代码和链接程序
- make通过比较对应文件（规则的目标和依赖）的最后修改时间，来决定哪些文件需要更新、那些文件不需要更新。

[Ant工具简介](http://blog.163.com/qiangyongbin2000@126/blog/static/77517819201151653423687)

- Ant是一种基于Java的build工具。
- Ant用Java的类来扩展。
- Ant本身就是这样一个流程脚本引擎，用于自动化调用程序完成项目的编译，打包，测试等。

此处顺便再提一下Ant的优点：

- 跨平台性。Ant是纯java语言编写的，所示具有很好的跨平台性。
- 操作简单。Ant是由一个内置任务和可选任务组成的。Ant运行时需要一个XML文件(构建文件)。
- 容易维护和书写，结构清晰。
Ant可以集成到开发环境中。

java与javac简介

- 用途：编译或执行java代码
- javac命令用来编译java文件
- java命令可以执行生成的class文件

接下来就开始安装了

1. 安装在linux环境下，建议使用虚拟机安装Ubuntu（[Ubuntu下载](http://www.ubuntu.com/download/desktop)）
我选择的虚拟机管理软件为VMware（[VMware教程](http://jingyan.baidu.com/article/0320e2c1ef9f6c1b87507bf6.html)），你也可以使用VirtualBox（[VirtualBox教程](http://jingyan.baidu.com/article/cdddd41c5eea3153ca00e160.html)）

2. 安装一些必要的环境
	
		$ sudo apt-get update

		$ sudo apt-get install ant

		$ sudo apt-get install openjdk-7-jdk

		$ sudo apt-get install unzip

3. 下载文件（使用Vmware虚拟机，也可以从主机拷贝到虚拟机中去（[教程](http://jingyan.baidu.com/article/c33e3f48a5c153ea15cbb5b2.html)），这里涉及到VMware Tools的安装，再补充一个Linux环境下的[教程](http://jingyan.baidu.com/album/c14654139e9ca10bfcfc4c8f.html?picindex=3)）：
	
		sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz

		sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip

4. 解压文件
	
	* 新建dol的文件夹 
		
			$ mkdir dol
	
	* 将dolethz.zip解压到 dol文件夹中
	
			$ unzip dol_ethz.zip -d dol

	* 解压systemc

			$ tar -zxvf systemc-2.3.1.tgz

5. 编译systemc

	* 解压后进入systemc-2.3.1的目录下
	
			$ cd systemc-2.3.1

	* 新建一个临时文件夹objdir

			$ mkdir objdir

	* 进入该文件夹objdir

			$ cd objdir

	* 运行configure(能根据系统的环境设置一下参数，用于编译)

			$ ../configure CXX=g++ --disable-async-updates

		运行configure之后的截图：

		![dol_img_1](https://github.com/XrLee/images/blob/master/1.JPG?raw=true)

	* 编译
	
			$ sudo make install

	* 编译完后文件目录如下(`$ cd ..` `$ ls`):
		
		![dol_img_2](https://github.com/XrLee/images/blob/master/2.JPG?raw=true)
	
		能看到include, lib-linux(对于64位系统，这里是lib-linux64)

	* 记录当前的工作路径(会输出当前所在路径，记下来，待会有用)

			$ pwd

		![dol_img_3](https://github.com/XrLee/images/blob/master/3.JPG?raw=true)

	* 这里表示我当前的工作路径为：

		/home/lxr/systemc-2.3.1

6. 编译dol

	* 进入刚刚dol的文件夹

			$ cd ../dol
	
	* 修改build_zip.xml文件
	
			$ sudo gedit build_zip.xml

	* 找到下面这段话，就是说上面编译的systemc位置在哪里，

			<property name="systemc.inc" value="YYY/include"/>         

			<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>   
 
		把YYY改成上页pwd的结果（注意，对于64位系统的机器，lib-linux要改成lib-linux64）

	* 然后是编译

			$ ant -f build_zip.xml all
	
	* 若成功会显示build successful

	* 接着可以试试运行第一个例子
	
		进入build/bin/mian路径下

			$ cd build/bin/main

		然后运行第一个例子

			$ ant -f runexample.xml -Dnumber=1

		成功结果如图:
		
		![dol_img_4](https://github.com/XrLee/images/blob/master/4.JPG?raw=true)

## 至此安装完毕

## Experimental experience

本次实验，了解了git版本控制并学习了其使用；另外，学习了markdown的符号，markdown用于编写文本，其目的是让书写者的主要精力放在书写内容上而不是排版。整过自学过程让我明白了：不懂就百度，结合网上的教程可以学到很多知识。