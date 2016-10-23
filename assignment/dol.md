## Lab2：DOL实例分析&编程

### 任务1：修改example2，让三个square模块变成2个，tips：修改xml的iterator
分析：该example中的square模块由迭代器控制。在xml文件的一开始，声明了一个变量N，值为3。后面在进行迭代时，迭代次数即由N控制，产生N + 1个channel、 共N个square模块。按照generator---square---...---square---consumer的顺序连接。故直接修改N值为2，即可以让square模块变为2个。

修改：

![img_01](https://raw.githubusercontent.com/XrLee/images/master/Lab2_01.JPG)

重新编译、运行：

	$ ant -f runexample.xml -Dnumber=2

运行结果如下：

![img_02](https://raw.githubusercontent.com/XrLee/images/master/Lab2_02.JPG)

修改后的Dot图：

![img_03](https://raw.githubusercontent.com/XrLee/images/master/Lab2_03.JPG)

修改完毕

### 任务2：修改 example1，使其输出3次方数，tips：修改square.c
分析：之所以会输出2次方数，是因为square.c模块在读取数据到i后，将其进行了一个平方的操作（i = i\*i，再将其传到一起相连的channel用于consumer输出。故想要输出三次方数，只需将i = i\*i改为i = i\*i\*i。

修改：

![img_04](https://raw.githubusercontent.com/XrLee/images/master/Lab2_04.jpg)

重新编译、运行（此处需要删除掉之前build后的example1文件夹）：

	$ ant -f runexample.xml -Dnumber=1
运行结果如下：

![img_05](https://raw.githubusercontent.com/XrLee/images/master/Lab2_05.JPG)

修改后的Dot图：

![img_06](https://raw.githubusercontent.com/XrLee/images/master/Lab2_06.JPG)

修改完毕

### 实验感想
本次实验，对DOL实例1和2的内容进行了分析，初步认识了DOL的代码内容以及由代码进行设计的过程。



