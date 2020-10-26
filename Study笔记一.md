# CMakeLists.txt学习

首先在工程文件下下面新建几个文件

![image-20201026162245987](../../../../AppData/Roaming/Typora/typora-user-images/image-20201026162245987.png)



新建CMakeLists.txt文件

```
 1 cmake_minimum_required (VERSION 2.8)
  2 
  3 project (Demo1)
  4 
  5 add_executable(Demo1 main.cc MathFun.cc)
```

编译 cmake . 

make 

运行





**记录一下vim 的使用**

在home下新建文件设置vim风格    

vim .vimrc 

```
  1 set smarttab
  2 set tabstop=4
  3 set shiftwidth=4
  4 set expandtab
  5 set smartindent
  6 set guifont=Courier\ New\ 10
  7 set number
  8 colorscheme desert
  9 syntax on
 10 set cindent
```

![image-20201026162814470](../../../../AppData/Roaming/Typora/typora-user-images/image-20201026162814470.png)

常用 命令

```
i 插入

复制 y

粘贴 p

删除一行 dd

选中 v

撤销：u

恢复撤销：Ctrl + r

搜索 / 

：set nu    :显示行号
：set nonu  :取消行号


```

vim打开多个文件一起：

:vsp 文件名

让鼠标可以在几个屏幕间自由切换

:set mouce =a

调整两个屏幕差不大

:vertical res 数字   （增加列）

![image-20201026164015258](../../../../AppData/Roaming/Typora/typora-user-images/image-20201026164015258.png)