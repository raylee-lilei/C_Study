## C++ 中的c_str()用法

c_str函数原型

```C++
const char* c_str();
```

====================================================
**函数作用**

​	把string对象转化成c中的字符串样式（C 中没有string 类型）

====================================================

**c_str() 返回的是一个临时指针。不能直接进行操作**

====================================================

```C++
const char* str = "lilei"   lilei 是字符串常量
char *str = "lilei"   和上面一样，不能通过 str去修改

char str[]  //数组  \0   长度+1   可以修改
char str[n] //长度 n

char* str = new char[100]
```

结构体中

```C++
struct Person {
	int age;
	char ID[10];
	string name;
	char sex;
};

//动态创建结构体

Person* P = new Person;
P->age = 18;
//不能通过  P->ID  去修改或者初始化 因为ID 是const  可以通过下面的方式去初始化
strcpy_s(P->ID, "lilei");
P->sex = 'a';

cout << P->age <<" "<< P->ID << " "<< P->name << " " << P->sex << endl;

delete P;
P = NULL;

/*Person* P1 = new Person[10];
Person** P2 = new Person*;
Person** P2 = new Person * [10];*/
```

===========================================================
变量只允许定义一次，但可以在多个文件中声明。
声明，编译器只知道有这么个东西，具体怎么定义的要编译器去找
定义时才分配内存
只有当extern声明位于函数外部时，才可以初始化

使用extern 这个函数可能在其他的源文件中使用

===========================================================



