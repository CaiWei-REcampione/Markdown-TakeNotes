# 参数声明

```c++
<typename> int
<point>=new <typename>
delete <point>
```

# 注释

```c++
/// @brief

//

/* --- */
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

## 权限

​	public

​	protected

​	private

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

>    该运算符把expression转换成type-id类型的对象。Type-id 必须是类的指针、类的引用或者void*
>
>    dynamic_cast运算符用于将派生类指针转换为基类指针，其主要用途是确保可以安全地调用虚函数。
>

如果可以，运算符将返回对象的地址，否则返回一个空指针

即便编译器支持RTTI，在默认情况下，它也可能关闭该特性，程序可能仍然能通过编译。

应尽可能使用虚函数，而在必要时使用RTTI。

### typeid

typeid运算符使能够确定两个对象是否为同种类型，与sizeof有些相像，可以接收两种参数

>    typeid运算符返回一个type_info对象。可以对两个typeid的返回值进行比较，以确定对象是否为特定的类型，而返回的type_info对象可用于获得关于对象的信息。

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

>    string实际上是模板具体化basic_string<char>的一个typedef，同时省略了与内存管理相关的参数

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