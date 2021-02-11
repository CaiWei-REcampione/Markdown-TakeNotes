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

acess

​	public

​	protected

​	private

特殊成员函数

​	默认构造函数

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

​	默认析构函数

*    构造函数中要么使用new[],要么使用new,而不能混用.
     *    如果**构造函数**使用的还是new[],则析构函数 应使用delete[]
     *    如果**构造函数**使用的是new,则析构函数应使用delete

​	复制构造函数

​	赋值运算符

​	地址运算符

## 派生类和基类之间的关系

派生类对象能使用基类的方法,条件是方法不是私有的

**基类指针可以在不进行显示类型转换的情况下指向派生类对象;基类引用可以在不进行显式类型转换的情况下引用派生类对象**

公有继承	public	

is-a关系(**建议**)

has-a关系

is-implemented-as-a关系

uses-a关系

**最好对类数据成员采用私有访问控制**，不要使用保护访问控制；同时通过基类方法使派生类能够访问基类数据

### 派生类使用new

为派生类定义显示析构函数、复制构造函数和赋值运算符

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

### ABC理念

在处理继承的问题上，在设计ABC之前，首先应**开发一个模型**，指出编程问题所需的类以及它们之间的相互关系。如果要设计类继承层次，则只能将那些不会用作基类的类设计为具体的类

可以将ABC看做是一种必须实施的接口，ABC要求不提派生类覆盖其纯虚函数，**迫使派生类遵循ABC设置的接口规则**，在这种情况下，使用ABC使得组件设计人员能够制定“接口约定”，确保从ABC派生出的所有组件都至少支持ABC指定的功能。

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

