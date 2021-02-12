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

**构造函数不能是虚函数，析构函数应当是虚函数**，除非类不用做基类

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

定义类模板

```c++
template<typename T>
//function
```

由于模板不是函数，不能单独编译。**模板必须与特定的模板实例化请求一起使用**