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
```

​	默认析构函数

​	复制构造函数

​	赋值运算符

​	地址运算符

# operator 重载运算符

```c++
operator typename();//类型转换
iostream& operator<<(iostream& _out,<object>& _name);//重载cout
fstream& operator<<(fstream& _out,<object>& _name);//重载ofstream
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

