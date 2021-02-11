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

