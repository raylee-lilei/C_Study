## CMakeLists.txt学习

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



## 知识点

为防止出现整形溢出行为 要注意有符号和无符号的使用      带有负数的使用有符号的，没有符号的尽量使用无符号，这样可以保证变量可以表示更大的值

-32768——+32767   表示一个周期上溢和下溢，如果定义 的值为 最大值32767的时候，对他进行加一 的时候会变成-32768



### 指针：

#### 指针含义

指针就是一个特殊的变量，里面 存储的是地址



**指针的类型**                                                          把指针声明语句里的指针名字去掉，剩下的部分就是这个指针的类型

**指针所指向的类型 **                                             把指针声明语句中的指针名字和名字左边的指针声明符\*去掉，剩下的就是指针所指向的类型。

**指针的值或者指针所指向的内存区 **                  一个指针的值是 XX，就相当于说该指针指向了以 XX 为首地址的一片内存区域。该指针的值是这块内存区域的首地址

**指针本身所占有的内存区 **                                  32 位平台里，指针本身占据了 4 个字节的长度



|                 | **指针的类型** | **指针所指向的类型** | **指针所指向的内存区** | **指针本身所占有的内存区** |
| --------------- | :------------- | -------------------- | ---------------------- | -------------------------- |
| int\*ptr        | int *          | int                  |                        |                            |
| char\*ptr       | char *         | char                 |                        |                            |
| int\**ptr       | int **         | int *                |                        |                            |
| int(\*ptr)[3]   | int (*)[3]     | int ()[3]            |                        |                            |
| int\*(\*ptr)[4] | int * (*) [4]  | int* ()[4]           |                        |                            |



#### 类型说明

从变量名开始看，根据优先级分析

int  *p              从p开始，与  *  一起，表示是一个指针，指向内容为int ，返回整形数据的指针

int p[3]             从p开始，与  [] 一起，表示是一个数组，数组内容为int ，返回整形数据的数组

[]优先级高于  *

int *p[3]           从p开始，与  [] 一起，表示是一个数组，然后与 *  结合   表示数组里面的元素是指针 ，再与int结合，指向的内容是int ，返回由整形数据的指针组成的数组 

int （*）p[3]    从p开始,与 *  结合，表示是一个指针，然后与 [] 结合，指针指向的内容是数组，然后与int 结合，说明数组的元素是int ,返回指向由int型组成数组的指针

int  ** p             从p开始，与 * 结合，表示是一个指针，然后与 * 结合，指针指向的内容是指针，然后与int 结合，说明该指针指向 的元素是int ,返回指向int 的二级指针



int  p（int）      从p开始，与 ()结合，表示是一个函数，然后进入括号，该函数带有一个int 型的参数，再与 int 结合，表示返回值是int

int (*p)(int)        从p开始，与  * 结合，表示是一个指针，然后与（）结合，指向带有int 型参数的函数，函数返回int 。p 是指向有int型参数的函数且返回类型为int 的函数的指针



#### 指针的算术运算



```C++
char a[20];

int *ptr=(int *)a; //强制类型转换并不会改变 a 的类型

ptr++;
```



指针ptr +1  ,把指针 ptr 的值加上了 sizeof(int)，在 32 位程序中，是被加上了 4，，int 占 4 个字节。 ptr 所指向的地址由原来的变量 a 的地址向高地址方向增加了 4 个字节



```C++
char a[20]="You_are_a_girl";

int *ptr=(int *)a;

ptr+=5;
```



将指针 ptr 的值加上 5 乘 sizeof(int), ptr 所指向的地址比起加 5 后的 ptr 所指向的地址来说，向高地址方向移动了 20 个字节

**一个指针 ptrold 加(减)一个整数 n 后，结果是一个新的指针 ptrnew，ptrnew 所指向的内存区将比 ptrold 所指向的内存区向高(低)地址方向移动了 n 乘sizeof(ptrold 所指向的类型)个字节**



```C++
char  str[] = "hello"  sizeof(str)  = 6;        strlen(str)  = 5 字符串的长度

char str[100]   sizeof(str)  = 100;

char str[5] = {'h','e','l','l','o'};          sizeof(str) = 5

char *p = "hello";       sizeof(p) = 4    一个指针

char *p[] = {"hello","world"};      sizeof(p) = 8  长度为2的字符串数组

int arr[100] = {0}     int  arr[100];       sizeof(arr) = 100*4
```





**&a 的运算结果是一个指针，指针的类型是 a 的类型加个\*，指针所指向的类型是 a 的类型，指针所指向的地址嘛，那就是 a 的地址。**

**int a=12**

&a  是一个指针，指针的类型是int  *   指向的类型是int  指向的地址就是a 的地址



#### 指针表达式

**一个表达式的结果如果是一个指针，那么这个表达式就叫指针表式**

```
int a,b;

int array[10];

int *pa;

pa=&a;    //&a 是一个指针表达式。 &a 不是一个左值，因为它还没有占据明确的内存

Int ptr=&pa;    //&pa 也是一个指针表达式。

*ptr=&b; // *ptr 和&b 都是指针表达式   *ptr 是 一个左值，因为*ptr 这个指针已经占据了内存

pa=array;

pa++;//这也是指针表达式。
```

**当一个指针表达式的结果指针已经明确地具有了指针自身占据的内存的话，这个指针表达式就是一个左值，否则就不是一个左值。**



char *str[3] = {"Hello,lilei","Hello,raylee","Hello,tingwa"}

| Hello,lilei | Hello,raylee   | Hello,tingwa |
| :---------: | -------------- | ------------ |
|   指针str   | str+1          | str+2        |
|             | *(str+1),指向H |              |





str 是指针指向数组的第0号元素，指针的类型是  char **    指向的类型是char * 

*str也是指针。指针的类型是char *   指向是char   ,指向的地址是Hello,lilei的第一个字符的位置，即H的位置

字符串相当于是一个数组,在内存中以数组的形式储存,只不过字符串是一个数组常量,内容不可改变,且只能是右值.如果看成指针的话,他即是常量指针,也是指针常量.



#### **指针和结构类型**

```
struct MyStruct

{

int a;

int b;

int c;

};

struct MyStruct ss={20,30,40};//声明了结构对象 ss，并把 ss 的成员初始化为 20，30 和 40。

struct MyStruct *ptr=&ss;//声明了一个指向结构对象 ss 的指针。它的类型是MyStruct*,它指向的类型是 MyStruct。

int *pstr=(int*)&ss;
```

ptr->a;

ptr->b;

ptr->c;



**各个数组单元存放在连续的存储区里，单元和单元之间没有空隙。但在存放结构对象的各个成员时，在某种编译环境下，可能会需要字节对齐，需要在相邻两个成员之间加若干个"填充字节"，这就导致各个成员之间可能会有若干个字节的空隙**

于是使用pstr的时候不能像数组那样通过移动指针的方式去取成员     * pstr； * (pstr+1);  *(pstr+2) 



#### **指针和函数**

**可以把一个指针声明成为一个指向函数的指针**

int  fun(char * ,int);

int (* Pfun) (char * ,int)

Pfun = fun;

int a = (*Pfun) ("sdsdsds",7);



#### 类型转化

float a  = 2.34;

int *p;

p = (int *)&a;

**这样强制类型转换的结果是一个新指针**,**原来的指针 p 的一切属性都没有被修改**



如果我们想要把一个整数赋给指针的值

```C++
unsigned int a ;

char* ptr;

a = N ; // 必须是一个合法的地址

ptr = (char *)a ;


```

```C++
int a=123,b;

int *ptr=&a;

char *str;

b=(int)ptr; //把指针 ptr 的值当作一个整数取出来。

str=(char*)b; //把这个整数的值当作一个地址赋给指针 str。 
```





#### **指针的安全问题**



```C++
char s='a';

int *ptr;

ptr=(int *)&s;

*ptr=1298；
```

ptr 指向s 的首地址，在32位中，  char 占一个字节，int  占4个字节，最后一条语句不但改变了 s 所占的一个字节，还把和 s 相临的高地址方向的三个字节也改变了

```C++
char a;

int *ptr=&a;

ptr++;

*ptr=115;
```

**在指针的强制类型转换：ptr1=(TYPE \*)ptr2 中，如果** **sizeof(ptr2的类型)大于 sizeof(ptr1 的类型)，那么在使用指针 ptr1 来访问 ptr2所 指 向 的 存 储 区时 是 安 全 的 。**

