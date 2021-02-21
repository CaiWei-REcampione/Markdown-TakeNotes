# 目录

[toc]

# 参数声明

```c++
<typename> int;
typename* name=new <typename>;
```

|    c++基本类型     |
| :----------------: |
|   unsigned char    |
|    signed char     |
|        char        |
|       short        |
|   unsigned short   |
|        int         |
|    unsigned int    |
|        long        |
|   unsigned long    |
|     long long      |
| unsigned long long |
|       float        |
|       double       |
|    long double     |



## 字符串

*    C风格字符串

```c++
char site[]="...";
char site[7]={'R','U,'N','O','O','B','\0'};
```

|        函数         | 目的                                                         |
| :-----------------: | :----------------------------------------------------------- |
| **strcpy(s1, s2);** | 复制字符串 s2 到字符串 s1。                                  |
| **strcat(s1, s2);** | 连接字符串 s2 到字符串 s1 的末尾。连接字符串也可以用 **+** 号，例如: `string str1 = "runoob"; string str2 = "google"; string str = str1 + str2;` |
|   **strlen(s1);**   | 返回字符串 s1 的长度。                                       |
| **strcmp(s1, s2);** | 如果 s1 和 s2 是相同的，则返回 0；如果 s1<s2 则返回值小于 0；如果 s1>s2 则返回值大于 0。 |
| **strchr(s1, ch);** | 返回一个指针，指向字符串 s1 中字符 ch 的第一次出现的位置。   |
| **strstr(s1, s2);** | 返回一个指针，指向字符串 s1 中字符串 s2 的第一次出现的位置。 |

## C++ string类

```c++
#include <iostream>
using namespace std;
string string-name;
```

### substr函数

原型：string substr ( size_t pos = 0, size_t n = npos ) const;
功能：获得子字符串。
参数说明：pos为起始位置（默认为0），n为结束位置（默认为npos）
返回值：子字符串

### to_string函数

c++11标准增加了全局函数std::to_string:

原型：

string to_string (int val);

string to_string (long val);

string to_string (long long val);

string to_string (unsigned val);

string to_string (unsigned long val);

string to_string (unsigned long long val);

string to_string (float val);

string to_string (double val);

string to_string (long double val);

功能：int转换成string

### atoi/atof/atol

采用标准库中atoi函数,对于其他类型也都有相应的标准库函数，比如浮点型atof(),long型atol()等等

# 注释

```c++
/// @brief

//

/* --- */
```

# 函数

| 函数       | 含义                                 |
| ---------- | ------------------------------------ |
| swap(a,b)  | swap 包含在命名空间std 里面,交换a和b |
| swap(a,b,) |                                      |

## string.h、cstring(C)

|                    函数                    |                             含义                             |
| :----------------------------------------: | :----------------------------------------------------------: |
|        strcat(char[], const char[])        |                        字符串连接函数                        |
|     strncat(char[],const char[],int )      |                        字符串连接函数                        |
|        strcpy(char[],const char[])         |                        字符串复制函数                        |
|      strncpy(char[],const char[],int)      |                        字符串复制函数                        |
|      strcmp(const char[],const char)       |                        字符串比较函数                        |
|         strlenstrlen(const char[])         |                        字符串长度函数                        |
|         memset(char[], int, int )          |                          初始化函数                          |
| char *strtok(char srcl, const char *delim) |         字符串分割src为待分解的字符串, delim为分隔符         |
|   char *strstr(char *str1, char *str2);    | 找出str2字符串在str1字符串中第一次出现的位置（不包括str2的串dao结束符） |

## cstring、string（C++）

|               函数               |     含义     |
| :------------------------------: | :----------: |
|           find(string)           |   正向查找   |
|           find(string)           |   逆向查找   |
| replacereplace(int,int ,string ) | 替换子串函数 |

## math.h、cmath

|             函数              |          含义           |
| :---------------------------: | :---------------------: |
|        int abs(int i)         |  返回整型参数i的绝对值  |
|     double fabs(double x)     | 返回双精度参数x的绝对值 |
|       long labs(long n)       | 返回长整型参数n的绝对值 |
|     double exp(double x)      |   返回指数函数e^x的值   |
| double pow(double x,double y) |       返回x^y的值       |
|      double pow10(int p)      |      返回10^p的值       |
|     double log(double x)      |      返回logex的值      |
|    double log10(double x)     |     返回log10x的值      |
|     double sqrt(double x)     |       返回√x的值        |
|      int ceil(double x)       |  返回不小于x的最小整数  |
|      int floor(double x)      |  返回不大于x的最大整数  |

## stdlib.h、cstdlib

|             函数             |            含义             |
| :--------------------------: | :-------------------------: |
|     void exit(int code)      |        终止程序执行         |
| void * malloc(long NumBytes) |          申请内存           |
|     void free(void *ptr)     |          释放内存           |
|     void srand(int seed)     |      随机数生成器种子       |
|        int rand(void)        | 生成0~32768之间的一个随机数 |

## algorithm

|            函数             | 含义 |
| :-------------------------: | ---- |
|  sort(begin, end, less())   | 升序 |
| sort(begin, end, greater()) | 降序 |



## for(:)语句

```c++
for(auto n:str){...};//不需要修改数组时
for(auto &n:str){...};//要修改数组时
```



# 指针

```c++
<typename>* <pointname> = new <typename>
<typename>* <pointname> = new <typename>[<length>]
str[i]<=>*(str+i);
String*glamour;//声明指向类对象的指针
String*first=&sayings[0];//将指针初始化为已有对象
String*gleep=new String;//使用new和默认的类构造函数对指针进行初始化
String*favorite=new String(sayings[choice]);//使用new和String(const string&)类构造函数对指针进行初始化
if(sayings[i].length()<shortest->length());//使用->操作符通过指针访问类方法
if(sayingts[i]<*first)//使用*解除引用操作符获得对象
```

# class 类

|   权限    |      |
| :-------: | :--: |
|  public   | 公有 |
| protected | 保护 |
|  private  | 私有 |

## 特殊成员函数

### 	默认构造函数

```c++
typename::typename(typename name=<default value>):name(value){};
```



```c++
//带参数的构造函数可以是默认构造函数,只要所有参数都有默认值
<class name>(typename parameter=<default value>){};
//使用new[]来初始化c_pointer
c_name&c_name::operator=(const c_name&cn){
    if(this==&cn){
        return *this;
    }
    delete[]c_pointer;
    //set size number of type_name units to be copied 
    c_pointer=new type_name[size];
    //the copy data pointed to by cn.c_pointer to location pointed to by c_pointer
    return *this;
}
```

默认构造函数要么没有参数，要么所有的参数都有默认值。如果没有定义任何构造函数，编译器将定义默认构造函数

### 默认析构函数

```
typename::~typename(){};
```

构造函数中要么使用new[],要么使用new,而不能混用.
*    如果**构造函数**使用的还是new[],则析构函数 应使用delete[]
*    如果**构造函数**使用的是new,则析构函数应使用delete

### 复制构造函数

```c++
typename::typename(const typename&_name);
```

复制构造函数接收其所属类的对象作为参数

*    将对象初始化为一个同类对象
*    按值将对象传递给函数
*    函数按值返回对象
*    编译器生成临时对象

### 赋值运算符

```c++
typename&operator=(const typename&_classname);
```

如果编译器发现程序将一个对象赋给同一个类的另一个对象，它将自动为这个类提供一个赋值运算符

如果类构造函数使用new来初始化指针，则需要提供一个显式赋值运算符

如果派生类使用了new，则必须提供显式赋值运算符

```c++
using namespace std;
baseDMA&baseDMA::operator=(const baseDMA&rs){//赋值运算符
    if(this==&rs){
        return *this;
    }
    delete[]label;
    label=new char[strlen(rs.label)+1];
    rating=rs.rating;
    return *this;
}
```

### 地址运算符

## 派生类和基类之间的关系

```c++
class Base{
private:
    typename value;
public:
    Base(typename _value=<default value>):value(_value){};
    virtual ~class_one(){};
}

class Pro():
	public Base
{
private:
	
public:
	Pro(){};
    ~Pro(){};
}
```

以公有方式派生的类的对象可以通过多种方式来使用基类的方法

*    派生类对象自动使用继承而来的基类方法，如果派生类没有重新定义该方法
*    派生类的构造函数自动调用基类的构造函数
*    派生类的构造函数自动调用基类的默认构造函数，如果没有在成员初始化列表总置顶其他构造函数
*    派生类构造函数显式地调用成员初始化列表中指定的基类构造函数
*    派生类方法可以使用作用域解析运算符来调用公有和受保护的基类方法
*    派生类的友元函数可以通过强制类型转换，将派生类引用或指针转换为基类引用或指针，然后使用该引用或指针调用基类的友元函数

|    函数    | 能否继承 | 成员还是友元 | 默认能否生成 | 能否为虚函数 | 是否可以有返回类型 |
| :--------: | :------: | :----------: | :----------: | :----------: | :----------------: |
|  构造函数  |    否    |     成员     |      能      |      否      |         否         |
|  析构函数  |    否    |     成员     |      能      |      能      |         否         |
|     =      |    否    |     成员     |      能      |      能      |         能         |
|     &      |    能    |     任意     |      能      |      能      |         能         |
|  转换函数  |    能    |     成员     |      否      |      能      |         否         |
|     ()     |    能    |     成员     |      否      |      能      |         能         |
|     []     |    能    |     成员     |      否      |      能      |         能         |
|     ->     |    能    |     成员     |      否      |      能      |         能         |
|    op=     |    能    |     任意     |      否      |      能      |         能         |
|    new     |    能    |   静态成员   |      否      |      否      |       void*        |
|   delete   |    能    |   静态成员   |      否      |      否      |        void        |
| 其他运算符 |    能    |     任意     |      否      |      能      |         能         |
|  其他成员  |    能    |     成员     |      否      |      能      |         能         |
|    友元    |    否    |     友元     |      否      |      否      |         能         |

派生类对象能使用基类的方法,条件是方法不是私有的

**构造函数和析构函数都不能继承，赋值运算符不能继承+**

**基类指针可以在不进行显示类型转换的情况下指向派生类对象;基类引用可以在不进行显式类型转换的情况下引用派生类对象**

公有继承	public	

is-a关系(**建议**)

has-a关系

is-implemented-as-a关系

uses-a关系

**最好对类数据成员采用私有访问控制**，不要使用保护访问控制；同时通过基类方法使派生类能够访问基类数据

|       特征       |       公有继承       |        保护继承        |       私有继承       |
| :--------------: | :------------------: | :--------------------: | :------------------: |
|   公有成员变成   |   派生类的公有成员   |    派生类的保护成员    |   派生类的私有成员   |
|   保护成员变成   |   派生类的保护成员   |    派生类的保护成员    |   派生类的私有成员   |
|  私有成员变变成  | 只能通过基类接口访问 |  只能通过基类接口访问  | 只能通过基类接口访问 |
| 能够隐式向上转换 |          是          | 是（但只能在派生类中） |          否          |

### 多重继承

```c++
class classname:public class_one,public class_two{...}  
```



## 重定义访问权限

希望Student类能够使用valarray类的sum()方法，可以在Student类的声明中声明一个sun()方法

```c++
double student::sum()const{
    return std::valarray<double>::sum();
}
```

将包装在另一个函数调用中

```c++
class Student:private std::string,private std:vallary<double>{
public:
    using std::valarray<double>::min;
    using std::valarray<double>::max;
}
```



### 派生类使用new

为派生类定义显示**析构函数**、**复制构造函数**和**赋值运算符**

```c++
baseDMA::~baseDMA(){//析构函数
    delete[]label;
    return;
}
hasDMA::~hasDMA(){//析构函数
    delete style;
    return;
}
```

```c++
using namespace std;
baseDMA::baseDMA(const baseDMA&rs){//复制构造函数
    label=new char[strlen(re.label)+1];
    strcpy(label,rs.label);
    rating=rs.rating;
    return;
}
```

```c++
using namespace std;
baseDMA&baseDMA::operator=(const baseDMA&rs){//赋值运算符
    if(this==&rs){
        return *this;
    }
    delete[]label;
    label=new char[strlen(rs.label)+1];
    rating=rs.rating;
    return *this;
}
```



### 虚方法（virtual method）

>    **允许在派生类中重新定义与基类同名的函数,并且可以通过基类指针或引用来访问基类和派生类中的同名函数。**

如果方法是通过引用或指针而不是对象调用的，它将确定使用哪一种方法。如果没有使用关键字virtual，程序将根据引用类型或指针类型选择方法；如果使用了virtual，程序将根据引用或指针指向的对象的类型来选择方法

在基类方法的声明中使用关键字virtual可使该方法在基类以及所有的派生类中是虚的

如果使用指向对象的引用或指针来调用虚方法，程序将使用为对象类型定义的方法，而不使用为引用或指针类型定义的方法，称之为**动态联编**

>    **构造函数不能是虚函数，析构函数应当是虚函数**，除非类不用做基类

友元不能是虚函数，友元不是类成员，而只用成员才能是虚函数

#### 纯虚方法

```c++
virtual typename founctionname()const=0
```

纯虚方法用于定义派生类的通用接口

**可以在声明中的分号前面加上=0来声明纯虚方法**

### 虚基类

从虚基类的一个或多个实例派生而来的类将只继承一个基类对象，为实现这种特性，必须满足其他要求

*    有间接虚基类的派生类包含直接调用间接基类构造函数的构造函数，这对于间接非虚基类来说是非法的
*    通过优先规则解决名称二义性

#### M1

M1会增加编程的复杂程度，这种**复杂性主要是由于派生类通过多条途径继承同一个基类引起的**

### ABC理念

在处理继承的问题上，在设计ABC之前，首先应**开发一个模型**，指出编程问题所需的类以及它们之间的相互关系。如果要设计类继承层次，则只能将那些不会用作基类的类设计为具体的类

可以将ABC看做是一种必须实施的接口，ABC要求不提派生类覆盖其纯虚函数，**迫使派生类遵循ABC设置的接口规则**，在这种情况下，使用ABC使得组件设计人员能够制定“接口约定”，确保从ABC派生出的所有组件都至少支持ABC指定的功能。

## 返回对象和返回引用

如果函数返回在函数中创建的临时对象，则不要使用引用（&）

如果函数返回的是通过引用或指针传递给它的对象，则应按引用返回对象

### const确保方法不修改调用它的对象

## 友元类、函数

```c++
class classname{
private:
    typename value;
public:
    classname(typename _name=<default value>):value(_name){};
    //friend function
    friend typename functionname(typename _name){};
}
```

友元能访问类的私有成员

## 私有继承

has-a

使用私有继承，基类的公有成员和保护成员都将成为派生类的私有成员，意味着基类方法不会成为派生对象公有接口的一部分

私有继承提供的特性与包含相同，获得实现，但不获得接口

# operator 重载运算符

```c++
operator typename();//类型转换
ostream& operator<<(ostream& _out,<object>& _name);//重载cout
ofstream& operator<<(ofstream& _out,<object>& _name);//重载ofstream
```



# 循环

```c++
//---
for(  ;  ;  ){

}
//---
do{

}while();
//---
while(){

}
```

# valarray class

valarray类是由头文件valarray支持的，用于处理数值，支持诸如将数组中所有元素的值相加以及在数组中找出最大和最小的值等操作

valarray定义为模板类

```c++
operator//访问各个元素
size()//返回包含的元素数
sum()//返回所有的元素总和
max()//返回最大的元素
min()//返回最小的元素
```

# template 类模板

模板提供参数化类型，能够将类型名作为参数传递给接收方来建立类或函数

## 定义类模板

```c++
template<typename T>
//function
```

>    **不能将模板成员函数放在独立的实现文件中** 

由于模板不是函数，不能单独编译。模板类必须与特定的模板实例化请求一起使用

## 递归使用模板

```c++
ArrayTP<ArrayTP<int,5>,10>twodee;
```

## 默认类型模板参数

```c++
template<typename T1,typename T2=int>
class classname{
public:
private:
}
```

## 显式实例化

*    当使用键字template并指出所需类型来声明类时，编译器将生成类声明的显式实例化

```c++
template class ArrayTP<string,100>;
```

## 显式具体化

*    显式具体化是特定类型的定义

```c++
template<typename T>
class SortedArray{
    //details omitted
}
```

## 部分具体化

```c++
template<class T1,class T2>class Pair{...}
template<class T1>class Pair<T1,int>{...}
```

## 将模板用作参数

```
template<template<typename T>class Thing>
class Crab
```

*    template<typename T>class是类型，Thing是参数

## 模板类和友元

### 非模板友元

```c++
template<class T>
class HsaFriend{
    public:
    friend void counts();//friend to all HasFriend instantiations
}
```

### 模板类的约束模板友元函数

首先，在类定义的前面声明每个模板函数

```c++
template<typename T>void counts();
template<typename T>void report(T &);
```

然后，在函数中再次将模板声明为友元

```c++
template <typename TT>
class HasFriendT{
	friend void counts<TT>();
	friend void report<>(HasFriendT<TT>&);
}
```

声明中的<>指出这是模板具体化。对于report()，<>可以为空，可以从函数参数推断出模板类型参数

第三步，为友元提供模板定义

```c++
template <typename T>void counts(){...}
template <typename T>void report(T& hf){...}
```

## 模板类的非约束模板友元函数

通过在类中声明模板，可以创建非约束友元函数

# 异常

## 调用abort()

受控方式运行代码

abort()函数位与头文件**cstdlib**中，典型实现是向标准错误流发送消息abnormal program termination，然后终止程序
**abort()是否刷新文件缓冲区取决于实现**，如果愿意，也可以用exit()，该函数刷新文件缓冲区，但不显示消息

## 异常机制

>    对异常的处理包含3个组成部分
>
>    *    引发异常
>    *    使用处理程序捕获异常
>    *    使用try块

throw关键字表示引发异常，紧随其后的值指出了异常的特征

程序使用异常处理程序来捕获异常，异常处理程序位与要处理问题的程序中

catch关键字表示捕获异常，以关键字catch开头，随后是位与括号中的类型声明，指出了异常处理程序要相应的异常类型；然后是一个用花括号括起的代码块，指出要采取的措施。catch关键字和异常类型用作标签，指出当异常被引发时，程序应跳到这个位置执行

try块表示其中特定的异常可能被激活的代码块，后面跟一个或多个catch块。try块是由关键字try指示的，关键字try的后面是一个由花括号括起的代码块，表明需要注意这些代码引发的异常

```c++
try{

}
catch{

}
```

## 栈解退

c++通常通过将信息放在栈中来处理函数调用

程序将调用函数的指令的地址放在栈中。当被调函数执行完毕后，程序将使用该地址来确定从哪里开始继续执行。

函数调用将函数参数放在栈中。在栈中，这些函数参数被视为自动变量。如果被调用的函数创建了新的自动变量，则这些变量也将被添加到栈中。如果被调用的函数调用了另一个函数，则后者的信息将被调用时存储的地址处，同时栈顶的元素被释放。

>    假设函数由于出现异常而终止，则程序也将释放栈中的内存，但不会再释放栈的第一个返回地址后停止，而是继续释放栈，直到找到一个位于try块的返回地址。随后，控制权交啊ing转到块尾的异常处理程序，而不是函数调用后面的第一条语句。

函数返回仅仅处理该函数放在栈中的对象，而throw语句则处理try块和throw之间整个函数调用序列放在栈中的对象。

## stdexcept异常类

头文件**stdexcept**定义了其他几个异常类。首先，该文件定义了logic_error和runtime_error类，它们都是以公有方式从exceptin派生而来的:

```c++
class logic_error:public exception{
public:
explicit logic_error(const string& what_arg);
    ...
}

class domain_error:public logic_error{
public:
explicit domain_error(const string& what_arg);
    ...
}
```

每个类的名称指出了它用于报告的错误类型

|     错误类型     |              解释              |
| :--------------: | :----------------------------: |
|   domain_error   |          定义域和值域          |
| invalid_argument |    给函数传递了一个意外的值    |
|   length_error   | 没有足够的空间来执行所需的操作 |
|  out_of_bounds   |            索引错误            |

每个类独有一个类似于logic_error的构造函数，能够提供一个供方法what()返回的字符串

接下来，**runtime_error**异常系列描述了可能在运行期间发生但难以预计和防范的错误

|    错误类型     |                            解释                            |
| :-------------: | :--------------------------------------------------------: |
|   range_error   | 计算结果可能不再函数允许的范围之内，但没有发生上溢下溢错误 |
| overflow_error  |                          上溢错误                          |
| underflow_error |                          下溢错误                          |

## bad_alloc异常和new

对于使用new导致的内存分配问题，让new引发bad_alloc异常

头文件new包含bad_alloc类的声明，是从exception类公有派生而来的

# RTTI

## RTTI用途

### dynamic_cast

判断是否可以将对象的地址赋给特定类型的指针

```c++
dynamic_cast <type-id> (expression)
```

>    **该运算符把expression转换成type-id类型的对象。Type-id 必须是类的指针、类的引用或者void***
>
>    **dynamic_cast运算符用于将派生类指针转换为基类指针，其主要用途是确保可以安全地调用虚函数。**

如果可以，运算符将返回对象的地址，否则返回一个空指针

即便编译器支持RTTI，在默认情况下，它也可能关闭该特性，程序可能仍然能通过编译。

应尽可能使用虚函数，而在必要时使用RTTI。

### typeid

typeid运算符使能够确定两个对象是否为同种类型，与sizeof有些相像，可以接收两种参数

>    **typeid运算符返回一个type_info对象。可以对两个typeid的返回值进行比较，以确定对象是否为特定的类型，而返回的type_info对象可用于获得关于对象的信息。**

|        参数        |      使用方法      |
| :----------------: | :----------------: |
|        类名        |  typeid(dataType)  |
| 结果为对象的表达式 | typeid(expression) |

### type_info

```
class type_info {
public:
    virtual ~type_info();
    int operator==(const type_info& rhs) const;
    int operator!=(const type_info& rhs) const;
    int before(const type_info& rhs) const;
    const char* name() const;
    const char* raw_name() const;
private:
    void *_m_data;
    char _m_d_name[1];
    type_info(const type_info& rhs);
    type_info& operator=(const type_info& rhs);
};
```

C++ 标准规定，type_info 类至少要有如下所示的 4 个 public 属性的成员函数，其他的扩展函数编译器开发者可以自由发挥，不做限制。

|                     原型                     |                             用法                             |
| :------------------------------------------: | :----------------------------------------------------------: |
|           const char* name() const           | 返回一个能表示类型名称的字符串。但是C++标准并没有规定这个字符串是什么形式的，例如对于上面的`objInfo.name()`语句，VC/VS 下返回“class Base”，但 GCC 下返回“4Base”。 |
|   bool before (const type_info& rhs) const   | 判断一个类型是否位于另一个类型的前面，rhs 参数是一个 type_info 对象的引用。但是C++标准并没有规定类型的排列顺序，不同的编译器有不同的排列规则，程序员也可以自定义。要特别注意的是，这个排列顺序和继承顺序没有关系，基类并不一定位于派生类的前面。 |
| bool operator== (const type_info& rhs) const | 重载运算符“==”，判断两个类型是否相同，rhs 参数是一个 type_info 对象的引用。 |
| bool operator!= (const type_info& rhs) const | 重载运算符“!=”，判断两个类型是否不同，rhs 参数是一个 type_info 对象的引用。 |

## 类型转换运算符

更严格限制允许的类型转换，并添加4个类型转换运算符，使转换过程更规范

|      运算符      | 用法                                    |                             作用                             |
| :--------------: | --------------------------------------- | :----------------------------------------------------------: |
|   dynamic_cast   | dynamic_cast<type-name>(expression)     |      使能够在类层次结构中进行向上转换，而不允许其他转换      |
|    const_cast    | const_cast<type-name>(expression)       | 除了const或volatile特征可以不同之外，type_name和expression的类型必须相同 |
|   static_cast    | static_cast<type-name>(expression)      | 仅当type_name可被隐式转换为expession所属的类型或expresion可被隐式转换为type_name所属的类型时，上述转换才是合法的 |
| reinterpret_cast | reinterpret_cast<type-name>(expression) | reinterprete_cast运算符并不支持所有的类型转换，不能将函数指针转换为数据指针，反之亦然 |

# string class

>    **string实际上是模板具体化basic_string<char>的一个typedef，同时省略了与内存管理相关的参数**

## 构造函数

|                           构造函数                           |                             描述                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|                     string(const char*s)                     |               将string对象初始化Wies指向的NBTS               |
|                 string(size_type n, char c)                  | 创建一个包含n个元素的string对象，其中每个元素都被初始化为字符c |
|                  string(const string& str)                   |            将一个string对象初始化为string对象str             |
|                           string()                           |              创建一个默认的string对象，长度为0               |
|              string(const char* s, size_type n)              | 将string对象初始化为s指向的NBTS的前n的字符，即使超过了NBTS结尾 |
|       template<class Iter>string(Iter begin, Iter end)       | 将string对象初始化为区间[begin, end]内的字符，其中begin和end的行为就像指针，用于指定位置，范围包括begin在内，但不包括end |
| string(const string& str,string size_type pos = 0,size_type n = npos) | 将一个string对象初始化为对象str中从位置pos开始到结尾的字符，或从位置pos开始的n个字符 |
|                string(string && str)noexcept                 | C++11新增，将一个string对象初始化为string对象str，并可能修改str |
|              string(initializer_list<char> il)               |   c++11新增，将一个string对象初始化为初始化列表il中的字符    |

## string类输入

### c风格字符串-数组

```c++
char info[100];
cin>>info;//read a word
cin.getline(info,100);//read a line, discard
cin.get(info,100);//read a line, leave
```

### string对象

```c++
string stuff;
cin>>stuff;//read a word
getline(cin,stuff);//read a line, discard
```

### getline版本

```c++
cin.getline(info,100,':');//read up to :, discard :
getline(stuff,':');//read up to :, discard :
```

## 使用字符串

### 比较字符串

string类对全部6个关系运算符都进行重载。如果在机器排列序列中，一个对象位与另一个对象的前面，则前者被视为小于后者。如果机器排列序列为ASCII码，则数字将小于大写字符，而大写字符小于小写字符。

### 字符串的长度

*    size()和length()成员函数都返回字符串中的字符数

### 搜索给定子字符或字符

| 方法原型                                                     | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| size_type find(const string & str, size_type pos = 0)const   | 从字符串的pos位置开始，查找子字符串str。如果找到，则返回该子字符串首次出现时其首字符的索引；否则，返回string::npos |
| size_type find(const char *s, size_type pos = 0)const        | 从字符串的pos位置开始，查找子字符串s。如果找到，则返回该子字符串首次出现时首字符的索引；否则，返回string::npos |
| size_type find(const char * s, size_type pos = 0, size_type n) | 从字符串的pos位置开始，查找s的前n个字符组成的子字符串。如果找到，则返回该子字符串首次出现时其首字符的索引；否则，返回string::npos |
| size_type find(char ch,size_type pos = 0)const               | 从字符串的pos位置开始，查找字符ch。如果找到，则返回该字符首次出现的位置；否则，返回string::npos |

由于关系运算符被重载，因此可以像对待数值变量那样对待字符串

```c++
while(guesses>0&&attempt!=target)
```

>    npos变量是string类的静态成员，它的值是string对象能存储的最大字符数。由于索引从0开始，所以它比最大的索引值大1，因此可以使用它来表示没有查找到字符或字符串。

### 自动调整大小

|    方法    |               解释               |
| :--------: | :------------------------------: |
| capacity() | 返回当前分配给字符串的内存块大小 |
| reserve()  |       请求内存块的最小长度       |

很多C++实现分配一个比实际字符串大的内存块，为字符串提供了增大空间。然而，如果字符串不断增大，超过了内存块的大小，程序将分配一个大小为原来两倍的新内存块，以提供足够的增大空间，避免不断地分配新的内存块。

# 智能指针

```c++
void remodel(string & str){
    string * ps=new string(str);
    ...
        str = ps;
    return;
}
```

每当调用时，该函数都分配堆中的内存，但从不收回，从而导致内存泄露

在return语句前添加下面的语句，以释放分配的内存

```c++
delete ps;
```

## 选择智能指针

要创建智能指针对象，必须包含头文件memory，该文件模板定义。然后使用通常的模板来实例化所需要类型的指针。

|  智能指针  |                   用法                   |
| :--------: | :--------------------------------------: |
|  auto_ptr  |  auto_ptr<type-name>name(new type-name)  |
| unique_ptr | unique_ptr<type-name>name(new type-name) |
| shared_ptr | shared_ptr<type-name>name(new type-name) |
|  weak_ptr  |  weak_ptr<type-name>name(new type-name)  |



```c++
#include <memory>
auto_ptr<double>pd(new double);
auto_ptr<std::string>ps(new std::stirng);
```

```c++
unique_ptr<double>pdu(new double);
shared_ptr<std::string>pss(new std::string);
```

auto_ptr被c++11摒弃，**避免潜在的内存泄漏问题**

>    你在一个函数中使用智能指针，在用的时候会有引用计数增加，这个时候指针指向的内存是有值的。
>
>    接着你将**一个正常指针指向这块内存区域，都能正常访问，但是他没有通知智能指针增加引用计数**，这就埋下伏笔！
>
>    然后，你的**智能指针不再被使用，（出了作用域等）引用计数减完，然后C++会自动删除指针所指向的内存区域，并释放！**
>
>    这时，正常指针并不知道自己所指向的区域已经被删除了，就变成了野指针，接下就是崩溃啦~~~~

### 指针类型

如果程序要使用多个指向同一个对象的指针，应选用`shared_ptr`。这样的情况包括：

-    有一个指针数组，并使用一些辅助指针来标示特定的元素，如最大的元素和最小的元素；
-    连个对象包含指向第三个对象的指针；
-    STL容器包含指针。很多STL算法都支持复制和赋值操作，这些操作可用于shared_ptr，但不能用于unique_ptr（编译器发出warning）和auto_ptr（行为不确定）。如果你的编译器没有提供shared_ptr，可使用Boost库提供的shared_ptr。

如果程序不需要多个指向同一个对象的指针，则可使用unique_ptr。如果函数使用new分配内存，并返还指向该内存的指针，将其返回类型声明为unique_ptr是不错的选择。这样，所有权转让给接受返回值的unique_ptr，而该智能指针将负责调用delete。可将unique_ptr储存到STL容器中，只要不调用将unique_ptr**复制或赋值**给另一个算法（如sort())。例如，可在程序中使用类似于下面的代码段：

设计weak_ptr的原因：**解决使用shared_ptr因循环引用而不能释放资源的问题。**

*    weak_ptr不控制对象的生命期，但是它知道对象是否还活着，如果对象还活着，那么它可以提升为有效的shared_ptr（提升操作通过lock()函数获取所管理对象的强引用指针）；如果对象已经死了，提升会失败，返回一个空的shared_ptr。

# 标准模板库STL

STL不是面向对象编程，而是泛型编程

## 模板类vector

```c++
vector<type-name>name(length);
```

vector使用动态内存分配，可以用初始化参数来指出需要多少矢量

### 合并两个vector

```c++
#include <vector>
using namespace std;

vector<type_name> name_one(size);
vector<type_name> name_two(size);
name_one.insert(name_one.end(),name_two.begin(),name_two.end());
```

# c++输入和输出

## 流和缓冲区

C++程序把输入和输出看做字节流。输入时，程序从输入流中抽取字节；输出时，程序将字节插入到输出流中。

流充当了程序和流源或流目标之间的桥梁。

管理输入包含

*    将流与输入去向的程序关联起来
*    将流与文件连接起来

缓冲区是用作中介的内存块，将信息从设备传输到程序或从程序传输给设备的临时存储工具。

输出时，程序首先填满缓冲区，然后把整块数据传输给硬盘，并清空缓冲区，以备下一批输出使用。这被称为**刷新缓冲区**。

## 流、缓冲区和iostream文件

iostream文件中包含一些专门设计用来实现、管理流和缓冲区的类。

*    streambuf类为缓冲区提供了内存,并提供了用于填充缓冲区、访问缓冲区内容、刷新缓冲区和管理缓冲区内存的类方法;
*    ios_base类表示流的一般特征,如是否可读取、是二进制流还是文本流等;
*    ios类基于ios-base,其中包括了一个指向streambuf对象的指针成员;
*    ostream类是从ios类派生而来的,提供了输出方法;
*    istream类也是从ios类派生而来的,提供了输入方法;
*    iostream类是基于istream和ostream类的,因此继承了输入方法和输出方法

---

*    cin对象对应于标准输入流。在默认情况下,这个流被关联到标准输入设备(通常为键盘)。wcin对象与此类似,但处理的是whar_t类型。
*    cout对象与标准输出流相对应。在默认情况下,这个流被关联到标准输出设备(通常为显示器) 。wcout对象与此类似,但处理的是wchar_t类型。
*    cerr对象与标准错误流相对应,可用于显示错误消息。在默认情况下,这个流被关联到标准输出设备(通常为显示器)。这个流没有被缓冲,这意味着信息将被直接发送给屏幕,而不会等到缓冲区填满或新的换行符。wcerr对象与此类似,但处理的是whar_t类型。
*    clog对象也对应着标准错误流。在默认情况下,这个流被关联到标准输出设备(通常为显示器)。这个流被缓冲。wclog对象与此类似,但处理的是wchar_t类型。
*    对象代表流。当iostream文件为程序声明一个cout对象时,该对象将包含存储了与输出有关的信息的数据成员,如显示数据时使用的字段宽度、小数位数、显示整数时采用的计数方法以及描述用来处理输出流的缓冲区的streambuf对象的地址。下面的语句通过指向的streambuf对象将字符串"Bjarna free"中的字符放到cout管理的缓冲区中。

## 重载的<<运算符

|  头文件  |   使用方法   |            原型            |
| :------: | :----------: | :------------------------: |
| iostream | cout<<value; | ostream & operator<<(int); |

## put

|         原型         |       调用        |
| :------------------: | :---------------: |
| ostream & put(char); | cout.put().put(); |

## write

|                             原型                             |
| :----------------------------------------------------------: |
| basic_ostream<charT,traits>& write(const char_type* s, streamsize n); |

write()方法并不会在遇到空字符时自动停止打印字符，而只是打印指定数目的字符，即使超出了字符串的边界

## 刷新输入缓冲区

将换行符发送到缓冲区后，将刷新缓冲区。

如果实现不能在所希望时刷新输出，可以使用两个控制符中的一个来强制进行刷新。

| 控制符 |             含义             |     使用     |
| :----: | :--------------------------: | :----------: |
| flush  |          刷新缓冲区          | cout<<flush; |
|  endl  | 刷新缓冲区，并插入一个换行符 | cout<<endl;  |

控制符也是函数

```c++
flush(cout);
```

ostream类对<<插入运算符进行了重载，使得下述表达式将被替换为函数调用flush(cout)

```c++
cout<<flush;
```

## 用cout进行格式化

ostream插入运算符将值转换为文本格式。在默认情况下,格式化值的方式如下。

*    对于char值,如果它代表的是可打印字符,则将被作为一个字符显示在宽度为一个字符的字段中。

*    对于数值整型,将以十进制方式显示在一个刚好容纳该数字及负号(如果有的话)的字段中。

*    字符串被显示在宽度等于该字符串长度的字段中。

浮点数的默认行为有变化。下面详细说明了老式实现和新实现之间的区别。

*    **新式**:浮点类型被显示为6位,末尾的0不显示(注意,显示的数字位数与数字被存储时精度没有任何关系)。数字以定点表示法显示还是以科学计数法表示(参见第3章),取决于它的值。具体来说,当指数大于等于6或小于等于一5时,将使用科学计数法表示。另外,字段宽度恰好容纳数字和负号(如果有的话)。默认的行为对应于带%g说明符的标准C库函数fprintf()。
*    **老式**:浮点类型显示为带6位小数,末尾的0不显示(注意,显示的数字位数与数字被存储时的精度没有任何关系)。数字以定点表示法显示还是以科学计数法表示,取决于它的值。另外,字段宽度恰好容纳数字和负号(如果有的话)。

### 修改显示时使用的计数系统

| 十进制 | 十六进制 | 八进制 |
| :----: | :------: | :----: |
|  dex   |   hex    |  oct   |

ostream类是从ios类派生而来的，而后者是从ios_base类派生而来的

>    ios_base类存储了描述格式状态的信息

```c++
hex(cout);
dex(cout);
oct(cout);
```

## 调整字段宽度

```c++
int width();
int width();
```

width()方法只影响将显示的下一个项目，然后字段宽度将恢复为默认值。

>    c++**永远不会截短数据**，如果试图在宽度为2的字段中打印一个7位值，c++将增宽字段，以容纳该数据

## 填充字符

用fill()成员函数来改变填充字符

```c++
cout.fill('char');
```

## 设置浮点数的显示精度

```c++
cout.precision(number);
```

>    新的精度设置将**一直有效**

## 打印末尾的0和小数点

```c++
cout.setf(ios_base::showpoint);
```

showpoint是ios_base类声明中定义的类级静态常量。必须加上作用域运算符(::)

## setf()

|                原型                |
| :--------------------------------: |
|      fmtflags setf(fmtflags);      |
| fmtflags setf(fmtflags, fmtflags); |

### fmtflags setf(fmtflags);

| 常量                | 含义                                  |
| ------------------- | ------------------------------------- |
| ios_base::boolalpha | 输入和输出bool值，可以为true或false   |
| ios_base::showbase  | 对于输出，使用c++基数前缀(0,0x)       |
| ios_base::showpoint | 显示末尾的小数点                      |
| ios_base::uppercase | 对于16进制输出，使用大写字母，E表示法 |
| ios_base::showpos   | 在正数前面加上+                       |

### fmtflags setf(fmtflags, fmtflags);

|      第一个参数      |      第二个参数       |              含义              |
| :------------------: | :-------------------: | :----------------------------: |
|    ios_base::dec     |  ios_base::basefield  |           使用基数10           |
|    ios_base::oct     |  ios_base::basefield  |           使用基数8            |
|    ios_base::hex     |  ios_base::basefield  |           使用基数16           |
|   ios_base::fixed    | ios_base::floatfield  |         使用定点计数法         |
| ios_base::scientific | ios_base::floatfield  |         使用科学计数法         |
|    ios_base::left    | ios_base::adjustfield |           使用左对齐           |
|   ios_base::right    | ios_base::adjustfield |           使用右对齐           |
|  ios_base::internal  | ios_base::adjustfield | 符号或基数前缀左对齐，值右对齐 |

在c++标准中，定点表示法和科学表示法都有下面两个特征

*    精度指的是小数位数，而不是总位数
*    显示末尾的0

setf()函数是ios_base类的一个成员函数。由于这个类是ostream类的基类，因此可以使用cout对象来调用该函数

```c++
ios_base::fmtflags old = cout.setf(,ios::adjustfield);
```

要恢复以前的设置，可以这样做

```c++
cout.setf(old,ios::adjustfield);
```

调用setf()的效果可以通过unsetf()消除，原型如下：

```c++
void unsetf(fmtflags mask);
```

mask是位模式，mask中所有的位都设置为1，将使得对应的位被复位。

>    setf()将位设置为1，unsetf()将位恢复为0

## 标准控制符

|   控制符    |                      调用                      |
| :---------: | :--------------------------------------------: |
|  boolalpha  |           setf(ios_base::boolalpha)            |
| noboolalpha |         unsetf(ios_base::noboolalpha)          |
|  showbase   |            setf(ios_base::showbase)            |
| noshowbase  |          unsetf(ios_base::noshowbase)          |
|  showpoint  |           setf(ios_base::showpoint)            |
| noshowpoint |         unsetf(ios_base::noshowpoint)          |
|   showpos   |            setf(ios_base::showpos)             |
|  noshowpos  |          unsetf(ios_base::noshowpos)           |
|  uppercase  |           setf(ios_base::uppercase)            |
| nouppercase |         unsetf(ios_base::nouppercase)          |
|  internal   | setf(ios_base::internal,ios_base::adjustfield) |
|    left     |   setf(ios_base::left,ios_base::adjustfield)   |
|    right    |  setf(ios_base::right,ios_base::adjustfield)   |
|     dec     |    setf(ios_base::dec,ios_base::basefield)     |
|     hex     |    setf(ios_base::hex,ios_base::basefield)     |
|     oct     |    setf(ios_base::oct,ios_base::basefield)     |
|    fixed    |   setf(ios_base::fixed,ios_base::basefield)    |
| scientific  | setf(ios_base::scientific,ios_base::basefield) |

## 头文件iomanip

|     控制符     |     含义     |
| :------------: | :----------: |
| setprecision() |   设置精度   |
|   setfill()    |   填充字符   |
|     setw()     | 设置字段宽度 |

## 流状态

| 成员                     | 描述                                                         |
| ------------------------ | ------------------------------------------------------------ |
| eofbit                   | 如果到达文件尾，则设置为1                                    |
| badbit                   | 如果流被破坏，则设置为1                                      |
| failbit                  | 如果输入操作未能读取预期的字符或输出操作没有写入预期的字符，则设置为1 |
| goodbit                  | 另一种表示0的方法                                            |
| good( )                  | 如果流可以使用（所有的位都被清除），则返回true               |
| eof( )                   | 如果eofbit被设置，则返回true                                 |
| bad( )                   | 如果badbit被设置，则返回true                                 |
| fail( )                  | 如果badbit或failbit被设置，则返回true                        |
| rdstate( )               | 返回流状态                                                   |
| exceptions( )            | 返回一个位掩码，指出哪些标记导致异常被引发                   |
| exceptions( isostate ex) | 设置哪些状态将导致clear()引发异常；例如，如果ex是eofbit，则如果eofbit被设置，clear()将引发异常 |
| clear( iostate s)        | 将流状态设置为s；s的默认值为0（goodbit）；如果(restate()& exceptions())! = 0，则引发异常basic_ ios:: failure |
| setstate( iostate s)     | 调用clear（ rdstate( )｜ s）。 这将设置与s中设置的位对应的流状态位，其他流状态位保持不变 |

### 设置状态

```c++
clear();
```

```c++
clear(eofbit);
```

```c++
setstate(eofbit);
```

### I/O和异常

exceptions( )方法返回一个位字段,它包含3位,分别对应于eofbit,failbit和badbit。修改流状态涉及clear( )或setstate( ),这都将使用clear( )。

修改流状态后, clear( )方法将当前的流状态与exceptions ( )返回的值进行比较。如果在返回值中某一位被设置,而当前状态中的对应位也被设置,则clear ( )将引发ios_base:: failure异常。如果两个值都设置了badbit,将发生这种情况。如果exceptions ( )返回goodbit,则不会引发任何异常。ios base:: failure异常类是从std::exception类派生而来的,因此包含一个what( )方法。

### 流状态的影响

只有在流状态良好(所有的位都被清除)的情况下,才返回true

设置流状态位有一个非常重要的后果:流将对后面的输入或输出关闭,直到位被清除。

如果希望程序在流状态位被设置后能够读取后面的输入,就必须将流状态重置为良好。这可以通过调用clear( )方法来实现

```c++
cin.clear();
```

### istream类方法

#### 使用cin进行输入

```c++
cin>>value_holder;
```

基本类型

*    signed char &
*    unsigned char &
*    char &
*    unsigned short &
*    int &
*    unsigned int &
*    long &
*    unsigned long &
*    long long &(c++11)
*    float &
*    double &
*    long double &

典型运算符函数原型

```c++
istream & operator>>(int &);
```

可以将hex、oct和dec控制符与cin一起使用，来指定将整数输入解释为十六进制、八进制还是十进制格式。

```c++
cin>>hex;
```

在单字符模式下, >>运算符将读取该字符,将它放置到指定的位置。在其他模式下, >>运算符将读取一个指定类型的数据。也就是说,它读取从非空白字符开始,到与目标类型不匹配的第一个字符之间的全部内容。

#### cin方法

|          方法          |                             含义                             |
| :--------------------: | :----------------------------------------------------------: |
|       cin.get();       |         从输入流中读取一个字符，输入流的数据被取走。         |
|   cin.ignore(n,ch);    | 将输入流中取出一个一个字符，并且每取出一个字符都会进行比较操作，如果取出字符个数等于n停止操作，如果遇到ch字符也停止操作，这个函数可以用来比如消除上一次输入对下一次输入的影响。 |
| cin.getline(str,n,ch); | 从输入流从接收n个字符到str变量中，ch是结束字符如果不给出这个参数那就默认为'\0'，就是当遇到ch这个字符的时候停止接收。 |
|     cin.gcount();      |            获取一个字符变量中包括空白字符的个数。            |
|      cin.read();       |                      只能读取一行的内容                      |
|     cin.getlie();      |               不限定行数直到到达结束标志为止。               |
|      cin.peek();       | 假设要读取输入,直到遇到换行*或句点,则可以用peek ( )查看输入流中的下一个字符,以此来判断是否继续读取: |
|        gcount()        |           返回最后一个非格式化抽取方法读取的字符数           |
|       putback()        | 将一个字符插入到输入字符串中，被插入的字符将是下一条输入语句读取的第一个字符。 |



#### 单字符输入

方法get (char&)和get (void)提供**不跳过空白**的单字符输入功能

函数get (char *, int, char)和getline(char *, int, char)在默认情况下**读取整行**而不是一个单词。

*    get(char &)

在使用char参数或没有参数的情况下, get()方法读取下一个输入字符,即使该字符是空格、制表符或换行符。get (char &ch)版本将输入字符赋给其参数, 而get (void)版本将输入字符转换为整型(通常是int),并将其返回。

*    get(void)

get(void)成员函数读取空白，但使用返回值来输入传递给程序,返回类型为int，因此

```c++
char c1,c2,c3;
cin.get().get()>>c3;//not valid
```

cin.get()将返回一个int值，由于返回值不是类对象，因此不能对它应用成员运算符。会出现语法错误。

```c++
char c1;
cin.get(c1).get();//valid
```

cin.get(c1)返回cin，因此可以放在get()的前面

到达文件尾后，cin.get(void)都将返回EOF值，使得

```c++
int ch;
while((ch = cin.get())!=EOF){
    //process input
}
```

##### cin.get(ch)与cin.get()

|           特征           |      cin.get(ch)      |   ch=cin.get()    |
| :----------------------: | :-------------------: | :---------------: |
|    传输输入字符的方法    |      赋给参数ch       | 将函数返回赋给ch  |
|  字符输入时函数的返回值  | 指向istream对象的引用 | 字符编码（int值） |
| 达到文件尾时函数的返回值 |      转换为false      |        EOF        |

###### 采用哪种单字符输入形式

*    首先,应确定是否希望跳过空白。如果跳过空白更方便,则使用抽取运算符>>。例如,提供菜单选项时,跳过空白更为方便。

*    如果希望程序检查每个字符,请使用get ( )方法。在get( )方法中, get (char &)的接口更佳。get (void)的主要优点是,它与标准c语言中的getchar ( )函数极其类似,这意味着可以通过包含iostream (而不是stdio.h),并用cin. get( )替换所有的getchar( ),用cout. put(ch)替换所有的putchar(ch),来将C程序转换为C++程序。

#### 字符串输入getline()、get()和ignore()

```c++
istream & get(char *, int, char);
istream & get(char *, int);
istream & getline(char *, int, char);
istream & getline(char *, int);
```

*    第一个参数是用于放置输入字符串的内存单元的地址。

*    第二个参数比要读取的最大字符数大1(额外的一个字符用于存储结尾的空字符,以便将输入存储为一个字符串)。

*    第三个参数指定用作分界符的字符,只有两个参数的版本将换行符用作分界符。

上述函数都在读取最大数目的字符或遇到换行符后为止。

get( )和getline( )之间的主要区别在于, 

*    get()将换行符留在输入流中,这样接下来的输入操作首先看到是将是换行符 
*    getline( )抽取并丢弃输入流中的换行符

```c++
cin.ignore();
```

该函数接受两个参数:一个是数字,指定要读取的最大字符数;另一个是字符,用作输入分界符。

原型为

```c++
istream & ignore(int = 1, int = EOF);
```

#### 意外字符串输入

get (char *, int)和getline ( )的某些输入形式将影响流状态。与其他输入函数一样,这两个函数在

*    遇到文件尾时将设置eofbit
*    遇到流被破坏(如设备故障)时将设置badbit
*    另外两种特殊情况是无输入以及输入到达或超过函数调用指定的最大字符数

| 方法                  | 行为                                                         |
| --------------------- | ------------------------------------------------------------ |
| getline( char *, int) | 如果没有读取任何字符（但换行符被视为读取了一个字符），则设置failbit如果读取了最大数目的字符，且行中还有其他字符，则设置failbit |
| get( char *, int)     | 如果没有读取任何字符，则设置failbit                          |

## 简单的文件I/O

让程序写入文件

*    创建一个ofstream对象来管理输出流
*    将该对象与特定的文件关联起来
*    以使用cout的方式使用该对象，唯一的区别是输出将进入文件，而不是屏幕

读取文件

*    创建一个ifstream对象来管理输入流
*    将该对象与特定的文件关联起来
*    以使用cin的方式使用该对象

```c++
fin.close();
fout.close();
```

### 流状态检查is_open()

```c++
if(!fin.isopen()){...};
```

### 命令行处理技术

文件处理程序通常使用命令行参数来指定文件。

命令行参数是用户在输入命令时,在命令行中输入的参数。

```c++
int main(int argc, char *argv []){...}
```

*    很多Windows IDE (集成开发环境)都有一个提供命令行参数的选项。通常,必须选择一系列菜单,才能打开一个可以输入命令行参数的对话框。具体的步骤随厂商和升级版本而异,因此请查看文档。
*    很多Windows IDE都可以生成可执行文件,这些文件能够在Windows命令提示符模式下运行。

### 文件模式

文件模式常量

| 常量             | 含义                     |
| ---------------- | ------------------------ |
| ios_base::in     | 打开文件，以便读取       |
| ios_base::out    | 打开文件，以便写入       |
| ios_base::ate    | 打开文件，并移到文件尾   |
| ios_base::app    | 追加到文件尾             |
| ios_base::trunc  | 如果文件存在，则截短文件 |
| ios_base::binary | 二进制文件               |

### 随机存取

随机存取指的是直接移动(不是依次移动)到文件的任何位置。随机存取常被用于数据库文件,程序维护一个独立的索引文件,该文件指出数据在主数据文件中的位置。这样,程序便可以直接跳到这个位置,读取(还可能修改)其中的数据。

如果文件由长度相同的记录组成,这种方法实现起来最简单。每条记录表示一组相关的数据。

```c++
finout.open(file,ios_base::in|ios_base::out|ios_base::binary);
```

| 方法    | 原型                         |
| ------- | ---------------------------- |
| seekg() | 将输入指针移到指定的文件位置 |
| tellg() | 检查输入指针的当前位置       |
| seekp() | 将输出指针移到指定的文件位置 |
| tellp() | 检查输出指针的当前位置       |

```c++
basic_istream<charT, traits>& seekg(off_type, ios_base::seekdir);
basic_istream<charT, traits>& seekg(pos_type);

istream &seekg(streamoff, ios_base::seekdir);
istream & seekg(streampos);
```

第一个原型定位到离第二个参数指定的文件位置特定距离(单位为字节)的位置

第二个原型定位到离文件开头特定距离(单位为字节)的位置

-    来看seekg ( )的第一个原型的参数。

streamoff值被用来度量相对于文件特定位置的偏移量(单位为字节)。streamoff参数表示相对于三个位置之一的偏移量为特定值(以字节为单位)的文件位置(类型可定义为整型或类)。

seek_dir参数是ios_base类中定义的另一种整型,有3个可能的值。

常量ios_base : : beg指相对于文件开始处的偏移量。

常量ios_base: : cur指相对于当前位置的偏移量;常量ios base : : end指相对于文件尾的偏移量。下面是一些调用示例,这里假设fin是一个ifstream对象:

-    下面来看第二个原型。

streampos类型的值定位到文件中的一个位置。它可以是类,但如果是这样的话,这个类将包含一个接受streamoff参数的构造函数和一个接受整数参数的构造函数,以便将两种类型转换为streampos值。

streampos值表示文件中的绝对位置(从文件开始处算起)。可以将streampos位置看作是相对于文件开始处的位置(以字节为单位,第一个字节的编号为0)。

## 内核格式化

iostream族(family)支持程序与终端之间的1/0,而fstream族使用相同的接口提供程序和文件之间的1/0. C++库还提供了sstream族,它们使用相同的接口提供程序和string对象之间的1/0.也就是说,可以使用于cout的ostream方法将格式化信息写入到string对象中,并使用istream方法(如getline( ))来读取string对象中的信息。读取string对象中的格式化信息或将格式化信息写入string对象中被称为**内核格式化**(incoreformatting)。下面简要地介绍一下这些工具(string的sstream族支持取代了char数组的strstream.h族支持)。

头文件sstream定义了一个从ostream类派生而来的ostringstream类(还有一个基于wostream的wostringstream类,这个类用于宽字符集)。如果创建了一个ostringstream对象,则可以将信息写入其中,它将存储这些信息。可以将可用于cout的方法用于ostringstream对象。

>    istringstream和ostringstream类使得能够使用istream和ostream类的方法来管理存储在字符串中的字符数据。

# 多线程

## 线程

在传统的操作系统中,每个进程都有自己的地址空间和一个执行线程,该线程通常叫<u>主线程</u>(primary thread).一般而言,运行在同一个进程中的多个线程具有相同的地址空间(即进程的地址空间),在准并行上下文中,这些线程就像是多个单独运行的进程,只不过它们的地址空间相同。

## _tmain() 和 main()

首先，这个_tmain()是为了支持unicode所使用的main一个别名而已。

既然是别名，应该有宏定义过的，在哪里定义的呢？就在那个让你困惑的<stdafx.h>里，有这么两行：

```c++
#include <stdio.h>
#include <tchar.h>
```

我们可以在头文件<tchar.h>里找到_tmain的宏定义   

```c++
#define  _tmain  main
```

所以，经过预编译以后， _tmain就变成main了

main()是标准C++的函数入口。标准C++的程序入口点函数,默认字符编码格式ANSI

函数签名为：

```c++
int main();
int main(int argc, char* argv[]);
```

<u>_tmain()是windows提供的对unicode字符集和ANSI字符集进行自动转换用的程序入口点函数</u>

函数签名为:

```c++
int _tmain(int argc, _TCHAR *argv[])
```

(1) 当你程序当前的字符集为unicode时，int _tmain(int argc, TCHAR *argv[])会被翻译成

```c++
int wmain(int argc, wchar_t *argv[])
```

wmain也是main的另一个别名,是为了支持二个字节的语言环境

(2) 当你程序当前的字符集为ANSI时，int _tmain(int argc, TCHAR *argv[])会被翻译成

```c++
int main(int argc, char *argv[])
```

>    我们需要实现一个程序的入口点: main函数。前面提到过, ANSI签名用main.Unicode签名用wmain,编译器根据项目属性页的预处理器定义确定签名用tmain。对于控制台应用程序, main函数有以下4种不同的原型:
>
>    -    int tmain(int argc, TCHAR* argv[])
>    -    void tmain(int argc, TCHAR* argv[])
>    -    int tmain (void)
>    -    void tmain (void)

# 参考

*    Stephen Prata. C++ Primer Plus（第6版）中文版（异步图书） (C和C++实务精选) . 人民邮电出版社.  
*    [黑山共和国]米洛斯·留莫维奇（Milos Ljumovic）. C++多线程编程实战 (Kindle 位置 344-345). 人民邮电出版社.
