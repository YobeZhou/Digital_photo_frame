# 前言
本程序实现最终的功能是数码相册：
1. 支持触摸屏；
2. 可浏览文件系统内容（文本与图片）；
3. 可多媒体查看图片（手动播放、自动连续播放、缩小、放大）；
4. 支持多种编码格式。

本程序的Makefile分为3类:
1. 顶层目录的Makefile
2. 顶层目录的Makefile.build
3. 各级子目录的Makefile

# 一、各级子目录的 Makefile
   它最简单，形式如下：
obj-y += file.o
obj-y += subdir/
   
   "obj-y += file.o"表示把当前目录下的file.c编进程序里，
   "obj-y += subdir/"表示要进入subdir这个子目录下去寻找文件来编进程序里，是哪些文件由subdir目录下的Makefile决定。

注意: "subdir/"中的斜杠"/"不可省略

# 二、顶层目录的 Makefile
   它除了定义obj-y来指定根目录下要编进程序去的文件、子目录外，主要是定义工具链、编译参数、链接参数──就是文件中用export导出的各变量。

# 三、顶层目录的 Makefile.build
   这是最复杂的部分，它的功能就是把某个目录及它的所有子目录中、需要编进程序去的文件都编译出来，打包为built-in.o

# 四、使用这个 Makefile 示例
1. 把顶层Makefile, Makefile.build放入程序的顶层目录
2. 修改顶层Makefile
   1. 修改工具链
   2. 修改编译选项、链接选项
   3. 修改obj-y决定顶层目录下哪些文件、哪些子目录被编进程序
   4. 修改TARGET，这是用来指定编译出来的程序的名字

3. 在各一个子目录下都建一个Makefile，形式为：
``` makefile
   obj-y += file1.o
   obj-y += file2.o
   obj-y += subdir1/
   obj-y += subdir2/
```

4. 执行"make"来编译，执行"make clean"来清除，执行"make distclean"来彻底清除
   
