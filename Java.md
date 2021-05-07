# Java语言特点

*    简单
*    面向对象
*    分布式
*    结构中立
*    可移植
*    解释执行
*    健壮
*    安全
*    高性能
*    多线程
*    动态

# 安装运行环境

1.   下载Sun Java Development Kit运行环境
2.   配置环境变量
3.   项目打包成".jar"文件
4.   生成".bat"文件,输入以下代码

```
java -jar %1
```

5.   .jar文件设置打开方式，以bat方式打开
6.   Windows上就可以运行.jar文件

# 标识符

*    区分大小写: Myname与myname是两个不同的标识符
*    首字符,可以是下划线(_)或美元符或字母,但不能是数字
*    除首字符外其他字符,可以是下划线(_)、美元符、字母和数字
*    关键字不能作为标识符

# 关键字

## abstract

### 修饰类

abstract修饰类，这个类就是抽象类，抽象类中可以有非抽象变量和成员变量，也可以有普通方法、构造方法。但是不能实例化，只能被子类继承。
如果子类不是抽象类，则必须重写父类的抽象方法。

```java
public abstract class AbstractList<E> extends AbstractCollection<E> implements List<E> {
    ...
}
```

### 修饰方法

abstract修饰方法，这个方法就是抽象方法。抽象方法必须存在于抽象类中。抽象方法不能有具体实现。

```java
abstract public E get(int index);
```

## assert

```java
assert 表达式;// 表达式为真，程序继续执行；若表达式为假，则抛出一个AssertionError异常
assert 表达式:错误信息;// 使用assert时不能在表达式中完成任何程序实际所需的行为（只能做判断）。因为正常发布的代码都是断言无效的，即正常发布的代码中断言语句都不不执行的
```

## boolean

boolean是Java的基本类型之一（默认值false）。

只有两个值：true和false。

区别C的判断句，Java不能直接使用1和0来表示真假，且boolean类型也不能强转到其他基本类型。

```java
boolean a = true;
boolean b = false;
```

## break

### switch块

break在switch中用于跳出switch块，停止switch向下穿透的现象。

```
case value:expression;
    break;
```

### 循环

用于跳出循环

```java
while(...){
    ...
    break;
}
```

加标签形式

```jave
flag:
for(...){
    for(...){
        break flag;
    }
}
```

## byte

byte是Java的基本类型之一（默认值0）。表示8位有符号整数。

范围：-128~127

## case

case用于switch中，用于判断和执行语句。

```java
case 变量值:语句;
```

## catch

catch用于捕获异常。

在try/catch语句块中，catch捕获发生的异常，并应对错误做一些处理。
当catch捕获到异常后，try中执行的语句终止，并跳到catch后的语句中。

```java
catch(异常类型 异常){...}
```

## char

char是Java的基本类型之一（默认值\u000）。表示16位、在Unicode编码表中的字符。使用单引号来表示字符常量，例如’A’。

范围：0-65535

## class

class表示类。用于声明一个类。

```java
[访问控制] (abstract) class 类名 (implements){...}
```

## const

const是Java的一个保留关键字，没有实际意义，但是不能用于做变量名（因为被保留作为关键字了）。

## continue

continue用于在循环中跳过本次循环。

```java
while(...){
    ...
    continue;
}
```

在后面接标签，在一些嵌套比较复杂的循环中跳过一次循环。

```java
flag:
for(...){
    for(...){
        continue flag;
    }
}
```

## default

### switch

用于switch做默认分支

```java
default:语句；
```

### 接口

用于接口,让接口实现具体的方法

```java
public interface a{
    default void b(){
        具体方法;
    }
}
```

default用于接口时，必须要有具体实现。

## do

do用于和while组成循环，do/while循环不同于while循环，属于先执行循环体再判断。

```java
do{
	循环体;
}while(...)
```

## double

double是Java的基本类型之一（默认值0.0d），表示双精度、64位的浮点数。

## else

else用于分支结构中的判断。

```java
if(判断1){
    语句1;
}else if(判断2){
    语句2;
}else{
    语句3;
}
```

## enum

enum表示枚举，用于限制变量值的类型

枚举类中可以有成员变量和方法。

## extends

extends表示继承。

```java
class 子类 extends父类{}
```

## final

final修饰的变量即成为常量，只能赋值一次，但是final所修饰局部变量和成员变量有所不同。

### 变量

将变量变为常量，在初始化变量后不能再改变值。

01.	final修饰的局部变量必须使用之前被赋值一次才能使用。
02.	final修饰的成员变量在声明时没有赋值的叫“空白final变量”。空白final变量必须在构造方法或静态代码块中初始化。

### 方法

被final修饰的方法不能被子类重写。

final修饰的方法不能被子类覆盖。有时也是出于设计安全的目的，父类中的方法不想被别人覆盖，这是可以使用final关键字修饰父类中方法。

### 类

被final修饰的类不能被继承。

final修饰的类不能被继承。有时出于设计安全的目的，不想让自己编写的类被别人继承，这时可以使用final关键字修饰父类。

## finally

finally在try/catch语句块中处理一些后续的工作。例如关闭网络连接和输入输出流等。

如果在try/catch中使用return，则finally会撤销这个return，无论如何都会执行finally中的语句。

## float

float是Java的基本类型之一（默认值0.0f）。表示单精度、32位的浮点数。

## for

for用于循环

```java
for(初始化循环变量; 判断执行条件;更新循环变量){
    语句
}
for(变量:数组){
    语句
}
```

## goto

Java中的保留关键字，没有实际意义，但是不能用做变量名。在C中表示无条件跳转语句。

## if

if用于分支结构中的判断。常与else和else if使用。

```java
if(表达式){语句}
```

## implements

implements用于接入接口。接上接口的类必须实现接口的抽象方法（可以不实现默认方法和静态方法）。

```java
class A implements B{
    @Override
    do(){
        ...
    }
}
```

## import

用于导入包。

```java
import android.content.Intent;
```

## instanceof

instanceof用于判断类与对象的关系。

```java
a instanceof b// 若a是b的一个实例(或子类对象)，则整个表达式的结果是true，否则结果为false
```

## int

int是Java的基本类型之一（默认值为0）。表示32位、有符号的整数。

范围：[-231,231-1)

## interface

interface用于声明一个接口

## long

long是Java的基本类型之一（默认值为0L），表示64位、有符号的整数。

范围：[-263,263)

## native

native可以让Java运行非Java实现的方法。例如c语言，要编译后用javah产生一个.h文件。导入该.h文件并且实现native方法，编译成动态链接库文件。在Java加载动态链接库文件，这个native方法就可以在Java中使用了。

```java
public native void aVoid();
```

## new

new用于生成类的实例

```java
Object a = new Object()；
```

## package

package用于规定当前文件的包

## private

访问控制的一种。
私有的方法和变量只能在本类中访问。类和接口不能为私有。

## protected

访问控制的一种。
受保护的方法和变量只能给子类和基类访问。

## public

访问控制的一种。
公有的方法、类、变量、接口能够被任何其他类访问。

## return

方法中返回数据，并结束方法。

## strictfp

使用strictfp关键字来声明一个类、接口或者方法时，那么该类、接口或者方法会遵循IEEE-754标准来执行，提高浮点运算的精度，并且减少不同硬件平台之间由于浮点运算带来的差异。

## short

short是Java的基本类型之一（默认值0）,表示16位、有符号的整数。

范围：[-215,215)

## static

static修饰的语句块存放在堆的方法区中。

### 静态变量

依附在类中的变量，可以被类的所有的实例共用

### 静态方法

依附在类中的方法。静态方法只能访问类中的静态变量和静态方法。

### 静态块

在类加载的时候执行块中的语句，块中不能访问非静态变量

### 静态内部类

用static修饰内部类

## super

super即超类

引用父类的的成员

```java
super.xxx
```

变量或方法重名时用super调用父类的成员或方法。

调用父类的构造方法:

```java
super(xxx);
```

## switch

switch用于分支结构，判断某个变量与一系列值是否相等。switch 语句中的变量类型可以是： byte、short、int 、char、String、enum。

```java
switch(变量){
	case value1:语句1;
		break;
	case value2:语句2;
		break;
	...
	default:语句;
}
```

*    若变量和case后的值相等则执行语句。
*    当语句执行到break时跳到switch块后，如果没有break会产生穿透现象。
*    default分支必须为最后一个分支，在没有值和case变量相等时执行该语句。

## synchronized

synchronized关键字用于保证线程安全。由这个关键字修饰的方法或者代码块保证了同一时刻只有一个线程执行该代码。

```java
synchronized(obj){...}
```

当一个线程访问同步代码块时，检查obj是否有锁，如果有就挂起。如果没有就获得这个obj的锁，也就是把其他线程锁在了外面。当代码执行完毕时释放该锁，其他线程获得锁继续执行代码。

## this

*    指向当前对象：this.xxx
*    形参和成员名字重名时时用this区分。
*    引用构造函数。

## throw

用于抛出一个异常。

```java
throw (Exception);
```

## throws

在方法中将发生的异常抛出。

```java
[控制访问](返回类型)(方法名)([参数列表])[throws(异常类)]{...}
```

## transient

类接上序列化接口后，可以通过transient关键字将某些变量变得无法序列化。

## try

在try/catch中，将可能出现异常的语句放在try{}块中，出现异常之后代码将会终止并跳到catch中继续执行。

```java
try{
    ...
}catch(Exception e){
    ...
}finally{
    ...
}
```

## void

修饰方法，表示方法没有返回值。

## volatile

volatile关键字修饰的变量在多线程中保持同步。相比synchronized效率要高，不会阻塞线程。但只能保证数据的可见性，不能保证数据的原子性。例如在处理i++的时候另外一个线程修改i的值，那么i的值将会发生错误，这是原子性导致的。

## while

*    方法1

```java
while(判读语句){
    循环体...
}
```

*    方法2

```java
do{
	循环体...
}while(判读语句)
```

## 保留字

### goto

在其他语言中叫做“无限跳转”语句，在Java语言中不再使用goto语句，因为“无限跳转”语句会破坏程序结构。在Java语言中goto的替换语句可以通过break、continue和return实现“有限跳转”。

### const

在其他语言中是声明常量关键字，在Java语言中声明常量使用public static final 方式声明。

# 分隔符

在Java源代码中，有一些字符被用作分隔，称为分隔符。分隔符主要有：分号（;）、左右大括号（{}）和空白。

## 分号

分号是Java语言中最常用的分隔符，它表示一条语句的结束。

## 大括号

在Java语言中，以左右大括号（{}）括起来语句集合称为语句块（block）或复合语句，语句块中可以有0~n条语句。在定义类或方法时，语句块也被用做分隔类体或方法体。语句块也可以嵌套，且嵌套层次没有限制。

## 空白

在Java源代码中元素之间允许有空白，空白的数量不限。空白包括空格、制表符（Tab键输入）和换行符（Enter键输入），适当的空白可以改善对源代码可读性。

# 变量与常量

## 变量

变量和常量是构成表达式的重要部分，变量所代表的内部是可以被修改的。

```java
数据类型 变量名 [=初始值];
```

变量名要遵守用标识符命名规范，却在相关的作用域中不能有重复的变量名。变量作用域是变量的使用范围，在此范围内变量可以使用，超过作用域，变量内容则被释放，根据作用域不同分为：成员变量和局部变量

## 常量

常量事实上是那些内容不能被修改的变量，常量与变量类似也需要初始化，即在声明常量的同时要赋予一个初始值。常量一旦初始化就不可以被修改。

```java
final 数据类型 变量名 = 初始值;
```

final关键字表示最终的，它可以修改很多元素，修饰变量就变成了常量。

常量有三种类型：静态常量、成员常量和局部常量。

# 规范

## 命名

命名方法很多，但是比较有名的且被广泛接受的命名法包括下面两种。

### 匈牙利命名

一般只是命名变量，原则是：变量名 = 类型前缀 + 描述，如bFoo表示布尔类型变
量，pFoo表示指针类型变量。匈牙利命名还是有一定争议的，在Java编码规范中基本不被采用。

### 驼峰命名

又称“骆驼命名法”，是指混合使用大小写字母来命名。驼峰命名又分为小驼峰法和大驼峰法。小驼峰法就是第一个单词是全部小写，后面的单词首字母大写，如

除了包和常量外，Java编码规范命名方法采用驼峰法

*    包名：包名是全小写字母，中间可以由点分隔开。作为命名空间，包名应该具有唯一性，推荐采用公司或组织域名的倒置，如com.apple.quicktime.v2但Java核心库包名不采用域名的倒置命名，如java.awt.event。
*    类和接口名：采用大驼峰法，如SplitViewController。
*    文件名：采用大驼峰法，如BlockOperation.java。
*    变量：采用小驼峰法，如studentNumber。
*    常量名：全大写，如果是由多个单词构成，可以用下划线隔开，如YEAR和WEEK_OF_MONTH。
*    方法名：采用小驼峰法，如balanceAccount、isButtonPressed等。

## 注释规范

Java中注释的语法有三种：单行注释（//）、多行注释（/* ...*/）和文档注释（/**... */）。

### 文件注释

文件注释就是在每一个文件开头添加注释。文件注释通常包括如下信息：版权信息、文件名、所在模块、作者信息、历史版本信息、文件内容和作用等。

### 文档注释

文档注释就是指这种注释内容能够生成API帮助文档，JDK中javadoc命令能够提取这些注释信息并生成HTML文件。文档注释主要对类（或接口）、实例变量、静态变量、实例方法和静态方法等进行注释。

文档是要给别人看的帮助文档，一般注释的实例变量、静态变量、实例方法和静态方法都应该是非私有的，那些只给自己看的内容可以不用文档注释。

| 标签        | 描述                       |
| ----------- | -------------------------- |
| @auther     | 说明类或接口的作者         |
| @deprecated | 说明类、接口或成员已经废弃 |
| @param      | 说明方法参数               |
| @return     | 说明返回值                 |
| @see        | 参考另一个主题的链接       |
| @exception  | 说明方法所抛出的异常类     |
| @throws     | 同@exception标签           |
| @version    | 类或接口的版本             |

### 代码注释

程序代码中处理文档注释还需要在一些关键的地方添加代码注释，文档注释一般是给一些看不到源代码的人看的帮助文档，而代码注释是给阅读源代码的人参考的。代码注释一般是采用单行注释（//）和多行注释（/*... */）。

## 代码排版

### 空行

用以将逻辑相关的代码段分隔开，以提高可读性。

01.	类声明和接口声明之间保留两个空行。
02.	两个方法之间保留一个空行。
03.	方法的第一条语句之前保留一个空行。
04.	代码注释（尾端注释外）之前保留一个空行。
05.	一个方法内的两个逻辑段之间。

### 空格

1.   赋值符号“=”前后各有一个空格。
2.   所有的二元运算符都应该使用空格与操作数分开。
3.   一元操作符：负号“-”、自增“++”和自减“--”等，它们与操作数之间没有空格。
4.   小左括号“(”之后，小右括号“)”之前不应有空格。
5.   大左括号“{”之前有一个空格。
6.   方法参数列表小左括号“(”之前没有空格，小右括号“)”之后有一个空格，参数列表中参数逗号“,”之后也有一个空格。
7.   关键字之后紧跟着小左括号“(”，关键字之后应该有一个空格。

### 缩进

1.   在方法、Lambda、控制语句等包含大括号“{}”的代码块中，代码块的内容相对于首行缩进一个级别（4个空格）。
2.   如果是if语句中条件表达式的断行，那么新的一行应该相对于上一行缩进两个级别（8个空格），再往后的断行要与第一次的断行对齐。

### 断行

一行代码的长度应尽量不要超过80个字符

01.	在一个逗号后面断开。
02.	在一个操作符前面断开，要选择较高级别的运算符（而非较低级别的运算符）断开。
03.	新的一行应该相对于上一行缩进两个级别（8个空格）。

### 其他规范

1.   在声明变量或常量时推荐一行一个声明。
2.   左大括号“{”位于声明语句同行的末尾。右大括号“}”另起一行，与相应的声明语句对齐，除非是一个空语句，右大括号“}”应紧跟在左大括号“{”之后。
3.   每行至多包含一条语句。
4.   虽然Java语言允许if、for等控制语句只有一行代码情况下，省略左右两个大括号，但是编码规范并不推荐这样使用。

# 数据

## 数据类型

*    整数类型：byte、short、int和long
*    浮点类型：float和double
*    字符类型：char
*    布尔类型：boolean

### 整型类型

Java中整数类型包括：byte、short、int和long ，它们之间的区别仅仅是宽度和范围的不同。Java中整数都是有符号，与C不同没有无符号的整数类型。

Java的数据类型是跨平台的（与平台无关），无论你计算机是32位的还是64位的，byte类型整数都是一个字节（8位）。

| 整数类型 | 宽度   | 取值范围             |
| -------- | ------ | -------------------- |
| byte     | 8bits  | -128~127             |
| short    | 16bits | -$2^{15}$~$2^{15}-1$ |
| int      | 32bits | -$2^{31}$~$2^{31}-1$ |
| long     | 64bits | -$2^{63}$~$2^{63}-1$ |

### 浮点类型

浮点类型主要用来储存小数数值，也可以用来储存范围较大的整数。它分为浮点数（float）和双精度浮点数（double）两种，双精度浮点数所使用的内存空间比浮点数多

| 浮点类型 | 宽度   |
| -------- | ------ |
| float    | 32bits |
| double   | 64bits |

### 数字表示方式

*    二进制数：以 0b 或0B为前缀，注意0是阿拉伯数字，不要误认为是英文字母o。
*    八进制数：以0为前缀，注意0是阿拉伯数字。
*    十六进制数：以 0x 或0X为前缀，注意0是阿拉伯数字。
*    指数表示：进行数学计算时往往会用到指数表示的数值。如果采用十进制表示指数，需要使用大写或小写的e表示幂，e2表示${10}^2$。

### 字符类型

字符类型表示单个字符，Java中char声明字符类型，Java中的字符常量必须用单引号括起来的单个字符

Java字符采用双字节Unicode编码，占两个字节（16位），因而可用十六进制（无符号的）编码形式表示，它们的表现形式是\un，其中n为16位十六进制数，所以'A'字符也可以用Unicode编码'\u0041'表示

### 转义符

| 字符表示 | Unicode编码 | 说明          |
| -------- | ----------- | ------------- |
| \t       | \u0009      | 水平制表符TAB |
| \n       | \u000a      | 换行          |
| \r       | \u000d      | 回车          |
| \\"      | \u0022      | 双引号        |
| \\'      | \u0027      | 单引号        |
| \\\\     | \u005c      | 反斜线        |

### 布尔类型

在Java语言中声明布尔类型的关键字是boolean，它只有两个值：true和false。

提示　在C语言中布尔类型是数值类型，它有两个取值：1和0。而在Java中的布尔类型取值不能用1和0替代，也不属于数值类型，不能与int等数值类型之间进行数学计算或类型转化。

### 数值类型相互转换

#### 自动类型转换

char类型比较特殊，char自动转换为int、long、float和double，但byte和short不能自动转换为char，而且char也不能自动转换为byte或short。

| 操作数1类型                         | 操作数2类型 | 转换后的类型 |
| ----------------------------------- | ----------- | ------------ |
| byte、short、char                   | int         | int          |
| byte、short、char、int              | long        | long         |
| byte、short、char、int、long        | float       | float        |
| byte、short、char、int、long、float | double      | double       |

#### 强制类型转换

在数值类型转换过程中，除了需要自动类型转换外，有时还需要强制类型转换，强制类型转换是在变量或常量之前加上“(目标类型)”实现。

```java
[typename] name = ([typename]) object;
```

当大宽度数值转换为小宽度数值时，大宽度数值的高位被截掉，这样就会导致数据精度丢失。除非大宽度数值的高位没
有数据，就是这个数比较小的情况

### 引用数据类型

在Java中除了8种基本数据类型外，其他数据类型全部都是引用（reference）数据类型

包含：类、接口和数组声明的数据类型

Java中的引用数据类型，相当于C等语言中指针（pointer）类型，引用事实上就是指针，是指向一个对象的内存地址。引用数据类型变量中保持的是指向对象的内存地址。

## 数据结构

### 数组

#### 基本特性

01.	一致性：数组只能保存相同数据类型元素，元素的数据类型可以是任何相同的数据类型。
02.	有序性：数组中的元素是有序的，通过下标访问。
03.	不可变性：数组一旦初始化，则长度（数组中元素的个数）不可变。

在Java中数组的下标是从零开始的，事实上很多计算机语言的数组下标从零开始的。Java数组下标访问运算符是中括号

ava中的数组本身是引用数据类型，它的长度属性是length。数组可以分为：一维数组和多维数组

#### 一维数组

##### 一维数组声明

数组的声明就宣告这个数组中元素类型，数组的变量名。

```java
元素数据类型[]数据变量名；
元素数据类型 数组变量名[];
```

可见数组的声明有两种形式：一种是两个中括号（[]）跟在元素数据类型之后；另一种是两个中括号（[]）跟在变量名之后。

##### 数组初始化

声明完成就要对数组进行初始化，数组初始化的过程就是为数组每一个元素分配内存空间，并为每一个元素提供初始值。初始化之后数组的长度就确定下来不能再变化了。

数组初始化可以分为静态初始化和动态初始化。

###### 静态初始化

静态初始化就是将数组的元素放到大括号中，元素之间用逗号（,）分隔。

###### 动态初始化

动态初始化使用new运算符分配指定长度的内存空间

```java
new 元素数据类型[数组长度];
```

new分配数组内存空间后，数组中的元素内容是数组类型的默认值

| 基本类型 | 默认值    |
| -------- | --------- |
| byte     | 0         |
| short    | 0         |
| int      | 0         |
| long     | 0L        |
| float    | 0.0f      |
| double   | 0.0d      |
| char     | '\\u0000' |
| boolean  | false     |
| 引用     | null      |

#### 多维数组

当数组中每个元素又可以带有多个下标时，这种数组就是“多维数组”。

##### 二维数组声明

```cpp
元素数据类型[][] 数组变量名;
元素数据类型 数组变量名[][];
元素数据类型[] 数组变量名[];
```

##### 二维数组的初始化

###### 静态初始化

```java
元素数据类型 数组名称 [][]={{...},{...},...};
```

###### 动态初始化

```java
new 元素数据类型[高维数组长度][低维数组长度];
```

高维数组就是最外面的数组，低维数组是每一个元素的数组。

#### 不规则数组

先初始化高维数组，然后再分别逐个初始化低维数组。

>    下标越界异常（ArrayIndexOutOfBoundsException）是试图访问不存在的下标时引发的。例如一个一维array数组如果有10个元素，那么表达式array[10]就会发生下标越界异常，这是因为数组下标是从0开始的，最后一个元素下标是数组长度减1，所以array[10]访问的元素是不存在的。

不规则数组访问和遍历可以使用for和for-each循环，但要注意下标越界异常发生。

### 字符串

Java SE提供了三个字符串类：String、StringBuffer和StringBuilder。

String是不可变字符串， StringBuffer和StringBuilder是可变字符串。

空字符串不是null，空字符串是分配内存空间，而null是没有分配内存空间。

#### 不可变字符串

##### String

Java中不可变字符串类是String，属于java.lang包，它也是Java非常重要的类。

###### 构造方法

*    String()：使用空字符串创建并初始化一个新的String对象。
*    String(String original)：使用另外一个字符串创建并初始化一个新的 String 对象。
*    String(StringBuffer buffer)：使用可变字符串对象（StringBuffer）创建并初始化一个新的 String对象。
*    String(StringBuilder builder)：使用可变字符串对象（StringBuilder）创建并初始化一个新的String 对象。
*    String(byte[] bytes)：使用平台的默认字符集解码指定的byte数组，通过byte数组创建并初始化一个新的 String 对象。
*    String(char[] value)：通过字符数组创建并初始化一个新的 String 对象。
*    String(char[] value, int offset, int count)：通过字符数组的子数组创建并初始化一个新的 String 对象；offset参数是子数组第一个字符的索引，count参数指定子数组的长度。

##### 字符串池

==运算符比较的是两个引用是否指向相同的对象

Java中的不可变字符串String常量，采用字符串池（String Pool）管理技术，字符串池是一种字符串驻留技术。

##### 去前后空格

*    String trim()：去前后空格，返回String

##### 字符串拼接

String字符串虽然是不可变字符串，但也可以进行拼接只是会产生一个新的对象。

String字符串拼接可以使用+运算符或String的concat(String str)方法。+运算符优势是可以连接任何类型数据拼接成为字符串，而concat方法只能拼接String类型字符串。

##### 字符串查找

在给定的字符串中查找字符或字符串是比较常见的操作。在String类中提供了indexOf和lastIndexOf方法用于查找字符或字符串，返回值是查找的字符或字符串所在的位置，-1表示没有找到。

*    int indexOf(char ch)：从前往后搜索字符ch，返回第一次找到字符ch所在处的索引。
*    int indexOf(char ch, int fromIndex)：从指定的索引开始从前往后搜索字符ch，返回第一次找到字符ch所在处的索引。
*    int indexOf(String str)：从前往后搜索字符串str，返回第一次找到字符串所在处的索引。
*    int indexOf(String str, int fromIndex)：从指定的索引开始从前往后搜索字符串str，返回第一次找到字符串所在处的索引。
*    int lastIndexOf(char ch)：从后往前搜索字符ch，返回第一次找到字符ch所在处的索引。
*    int lastIndexOf(char ch, int fromIndex)：从指定的索引开始从后往前搜索字符ch，返回第一次找到字符ch所在处的索引。
*    int lastIndexOf(String str)：从后往前搜索字符串str，返回第一次找到字符串所在处的索引。
*    int lastIndexOf(String str, int fromIndex)：从指定的索引开始从后往前搜索字符串str，返回第一次找到字符串所在处的索引。

##### 字符串比较

###### 比较相等

*    boolean equals(Object anObject)：比较两个字符串中内容是否相等。
*    boolean equalsIgnoreCase(String anotherString)：类似equals方法，只是忽略大小写。

###### 比较大小

*    int compareTo(String anotherString)：按字典顺序比较两个字符串。如果参数字符串等于此字符串，则返回值 0；如果此字符串小于字符串参数，则返回一个小于 0 的值；如果此字符串大于字符串参数，则返回一个大于 0 的值。
*    int compareToIgnoreCase(String str)：类似compareTo，只是忽略大小写。

###### 比较前缀和后缀

*    boolean endsWith(String suffix)：测试此字符串是否以指定的后缀结束。 如果字符串以指定的前缀开始，则返回 true；否则返回 false。
*    boolean startsWith(String prefix)：测试此字符串是否以指定的前缀开始。如果字符串以指定的前缀开始，则返回 true；否则返回 false。

###### 字符串截取

*    String substring(int beginIndex)：从指定索引beginIndex开始截取一直到字符串结束的子字符串。
*    String substring(int beginIndex, int endIndex)：从指定索引beginIndex开始截取直到索引endIndex -1处的字符，注意包括索引为beginIndex处的字符，但不包括索引为endIndex处的字符。
*    String[] split(String regex)：根据给定正则表达式的匹配拆分此字符串。该方法的作用就像是使用给定的表达式和限制参数 0 来调用两参数 split方法。所得数组中不包括结尾空字符串。

#### 可变字符串

可变字符串在追加、删除、修改、插入和拼接等操作不会产生新的对象。

##### StringBuffer和StringBuilder

Java提供了两个可变字符串类StringBuffer和StringBuilder，中文翻译为“字符串缓冲区”。

StringBuffer是线程安全的，它的方法是支持线程同步 ，线程同步会操作串行顺序执行，在单线程环境
下会影响效率。StringBuilder是StringBuffer单线程版本，Java 5之后发布的，它不是线程安全的，但它的执行效率很高。

>    线程同步是一个多线程概念，就是当多个线程访问一个方法时，只能由一个优先级别高的线程先访问，在访问期间会锁定该方法，其他线程只能等到它访问完成释放锁，才能访问。

StringBuffer和StringBuilder具有完全相同的API，即构造方法和普通方法等内容一样。

###### 构造方法

*    StringBuilder()：创建字符串内容是空的StringBuilder对象，初始容量默认为16个字符。
*    StringBuilder(CharSequence seq)：指定CharSequence字符串创建StringBuilder对象。CharSequence接口类型，它的实现类有：String、StringBuffer、StringBuilder等，所以参数seq可以是String、 StringBuffer和StringBuilder等类型。
*    StringBuilder(int capacity)：创建字符串内容是空的StringBuilder对象，初始容量由参数capacity指定的。
*    StringBuilder(String str)：指定String字符串创建StringBuilder对象。

>    字符串长度和字符串缓冲区容量区别。字符串长度是指在字符串缓冲区中目前所包含字符串长度，通过length()获得；字符串缓冲区容量是缓冲区中所能容纳的最大字符数，通过capacity()获得。当所容纳的字符超过这个长度时，字符串缓冲区自动扩充容量，但这是以牺牲性能为代价的扩容。

###### 字符串追加

*    append()：StringBuilder的追加法与StringBuffer完全一样。

###### 插入

*    StringBuilder insert(int offset, String str)：在字符串缓冲区中索引为offset的字符位置之前插入str， insert有很多重载方法，可以插入任何类型数据。

###### 删除

*    StringBuffer delete(int start, int end)：在字符串缓冲区中删除子字符串，要删除的子字符串从指定索引start开始直到索引end - 1处的字符。start和end两个参数与substring(int beginIndex, int endIndex)方法中的两个参数含义一样。

###### 替换

*    StringBuffer replace(int start, int end, String str)字符串缓冲区中用str替换子字符串，子字符串从指定索引start开始直到索引end - 1处的字符。start和end同delete(int start, int end)方法。

###### StringBuilder转String

*    StringBuilder toString()：StringBuilder转String

### List集合

*    List接口继承自Collection接口，List接口中的很多方法都继承自Collection接口的。
*    List接口的实现类有：ArrayList 和 LinkedList。ArrayList是基于动态数组数据结构的实现，LinkedList是基于链表数据结构的实现。ArrayList访问元素速度优于LinkedList，LinkedList占用的内存空间比较大，但LinkedList在批量插入或删除数据时优于ArrayList。

```java
List list=new ArrayList();			// ArrayList
List list=new LinkedList();			// LinkedList
```

#### 操作元素

*    get(int index)：返回List集合中指定位置的元素。
*    set(int index, Object element)：用指定元素替换List集合中指定位置的元素。
*    add(Object element)：在List集合的尾部添加指定的元素。该方法是从Collection集合继承过来的。
*    add(int index, Object element)：在List集合的指定位置插入指定元素。
*    remove(int index)：移除List集合中指定位置的元素。
*    remove(Object element)：如果List集合中存在指定元素，则从List集合中移除第一次出现的指定元素。该方法是从Collection集合继承过来的。
*    clear()：从List集合中移除所有元素。该方法是从Collection集合继承过来的。

#### 判断元素

*    isEmpty()：判断List集合中是否有元素，没有返回true，有返回false。该方法是从Collection集合继承过来的。
*    contains(Object element)：判断List集合中是否包含指定元素，包含返回true，不包含返回false。该方法是从Collection集合继承过来的。

#### 查询元素

*    indexOf(Object o)：从前往后查找List集合元素，返回第一次出现指定元素的索引，如果此列表不包含该元素，则返回-1。
*    lastIndexOf(Object o)：从后往前查找List集合元素，返回第一次出现指定元素的索引，如果此列表不包含该元素，则返回-1。

#### 迭代器

*    iterator()：返回迭代器（Iterator）对象，迭代器对象用于遍历集合。该方法是从Collection集合继承过来的。

#### 元素数

*    size()：返回List集合中的元素数，返回值是int类型。该方法是从Collection集合继承过来的。

#### 子集合

*    subList(int fromIndex, int toIndex)：返回List集合中指定的 fromIndex（包括 ）和toIndex（不包括）之间的元素集合，返回值为List集合。

#### 遍历集合

##### 方法

*    使用for循环遍历：List集合可以使用for循环进行遍历，for循环中有循环变量，通过循环变量可以访问List集合中的元素。
*    使用for-each循环遍历：for-each循环是针对遍历各种类型集合而推出的，笔者推荐使用这种遍历方法。
*    使用迭代器遍历：Java提供了多种迭代器，List集合可以使用Iterator和ListIterator迭代器。

```java
for(Object item:list){
    type name=(type)item;
}
```

```java
Iterator pos = list.iterator();
while (pos.hasNext()) {

    type item = (type) pos.next();
    System.out.println(item);
}
```

### Set集合

>    List集合中的元素是有序的、可重复的，而Set集合中的元素是无序的、不能重复的。List集合强调的是有序，Set集合强调的是不重复。当不考虑顺序，且没有重复元素时，Set集合和List集合可以互相替换的。

*    Set接口也继承自Collection接口，Set接口中大部分都是继承自Collection接口。
*    Set接口直接实现类主要是HashSet，HashSet是基于散列表数据结构的实现。

```java
Set set=new HashSet();
```

#### 操作元素

*    add(Object element)：在Set集合的尾部添加指定的元素。该方法是从Collection集合继承过来的。
*    remove(Object element)：如果Set集合中存在指定元素，则从Set集合中移除该元素。该方法是从Collection集合继承过来的。
*    clear()：从Set集合中移除所有元素。该方法是从Collection集合继承过来的。

#### 判断元素

*    isEmpty()：判断Set集合中是否有元素，没有返回true，有返回false。该方法是从Collection集合继承过来的。
*    contains(Object element)：判断Set集合中是否包含指定元素，包含返回true，不包含返回false。该方法是从Collection集合继承过来的。

#### 迭代器

*    iterator()：返回迭代器（Iterator）对象，迭代器对象用于遍历集合。该方法是从Collection集合继承过来的。

#### 元素数

*    size()：返回Set集合中的元素数，返回值是int类型。该方法是从Collection集合继承过来的。

#### 遍历

*    Set集合中的元素由于没有序号，所以不能使用for循环进行遍历，但可以使用for-each循环和迭代器进行遍历。

```java
for(Object item:list){
    type name=(type)item;
}
```

```java
Iterator pos = list.iterator();
while (pos.hasNext()) {

    type item = (type) pos.next();
    System.out.println(item);
}
```

### Map集合

*    Map（映射）集合表示一种非常复杂的集合，允许按照某个键来访问元素。
*    Map集合是由两个集合构成的，一个是键（key）集合，一个是值（value）集合。
*    键集合是Set类型，因此不能有重复的元素。而值集合是Collection类型，可以有重复的元素。Map集合中的键和值是成对出现的。
*    Map接口直接实现类主要是HashMap，HashMap是基于散列表数据结构的实现。

#### 操作元素

*    get(Object key)：返回指定键所对应的值；如果Map集合中不包含该键值对，则返回null。
*    put(Object key, Object value)：指定键值对添加到集合中。
*    remove(Object key)：移除键值对。
*    clear()：移除Map集合中所有键值对。

#### 判断元素

*    isEmpty()：判断Map集合中是否有键值对，没有返回true，有返回false。
*    containsKey(Object key)：判断键集合中是否包含指定元素，包含返回true，不包含返回false。
*    containsValue(Object value)：判断值集合中是否包含指定元素，包含返回true，不包含返回false。

#### 查看集合

*    keySet()：返回Map中的所有键集合，返回值是Set类型。
*    values()：返回Map中的所有值集合，返回值是Collection类型。
*    size()：返回Map集合中键值对数。

#### 遍历

*    Map集合遍历与List和Set集合不同，Map有两个集合，因此遍历时可以只遍历值的集合，也可以只遍历键的集合，也可以同时遍历。这些遍历过程都可以使用for-each循环和迭代器进行遍历。

```java
Iterator pos=map.entrySet().iterator();
while(pos.hasNext()){
    
    Map.Entry entry=(Map.Entry)pos.next();
    
    type key= (type) entry.getKey();
    type value=(type)entry.getValue();
    
    // TODO:System.out.println(key+":"+value);
}
```

```java
for(Object item:map.entrySet()){

    Map.Entry entry=(Map.Entry)item;
    int key= (int) entry.getKey();
    String value=(String)entry.getValue();
    System.out.println(key+":"+value);
}
```

# 运算符

## 算术运算符

### 一元运算符

| 运算符 | 名称     | 说明                         | 例子        |
| ------ | -------- | ---------------------------- | ----------- |
| -      | 取反符号 | 取反运算                     | b = -a      |
| ++     | 自加一   | 先取值再加一，或先加一再取值 | a++或++a    |
| - -    | 自减一   | 先取值再减一，或先减一再取值 | a- -或- - a |

### 二元运算符

| 运算符 | 名称 | 说明                                               | 例子 |
| ------ | ---- | -------------------------------------------------- | ---- |
| +      | 加   | 求a加b的和，还可用于String类型，进行字符串连接操作 | a+b  |
| -      | 减   | 求a减b的差                                         | a-b  |
| **     | 乘   | 求a乘以b的积                                       | a*b  |
| /      | 除   | 求a除以b的商                                       | a/b  |
| %      | 取余 | 求a除以b的余数                                     | a%b  |

## 算术赋值运算符

| 运算符 | 名称     | 例子         |
| ------ | -------- | ------------ |
| +=     | 加赋值   | a+=b、a+=b+3 |
| -=     | 减赋值   | a-=b         |
| *=     | 乘赋值   | a*=b         |
| /=     | 除赋值   | a/=b         |
| %=     | 取余赋值 | a%=b         |

## 关系运算符

| 运算符 | 名称     | 说明                                | 例子   |
| ------ | -------- | ----------------------------------- | ------ |
| ==     | 等于     | a等于b时返回true，否则返回false     | a == b |
| !=     | 不等于   | 与==相反                            | a != b |
| >      | 大于     | a大于b时返回true，否则返回false     | a > b  |
| <      | 小于     | a小于b时返回true，否则返回false     | a < b  |
| >=     | 大于等于 | a大于等于b时返回true，否则返回false | a >= b |
| <=     | 小于等于 | a小于等于b时返回true，否则返回false | a <= b |

## 逻辑运算符

| 运算符 | 名称   | 说明                                                         |        |
| ------ | ------ | ------------------------------------------------------------ | ------ |
| !      | 逻辑非 | a为true时,值为false , a为false时,值为true                    | !a     |
| &      | 逻辑与 | ab全为true时,计算结果为true,否则为false                      | a&b    |
| \|     | 逻辑或 | ab全为false时,计算结果为false ,否则为true                    | a\|b   |
| &&     | 短路与 | ab全为true时，计算结果为true，否则为false。&&与&区别：如果a为false，则不计算b | a&&b   |
| \|\|   | 短路或 | ab全为false时，计算结果为false，否则为true。\|\|与\|区别：如果a为true，则不计算b | a\|\|b |

## 位运算符

| 运算符 | 名称       | 例子   | 说明                         |
| ------ | ---------- | ------ | ---------------------------- |
| ~      | 位反       | ~x     | 将x的值按位取反              |
| &      | 位与       | x&y    | x与y位进行位与运算           |
| \|     | 位或       | x\|y   | x与y位进行位或运算           |
| ^      | 位异或     | x^a    | x与y位进行位异或运算         |
| >>     | 有符号右移 | x>>a   | x右移a位，高位采用符号位补位 |
| <<     | 左移       | x<<a   | x左移a位，低位用0补位        |
| >>>    | 无符号右移 | a>>>b  | x右移a位，高位用0补位        |
| &=     | 位与等于   | a&=b   | 等价于a=a&b                  |
| \|=    | 位或等于   | a\|=b  | 等价于a=a\|b                 |
| ^=     | 位异或等于 | a^=b   | 等价于a=a^b                  |
| <<=    | 左移等于   | a<<=b  | 等价于a=a<<b                 |
| >>=    | 右移等于   | a>>=b  | 等价于a=a>>b                 |
| >>>=   | 右移等于   | a>>>=b | 等价于a=a>>>b                |

## 其他运算符

*    三元运算符（? :）。例如x?y:z;，其中x、y和z都为表达式。
*    小括号。起到改变表达式运算顺序的作用，它的优先级最高。
*    中括号。数组下标。
*    引用号（.）。对象调用实例变量或实例方法的操作符，也是类调用静态变量或静态方法的操作符。
*    赋值号（=）。赋值是用等号运算符（=）进行的。
*    instanceof。判断某个对象是否为属于某个类。
*    new。对象内存分配运算符。
*    箭头（->）。Java 8新增加的，用来声明Lambda表达式。
*    双冒号（::）。Java 8新增加的，用于Lambda表达式中方法的引用。

# 控制语句

## 分支语句

### if-else if-else语句

```java
if(条件表达式){
	// TODO
}else if(条件表达式2){
	// TODO
}else{
	// TODO
}
```

### switch语句

```java
switch(表达式){
    case value1:
        // TODO
    case value2:
        // TODO
    default:
        // TODO
}
```

## 循环语句

### while语句

```java
while(循环条件){
    // TODO
}
```

### do-while语句

```java
do{
    // TODO
}while(循环条件);
```

### for语句

```java
for(初始化;循环条件;迭代){
    // TODO
}
```

### for-each语句

*    遍历集合

```java
for([typename] item: [container]){
    // TODO
}
```

## 跳转语句

### break语句

break语句可用于上一节介绍的while、repeat-while和for循环结构，它的作用是强行退出循环体，不再执行循环体中剩余的语句。

```java
break;			// 不带标签
break label;	// 带标签
```

### continue语句

continue语句用来结束本次循环，跳过循环体中尚未执行的语句，接着进行终止条件的判断，以决定是否继续循环。对于for语句，在进行终止条件的判断前，还要先执行迭代语句。

```java
continue;			// 不带标签
continue label;		// 带标签
```

# 面向对象

面向对象的编程思想：按照真实世界客观事物的自然规律进行分析，客观世界中存在什么样的实体，构建的软件系统就存在什么样的实体。

## 面向对象三个基本特性

面向对象思想有三个基本特性：封装性、继承性和多态性。

### 封装性

封装能够使外部访问者不能随意存取对象的内部数据，隐藏了对象的内部细节，只保留有限的对外接口。

外部访问者不用关心对象的内部细节，使得操作对象变得简单。

### 继承性

在Java语言中一般类称为“父类”，特殊类称为“子类”。

Java语言是单继承的，即只能有一个父类，但Java可以实现多个接口，可以防止多继承所引起的冲突问题。

### 多态性

多态性是指在父类中成员变量和成员方法被子类继承之后，可以具有不同的状态或表现行为。

## 类

类是Java中的一种重要的引用数据类型，是组成Java程序的基本要素。它封装了一类对象的数据和操作。

### 类声明

Java语言中一个类的实现包括：类声明和类体。

```java
[public][abstract|final] class className [extends superclassName][implements interfaceNameList]{
    // TODO
}
```

*    class是声明类的关键字
*    className是自定义的类名
*    class前面的修饰符public、abstract、final用来声明类，它们可以省略
*    superclassName为父类名，可以省略，如果省略则该类继承Object类，Object类所有类的根类，所有类都直接或间接继承Object
*    interfaceNameList是该类实现的接口列表，可以省略，接口列表中的多个接口之间用逗号分隔。

### 成员变量

```java
class className{
    [public|protected|private][static][final] type variableName;// 成员变量
}
```

其中type是成员变量数据类型，variableName是成员变量名。type前的关键字都是成员变量修饰符

*    public、protected和private修饰符用于封装成员变量。
*    static修饰符用于声明静态变量，所以静态变量也称为“类变量”。
*    final修饰符用于声明变量，该变量不能被修改。

### 成员方法

```java
class className{
     [public | protected | private ] [static] [final | abstract] [native] [synchronized] type methodname([paramList])[throws exceptionList]{
         // TODO
     }
}
```

其中type是方法返回值数据类型，methodName是方法名。type前的关键字都是方法修饰符

*    public、protected和private修饰符用于封装方法。
*    static修饰符用于声明静态方法，所以静态方法也称为“类方法”。
*    final | abstract不能同时修饰方法，final修饰的方法不能在子类中被覆盖；abstract用来修饰抽象方法，抽象方法必须在子类中被实现。
*    native修饰的方法，称为“本地方法”，本地方法调用平台本地代码（如：C或C++编写的代码），不能实现跨平台。
*    synchronized修饰的方法是同步的，当多线程方式同步方法时，只能串行地执行，保证是线程安全的。

### 包

#### 包作用

在Java中为了防止类、接口、枚举和注释等命名冲突引用了包（package）概念，包本质上命名空间（namespace）。

在包中可以定义一组相关的类型（类、接口、枚举和注释），并为它们提供访问保护和命名空间管理。

命名空间，也称名字空间、名称空间等，它表示着一个标识符（identifier）的可见范围。一个标识符可在多个命名空间中定义，它在不同命名空间中的含义是互不相干的。这样，在一个新的命名空间中可定义任何标识符，它们不会与任何已有的标识符发生冲突，因为已有的定义都处于其他命名空间中。

#### 包定义

Java中使用package语句定义包，package语句应该放在源文件的第一行，在每个源文件中只能有一个包定义语句，并且package语句适用于所有类型（类、接口、枚举和注释）的文件。

```java
package pkg1[.pkg2[.pkg3...]];
```

pkg1~ pkg3都是组成包名一部分，之间用点（.）连接，它们命名应该是合法的标识符，其次应该遵守Java包命名规范，即全部小写字母。

包名一般是公司域名的倒置。

如果在源文件中没有定义包，那么类、接口、枚举和注释类型文件将会被放进一个无名的包中，也称为默认包。

#### 包引入

为了能够使用一个包中类型（类、接口、枚举和注释），需要在Java程序中明确引入该包。使用import语句实现引入包，import语句应位于package语句之后，所有类的定义之前，可以有0~n条import语句。

```java
 import package1[.package2…].(类型名|*);
```

“包名.类型名”形式只引入具体类型，“包名.*”采用通配符，表示引入这个包下所有的类型。但从编程规范的角度提倡明确引入类型名，即“包名.类型名”形式可以提高程序的可读性。

当前源文件与要使用的类型（类、接口、枚举和注释）在同一个包中，可以不用引入包。

#### 常用包

##### java.lang包

*    java.lang包含中包含了Java语言的核心类，如Object、Class、String、包装类和Math等，还有包装类Boolean、Character、Integer、Long、Float和Double。使用java.lang包中的类型，不需要显示使用import语句引入，它是由解释器自动引入。

##### java.io包

*    java.io包含中提供多种输入/输出流类，如InputStream、OutputStream、Reader和Writer。还有文件管理相关类和接口，如File和FileDescriptor类以及FileFilter接口。

##### java.net包

*    java.net包含进行网络相关的操作的类，如URL、Socket和ServerSocket等。

##### java.util包

*    java.util包含一些实用工具类和接口，如集合、日期和日历相关类和接口。

##### java.text包

*    java.text包中提供文本处理、日期式化和数字格式化等相关类和接口。

##### java.awt和javax.swing包

*    java.awt和javax.swing包提供了Java图形用户界面开发所需要的各种类和接口。java.awt提供是一些基础类和接口，javax.swing提供了一些高级组件。

### 抽象类与接口

设计良好的软件系统应该具备“可复用性”和“可扩展性”，能够满足用户需求的不断变更。使用抽象类和接口是实现“可复用性”和“可扩展性”重要的设计手段。

#### 抽象类

##### 抽象类声明和实现

在Java中抽象类和抽象方法的修饰符是abstract

```java
public abstract class name{
    
    // TODO
}
```

-    如果一个方法被声明为抽象的，那么这个类也必须声明为抽象的。而一个抽象类中，可以有0~n个抽象方法，以及0~n具体方法。
-    设计抽象方法目的就是让子类来实现的，否则抽象方法就没有任何意义(override重写)
-    抽象类不能被实例化,只有具体类才能被实例化。

#### 使用接口

-    比抽象类更加抽象的是接口，在接口中所有的方法都是抽象的。
-    接口可以有成员变量。

##### 接口声明和实现

-    在Java中接口的声明使用的关键字是interface

```java
public interface name{
    // 接口中静态成员变量，省略public static final
    // 接口中函数，省略public
}
```

-    某个类实现接口时，要在声明时使用implements关键字，当实现多个接口之间用逗号（,）分隔。实现接口时要实现接口中声明的所有方法。

```java
public class name implements interfacename{
    
    // override
}
```

##### 接口与多继承

-    在Java中只允许继承一个类，但可实现多个接口。通过实现多个接口方式满足多继承的设计需求。如果多个接口中即便有相同方法，它们也都是抽象的，子类实现它们不会有冲突。

```java
public interface InterfaceA {
    // TODO
}

public interface InterfaceB{
    // TODO
}

public class name implements InterfaceA,InterfaceB{
    // TODO
}
```

###### 接口继承

-    Java语言中允许接口和接口之间继承。由于接口中的方法都是抽象方法，所以继承之后也不需要做什么，因此接口之间的继承要比类之间的继承简单的多。

```java
public interface InterfaceA {
    // TODO
}

public interface InterfaceB extends InterfaceA{
    // TODO
}

public class name implements InterfaceB{
    // TODO
}
```

##### 默认方法和静态方法

###### java 8之前的特性

*    不能可选实现方法，接口的方法全部是抽象的，实现接口时必须全部实现接口中方法，哪怕是有些方法并不需要，也必须实现。
02.	没有静态方法。

###### Java 8新特性默认方法和静态方法

02.	接口中的默认方法类似于类中具体方法，给出了具体实现，只是方法修饰符是default。接口中静态方法类似于类中静态方法。

```java
public interface InterfaceA{
    
    // 默认方法
    default type name(){
        
        // TODO
    }
    
    // 静态方法
    static type name1(){
        
        // TODO
    }
}
```

02.	默认方法可以根据需要有选择实现（覆盖）。
02.	静态方法不需要实现，实现类中不能拥有接口中的静态方法。

#### 抽象类与接口区别

*    接口支持多继承，而抽象类（包括具体类）只能继承一个父类。
*    接口中不能有实例成员变量，接口所声明的成员变量全部是静态常量，即便是变量不加public static final修饰符也是静态常量。抽象类与普通类一样各种形式的成员变量都可以声明。
*    接口中没有包含构造方法，由于没有实例成员变量，也就不需要构造方法了。抽象类中可以有实例成员变量，也需要构造方法。
*    抽象类中可以声明抽象方法和具体方法。Java 8之前接口中只有抽象方法，而Java 8之后接口中也可以声明具体方法，具体方法通过声明默认方法实现。

### 枚举类

#### 特性

-    Java枚举类型本质上是一种继承java.lang.Enum类，是引用数据类型，因此也称为“枚举类”。
-    Java枚举类型是一种类，是引用类型，具有了面向对象特性，可以添加方法和成员变量等。
02.	Java枚举类型父类是java.lang.Enum，不需要显式声明。
03.	Java枚举类型可以实现接口，与类实现接口类似。
04.	Java枚举类型不能被继承，不存在子类。

#### 声明和定义

```java
public enum name{
    // 枚举常量表
    // MONDAY("星期一",0),TUESDAY("星期二",1),...
    
    // 实例变量
    [public|private|protected] type param_name;
    
    // 静态变量
    [public|private|protected] static type param_name;
    
    // 构造方法
    [public|private|protected] name(type param_name){
        
        // TODO
    }
    
    @Override
    public String toString(){
        
        // TODO
    }
}
```

#### 枚举方法

所有枚举类都继承java.lang.Enum类，Enum中定义了一些枚举中常用的方法：

*    int ordinal()：返回枚举常量的顺序。这个顺序根据枚举常量声明的顺序而定，顺序从零开始。
*    枚举类型[] values()：静态方法，返回一个包含全部枚举常量的数组。
*    枚举类型 valueOf(String str)：静态方法，str是枚举常量对应的字符串，返回一个包含枚举类型实例。

### Java常用类

#### Java根类——Object

-    java.lang.Object类，它是Java所有类的根类，Java所有类都直接或间接继承自Object类，它是所有类的“祖先”。
-    Object类属于java.lang包中的类型，不需要显示使用import语句引入，它是由解释器自动引入。

##### 方法

###### String toString()

返回该对象的字符串表示。

为了日志输出等处理方便，所有的对象都可以以文本方式表示，需要在该对象所在类中覆盖toString()方法。如果没有覆盖toString()方法，默认的字符串是“类名@对象的十六进制哈希码”。

>    哈希码（hashCode），每个Java对象都有哈希码（hashCode）属性，哈希码可以用来标识对象，提高对象在集合操作中的执行效率。

###### boolean equals(Object obj)

指示其他某个对象是否与此对象“相等”。

```java
public class Name {
	
	// equals override
    public boolean equals(Object _object){

        [public|protected|private] type value;
        
        if(_object instanceof Name){

            Person _otherPerson=(Person)_otherObject;
            return this.value == _otherPerson.value;
        }

        return false;
    }
}
```

#### 包装类

*    在Java中8种基本数据类型不属于类，不具备“对象”的特征，没有成员变量和方法，不方便进行面向对象的操作。
*    Java提供包装类（Wrapper Class）来将基本数据类型包装成类，每个Java基本数据类型在java.lang包中都有一个相应的包装类，每个包装类对象封装一个基本数据类型数值。

| 基本数据类型 | 包装类    |
| ------------ | --------- |
| boolean      | Boolean   |
| byte         | Byte      |
| char         | Character |
| short        | Short     |
| int          | Integer   |
| long         | Long      |
| float        | Float     |
| double       | Double    |

*    包装类都是final的，不能被继承。包装类都是不可变类，类似于String类，一旦创建了对象，其内容就不可以修改。

##### 数值包装类

###### 构造方法类似

*    [包装类] (int value):通过指定一个数值构造包装类对象
*    [包装类] (String str):通过指定一个字符串str构造对象，s是十进制字符串表示的数值

###### 共同的父类

*    这6个数值包装类有一个共同的父类——Number，Number是一个抽象类，除了这6个子类还有：AtomicInteger、AtomicLong、BigDecimal和BigInteger
*    Number是抽象类，要求它的子类必须实现如下6个方法
     *    如果数值本身很大，可以会导致精度的丢失。
          *    byte byteValue()：将当前包装的对象转换为byte类型的数值。
          *    double doubleValue()：将当前包装的对象转换为double类型的数值。
          *    float floatValue()：将当前包装的对象转换为float类型的数值。
          *    int intValue()：将当前包装的对象转换为int类型的数值。
          *    long longValue()：将当前包装的对象转换为long类型的数值。
          *    short shortValue()：将当前包装的对象转换为short类型的数值。

###### compareTo()方法

*    每一个数值包装类都有int compareTo(数值包装类对象)方法，可以进行包装对象的比较。方法返回值是int，如果返回值是0，则相等；如果返回值小于0，则此对象小于参数对象；如果返回值大于0，则此对象大于参数对象。

###### 字符串转换为基本数据类型

*    每一个数值包装类都提供一些静态parseXXX()方法将字符串转换为对应的基本数据类型
     *    static type parseXXX(String s):将字符串s转换为有符号的十进制
     *    static int parseInt(String s,int radix):将字符串s转换有符号的整数，radix是指定基数，基数用来指定进制。注意这种指定基数的方法在浮点数包装类（Double和Float）中没有的。

###### 基本数据类型转换为字符串

*    每一个数值包装类都提供一些静态toString()方法实现将基本数据类型数值转换为字符串。
     *    static String toString(int i)：将该整数i转换为有符号的十进制表示的字符串。
     *    static String toString(int i, int radix)：将该整数i转换为有符号的特定进制表示的字符串， radix是基数可以指定进制。注意这种指定基数的方法在浮点数包装类（Double和Float）中没有的。

###### 数值转换

*    String 转 int

```java
int [intname] = Integer.parseInt("[Stringvalue]");
```

*    int 转 String

```java
String [stringname] = Integer.toString([intvalue]);
```

*    int 转 x进制，并返回String对象

```java
String strname = Integer.toString(int [intvalue], int x);
```

##### Character类

Character类是char类型的包装类。

###### 方法

*    Character(char value)：构造方法，通过char值创建一个新的Character对象。
*    char charValue()：返回此Character对象的值。
*    int compareTo(Character anotherCharacter)：方法返回值是int，如果返回值是0，则相等；如果返回值小于0，则此对象小于参数对象；如果返回值大于0，则此对象大于参数对象。

##### Boolean类

###### 构造方法

*    Boolean(boolean value)：通过一个boolean值创建Boolean对象。
*    Boolean(String s)：通过字符串创建Boolean对象。s不能为null，s如果是忽略大小写"true"则转换为true对象，其他字符串都转换为false对象。

###### compareTo()

-    Boolean类有int compareTo(Boolean包装类对象)方法，可以进行包装对象的比较。方法返回值是int，如果返回值是0，则相等；如果返回值小于0，则此对象小于参数对象；如果返回值大于0，则此对象大于参数对象。

###### 字符串转换为boolean类型

-    Boolean包装类都提供静态parseBoolean()方法实现将字符串转换为对应的boolean类型
-    static boolean parseBoolean(String s)：将字符串转换为对应的boolean类。s不能为null，s如果是忽略大小写"true"则转换为true，其他字符串都转换为false。

##### 自动装箱/拆箱

*    ava 5之后提供了拆箱(unboxing )功能，拆箱能够将包装类对象自动转换为基本数据类型的数值，而不需要使用intValue()或doubleValue()等方法。
*    类似Java 5还提供了相反功能，自动装箱( autoboxing )，装箱能够自动地将基本数据类型的数值自动转换为包装类对象，而不需要使用构造方法。

##### Math类

###### 舍入方法

*    static double ceil(double a)：返回大于或等于a最小整数。 
*    static double floor(double a)：返回小于或等于a最大整数。 
*    static int round(float a)：四舍五入方法。

###### 最大值和最小值

*    static int min(int a, int b)：取两个int整数中较小的一个整数。
*    static int min(long a, long b)：取两个long整数中较小的一个整数。
*    static int min(float a, float b)：取两个float浮点数中较小的一个浮点数。 
*    static int min(double a, double b)：取两个double浮点数中较小的一个浮点数。

###### 绝对值

*    static int abs(int a)：取int整数a的绝对值。
*    static long abs(long a)：取long整数a的绝对值。
*    static float abs(float a)：取float浮点数a的绝对值。 
*    static double abs(double a)：取double浮点数a的绝对值。

###### 三角函数

*    static double sin(double a)：返回角的三角正弦。
*    static double cos(double a)：返回角的三角余弦。 
*    static double tan(double a)：返回角的三角正切。 
*    static double asin(double a)：返回一个值的反正弦。 
*    static double acos(double a)：返回一个值的反余弦。 
*    static double atan(double a)：返回一个值的反正切。
*    static double toDegrees(double angrad)：将弧度转换为角度。 
*    static double toRadians(double angdeg)：将角度转换为弧度。

###### 对数运算

*    static double log(double a)：返回a的自然对数。

###### 平方根

*    static double sqrt(double a)：返回a的正平方根。

###### 幂运算

*    static double pow(double a, double b)：返回第一个参数的第二个参数次幂的值。

###### 计算随机值

-    static double random()：返回大于等于 0.0 且小于 1.0随机数。

###### 常量

*    圆周率PI
*    自然对数的底数E。

##### 大数值

-    BigInteger和BigDecimal，这里两个类都继承自Number抽象类。

###### BigInteger

-    java.math.BigInteger是不可变的任意精度的大整数。
-    构造方法
     -    BigInteger(String val)：将十进制字符串val转换为BigInteger对象。
     -    BigInteger(String val, int radix)：按照指定基数radix将字符串val转换为BigInteger对象。
-    int compareTo(BigInteger val)：将当前对象与参数val进行比较，方法返回值是int，如果返回值是0，则相等；如果返回值小于0，则此对象小于参数对象；如果返回值大于0，则此对象大于参数对象。
-    BigInteger add(BigInteger val)：加运算，当前对象数值加参数val。
-    BigInteger subtract(BigInteger val)：减运算，当前对象数值减参数val。
-    BigInteger multiply(BigInteger val)：乘运算，当前对象数值乘参数val。
-    BigInteger divide(BigInteger val)：除运算，当前对象数值除以参数val。

###### BigDecimal

*    构造方法
     *    BigDecimal(BigInteger val)：将BigInteger对象val转换为BigDecimal对象。
     *    BigDecimal(double val)：将double转换为BigDecimal对象，参数val是double类型的二进制浮点值准确的十进制表示形式。
     *    BigDecimal(int val)：将int转换为BigDecimal对象。
     *    BigDecimal(long val)：将long转换为BigDecimal对象。
     *    BigDecimal(String val)：将字符串表示数值形式转换为BigDecimal对象。
*    int compareTo(BigDecimal val)：将当前对象与参数val进行比较，方法返回值是int，如果返回值是0，则相等；如果返回值小于0，则此对象小于参数对象；如果返回值大于0，则此对象大于参数对象。
*    BigDecimal add(BigDecimal val)：加运算，当前对象数值加参数val。
*    BigDecimal subtract(BigDecimal val)：减运算，当前对象数值减参数val。
*    BigDecimal multiply(BigDecimal val)：乘运算，当前对象数值乘参数val。
*    BigDecimal divide(BigDecimal val)：除运算，当前对象数值除以参数val。
*    BigDecimal divide(BigDecimal val, int roundingMode)：除运算，当前对象数值除以参数val。 roundingMode要应用的舍入模式。
*    

#### 日期时间相关类

##### Date类

###### 构造方法

*    Date()：用当前时间创建Date对象，精确到毫秒。
*    Date(long date)：指定标准基准时间以来的毫秒数创建Date对象。标准基准时间是格林威治时间1970年1月1日00:00:00。

###### 方法

*    boolean after(Date when)：测试此日期是否在when日期之后。
*    boolean before(Date when)：测试此日期是否在when日期之前。
*    int compareTo(Date anotherDate)：比较两个日期的顺序。如果参数日期等于此日期，则返回值0；如果此日期在参数日期之前，则返回小于0的值；如果此日期在参数日期之后，则返回大于0的值。
*    long getTime()：返回自1970年1月1日00:00:00以来此Date对象表示的毫秒数。
*    void setTime(long time)：用毫秒数time设置日期对象，time是自1970年1月1日00:00:00以来此Date对象表示的毫秒数。

###### 日期格式化和解析

*    日期格式化类是java.text.DateFormat，DateFormat是抽象类，它的常用具体类是java.text.SimpleDateFormat。
     *    String format(Date date)：将一个Date格式化为日期/时间字符串。
     *    Date parse(String source)：从给定字符串的开始解析文本，以生成一个日期对象。如果解析失败则抛出ParseException。
     *    并不是所有的字符串都能够转换为日期，如果转换失败parse方法会抛出异常ParseException。

```java
public static void main(String[] args) throws ParseException {...}
```

*    构造方法
     *    SimpleDateFormat()：用默认的模式和默认语言环境的日期格式符号构造SimpleDateFormat。
     *    SimpleDateFormat(String pattern)：用给定的模式和默认语言环境的日期格式符号构造SimpleDateFormat。pattern参数是日期和时间格式模式。

| 字母 | 日期或时间元素  |
| ---- | --------------- |
| y    | 年              |
| M    | 年中的月份      |
| D    | 年中的天数      |
| d    | 月份中的天数    |
| H    | 一天中的小时数  |
| h    | AM/PM中的小时数 |
| a    | AM/PM标记       |
| m    | 小时中的分钟数  |
| s    | 分钟中的秒数    |
| S    | 毫秒数          |
| Z    | 时区            |

##### Calendar类

*    有时为了取得更多的日期时间信息，或对日期时间进行操作，可以使用java.util.Calendar类，Calendar是一个抽象类，不能实例化，但是通过静态工厂方法getInstance()获得Calendar实例。

###### 方法

*    static Calendar getInstance()：使用默认时区和语言环境获得一个日历。
*    void set(int field, int value)：将给定的日历字段设置为给定值。
*    void set(int year,int month,int date)：设置日历字段YEAR、MONTH和DAY_OF_MONTH的值。
*    Date getTime()：返回一个表示此Calendar时间值（从1970年1月1日00:00:00至现在的毫秒数）的Date对象。
*    boolean after(Object when)：判断此Calendar表示的时间是否在指定时间之后，返回判断结果。 
*    boolean before(Object when)：判断此Calendar表示的时间是否在指定时间之前，返回判断结果。
*    int compareTo(Calendar anotherCalendar)：比较两个Calendar对象表示的时间值。

##### LocalDate、LocalTime和LocalDateTime

*    都位于java.time包中，LocalDate表示一个不可变的日期对象；LocalTime表示一个不可变的时间对象；LocalDateTime表示一个不可变的日期和时间。

###### 方法

*    now()
     *    static LocalDate now()：LocalDate静态工厂方法，该方法使用默认时区获得当前日期，返回LocalDate对象。
     *    static LocalTime now()：LocalTime静态工厂方法，该方法使用默认时区获得当前时间，返回LocalTime对象。
     *    static LocalDateTime now()：LocalDateTime静态工厂方法，该方法使用默认时区获得当前日期时间，返回LocalDateTime对象。
*    of()
     *    static LocalDateTime of(int year, int month, int dayOfMonth, int hour, int minute, int second)：按照指定的年、月、日、小时、分钟和秒获得LocalDateTime实例，将纳秒设置为零。
     *    static LocalTime of(int hour, int minute, int second)：按照指定的小时、分钟和秒获取一个LocalTime实例。
     *    static LocalDate of(int year, int month, int dayOfMonth)：按照指定的年、月和日获得一个LocalDate实例，日期中年、月和日必须有效，否则将抛出异常。

| 参数       | 说明                              |
| ---------- | --------------------------------- |
| year       | 从-999,999,999到999,999,999的年份 |
| month      | 一年中的月份，从1至12             |
| dayOfMonth | 月中的天，从1至31                 |
| hour       | 从0到23表示的小时                 |
| minute     | 从0到59表示的分钟                 |
| second     | 从0到59表示的秒                   |

###### 日期格式化和解析

-    Java 8提供的日期格式化类是java.time.format.DateTimeFormatter，DateTimeFormatter中本身没有提供日期格式化和日期解析方法，这些方法还是由LocalDate、LocalTime和LocalDateTime提供的。
-    日期格式化
     -    日期格式化方法是format，这三个类每一个都有String format(DateTimeFormatter formatter)，参数formatter是DateTimeFormatter类型

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
```

-    日期解析
     -    static LocalDateTime parse(CharSequence text)：使用默认格式，从一个文本字符串获取一个LocalDateTime实例。
     -    static LocalDateTime parse(CharSequence text, DateTimeFormatter formatter)：使用指定格式化，从文本字符串获取LocalDateTime实例。
     -    static LocalDate parse(CharSequence text)：使用默认格式，从一个文本字符串获取一个LocalDate实例。
     -    static LocalDate parse(CharSequence text, DateTimeFormatter formatter)：使用指定格式化，从文本字符串获取LocalDate实例。
     -    static LocalTime parse(CharSequence text)：使用默认格式，从一个文本字符串获取一个LocalTime实例。
     -    static LocalTime parse(CharSequence text, DateTimeFormatter formatter)：使用指定的格式化，从文本字符串获取LocalTime实例。

### 内部类

*    Java中还有一种内部类技术，简单说就是在一个类的内部定义一个类。

>    内部类技术虽然使程序结构变得紧凑，但是却在一定程度上破坏了Java面向对象思想。

#### 概述

*    Java语言中允许在一个类（或方法、代码块）的内部定义另一个类，后者称为“内部类”（Inner Classes），也称为“嵌套类”（Nested Classes），封装它的类称为“外部类”。内部类与外部类之间存在逻辑上的隶属关系，内部类一般只用在封装它的外部类或代码块中使用。

#### 作用

*    封装。将不想公开的实现细节封装到一个内部类中，内部类可以声明为私有的，只能在所在外部类中访问。
02.	提供命名空间。静态内部类和外部类能够提供有别于包的命名空间。
03.	便于访问外部类成员。内部类能够很方便访问所在外部类的成员，包括私有成员也能访问。

#### 内部类的分类

*    内部类
     *    有名内部类
          *    局部内部类
          *    成员内部类
               *    实例成员内部类
               *    静态成员内部类
     *    匿名内部类

#### 成员内部类

成员内部类类似于外部类的成员变量，在外边类的内部，且方法体和代码块之外定义的内部类。

##### 实例内部类

*    实例内部类与实例变量类似，可以声明为公有级别、私有级别、默认级别或保护级别，即4种访问级别都可以，而外部类只能声明为公有或默认级别。

```java
public class name{
    
    // TODO
    
    // 内部类
    class name2{
        
        // TODO
    }
}
```

##### 静态内部类

*    在静态内部类中可以访问外部类的静态成员，但是不能访问非静态成员。
*    静态内部类与静态变量类似，在声明的时候使用关键字static修饰，静态内部类只能访问外部类静态成员，所以静态内部类使用的场景不多。但可以提供有别于包的命名空间。

```java
public class name{
    
    // static
    static [public|protected|private] type value;
    
    // 内部类
    static class name2{
        
        // TODO
        // use outer static value
    }
}
```

##### 局部内部类

*    局部内部类就是在方法体或代码块中定义的内部类，局部内部类的作用域仅限于方法体或代码块中。
*    局部内部类访问级别只能是默认的，不能是公有的、私有的和保护的访问级别，即不能使用public、 private和protected修饰。局部内部类也不能是静态，即不能使用static修饰。局部内部类可以访问外部类所有成员。

```java
public class Outer {

    // TODO

    // 在方法体或代码块中
    public type function([parameter] value) {

        // TODO

        // 在方法体或代码块中定义的内部类
        // 局部内部类访问级别只能是默认的
        class Inner {

            void function_2()) {

                // TODO
            }
        }

        new Inner().function_2();
    }
}
```

##### 匿名内部类

-    匿名内部类是没有名字的内部类，本质上是没有名的局部内部类，具有局部内部类所有特征。
-    匿名内部类可以使你的代码更加简洁，你可以在定义一个类的同时对其进行实例化。它与局部类很相似，不同的是它没有类名，如果某个局部类你只需要用一次，那么你就可以使用匿名内部类
-    请参考Lambda使用方法

```java
interface name{
    
    public function();
}

name name_2=new name(){
    
    @Override
    public function(){
        
        // TODO
    }
}
```

## 方法重载（Overload）

这些相同名字的方法之所以能够在一个类中同时存在，是因为它们的方法参数列表，调用时根据参数列表调用相应重载方法。

调用哪一个方法是根据参数列表决定的。如果参数类型不一致，编译器会进行自动类型转换寻找适合版本的方法，如果没有适合方法，则会发生编译错误。

## 封装性与访问控制

|      | 同一个类 | 同一个包 | 不同包的子类 | 不同包非子类 |
| ---- | -------- | -------- | ------------ | ------------ |
| 私有 | Y        |          |              |              |
| 默认 | Y        | Y        |              |              |
| 保护 | Y        | Y        | Y            |              |
| 公有 | Y        | Y        | Y            | Y            |

### 私有级别

私有级别的关键字是private，私有级别的成员变量和方法只能在其所在类的内部自由使用，在其他的类中则不允许直接访问。

私有级别限制性最高。

### 默认级别

默认级别没有关键字，也就是没有访问修饰符，默认级别的成员变量和方法，可以在其所在类内部和同一个包的其他类中被直接访问，但在不同包的类中则不允许直接访问。

### 公有级别

公有级别的关键字是public，公有级别的成员变量和方法可以在任何场合被直接访问，是最宽松的一种访问控制等级。

### 保护级别

保护级别的关键字是protected，保护级别在同一包中完全与默认访问级别一样，但是不同包中子类能够继承父类中的protected变量和方法，这就是所谓的保护级别，“保护”就是保护某个类的子类都能继承该类的变量和方法。

>    访问成员有两种方式：一种是调用，即通过类或对象调用它的成员；另一种是继承，即子类继承父类的成员变量和方法。

访问类成员时，在能满足使用的前提下，应尽量限制类中成员的可见性，访问级别顺序是：私有级别→默认级别→保护级别→公有级别。

## 静态变量和静态方法

Java 中被 static 修饰的成员称为静态成员或类成员。它属于整个类所有，而不是某个对象所有，即被类的所有对象所共享。

静态成员可以使用类名直接访问，也可以使用对象名进行访问。

*    静态变量可以直接使用类名来访问，无需创建对象

使用 static 可以修饰变量、方法和代码块。

静态成员属于整个类，当系统第一次使用该类时，就会为其分配内存空间直到该类被卸载才会进行资源回收

### 静态变量与静态方法关系

*    静态方法中可以直接调用同类中的静态成员，但不能直接调用非静态成员
*    如果希望在静态方法中调用非静态变量，可以通过创建类的对象，然后通过对象来访问非静态变量。
*    在普通成员方法中，则可以直接访问同类的非静态变量和静态变量
*    静态方法中不能直接调用非静态方法，需要通过对象来访问非静态方法。

### 执行顺序

程序运行时静态初始化块最先被执行，然后执行普通初始化块，最后才执行构造方法。

## 对象

类实例化可生成对象，实例方法就是对象方法，实例变量就是对象属性。一个对象的生命周期包括三个阶段：创建、使用和销毁。

### 创建对象

创建对象包括两个步骤：声明和实例化。

#### 声明

*    声明对象与声明普通变量没有区别

```java
type objectName;
```

##### 空对象

*    一个引用变量没有通过new分配内存空间，这个对象就是空对象，Java使用关键字null表示空对象。
*    引用变量默认值是null。当试图调用一个空对象的实例变量或实例方法时，会抛出空指针异常NullPointerException
*    应该避免调用空对象的成员变量和方法

#### 实例化

*    实例化过程分为两个阶段：为对象分配内存空间和初始化对象，首先使用new运算符为对象分配内存空间，然后再调用构造方法初始化对象。

### 构造方法

*    构造方法名必须与类名相同。
*    构造方法没有任何返回值，包括void。
*    构造方法只能与new运算符结合使用。

```java
public class name{
    // default
    public name([parameter] value){
        // TODO
    }
}
```

#### 默认构造方法

*    有时在类中根本看不到任何的构造方法。Java虚拟机为没有构造方法的类，提供一个无参数的默认构造方法，默认构造方法其方法体内无任何语句

```java
public class name{
    public name(){}
}
```

#### 构造方法重载

*    在一个类中可以有多个构造方法，它们具体有相同的名字（与类名相同），参数列表不同，所以它们之间一定是重载关系。

#### 构造方法封装

```java
public class name{
    // 公有级别限制
    public name([parameter] value){
        // TODO
    }
    
    // 私有级别限制
    private name([parameter] value){
        // TODO
    }
    
    // 默认级别限制，默认级别只能在同一个包中访问
    name([parameter] value){
        // TODO
    }
    
    // 保护级别限制，该构造方法在同一包中与默认级别相同，在不同包中可以被子类继承
    protected name([parameter] value){
        // TODO
    }
}
```

>    单例模式是一种常用的软件设计模式，单例模式可以保证系统中一个类只有一个实例。

*    不同访问权限而相同参数的构造函数不能共存。

## this关键字

this指向对象本身，一个类可以通过this来获得一个代表它自身的对象变量。

#### 使用

*    调用实例变量。
*    调用实例方法。
*    调用其他构造方法。

#### 作用

*    命名冲突，参数是作用域为整个方法的局部变量，为了防止局部变量与成员变量命名发生冲突，可以使用this调用成员变量。
*    this也可以调用本对象的方法

## 对象销毁

对象不再使用时应该销毁。C++语言对象是通过delete语句手动释放，Java语言对象是由垃圾回收器（Garbage Collection）收集然后释放，程序员不用关心释放的细节。

垃圾回收器（Garbage Collection）的工作原理是：当一个对象的引用不存在时，认为该对象不再需要，垃圾回收器自动扫描对象的动态内存区，把没有引用的对象作为垃圾收集起来并释放。

## 继承与多态

类的继承性是面向对象语言的基本特性，多态性的前提是继承性。Java支持继承性和多态性。

### Java中的继承

继承使用的关键字是extends， extends后面的class是父类。

>    一般情况下，一个子类只能继承一个父类，这称为“单继承”，但有的情况下一个子类可以有多个不同的父类，这称为“多重继承”。在Java中，类的继承只能是单继承，而多重继承可以通过实现多个接口实现。也就是说，在Java中，一个类只能继承一个父类，但是可以实现多个接口。

面向对象分析与设计（OOAD）时，会用到UML图 ，其中类图非常重要，用来描述系统静态结构。

UML是Unified Modeling Language的缩写，即统一标准建模语言。它集成了各种优秀的建模方法学发展而来的。UML图常用的有例图、协作图、活动图、序列图、部署图、构件图、类图、状态图。

### 调用父类构造方法

当子类实例化时，不仅需要初始化子类成员变量，也需要初始化父类成员变量，初始化父类成员变量需要调用父类构造方法，子类使用super关键字调用父类构造方法。

```java
public class Base{
    
    public Base([parameter1] value1){
        // TODO
    }
}

public class Plus extends Base{
    
    public Plus([parameter2] value2){
        supper(value1);
        // TODO
    }
}
```

*    super语句必须位于子类构造方法的第一行。

子类构造方法由于没有super语句，编译器会试图调用父类默认构造方法（无参数构造方法），但是如果父类并没有默认构造方法，因此会发生编译错误。解决这个编译错误有三种办法：

*    在父类中添加默认构造方法，子类Student会隐式调用父类的默认构造方法。
*    在子类构造方法添加super语句，显式调用父类构造方法，super语句必须是第一条语句。
*    在子类构造方法添加this语句，显式调用当前对象其他构造方法，this语句必须是第一条语句。

### 成员变量隐藏和方法覆盖

#### 成员变量隐藏

子类成员变量与父类一样，会屏蔽父类中的成员变量，称为“成员变量隐藏”。

```java
public class Base{
    
    type value;
    
    public Base(){
        // TODO
    }
}

public class Plus extends Base{
    
    type value;// hide the base value
    
    public Plus(){
        super();
        // TODO
    }
}
```

#### 方法的覆盖（Override）

如果子类方法完全与父类方法相同，即：相同的方法名、相同的参数列表和相同的返回值，只是方法体不同，这称为子类覆盖（Override）父类方法。

##### @Override注解

1.   提高程序的可读性。
2.   编译器检查@Override注解的方法在父类中是否存在，如果不存在则报错。

##### 方法覆盖原则

1.	覆盖后的方法不能比原方法有更严格的访问控制（可以相同）。例如将代码第②行访问控制public修改private，那么会发生编译错误，因为父类原方法是protected。
2.	覆盖后的方法不能比原方法产生更多的异常。

##### 首先重载与覆盖的区别

1.   方法重载是同一个类中多个方法之间的关系，是水平关系；而方法覆盖是子类和父类之间的关系，是垂直关系。
2.   方法重载要求参数的列表不同（类型或者数目，仅形参名不同不视为参数列表不同），覆盖则要求参数列表相同（形参名不同亦视为参数列表相同）。
3.   方法重载是多个方法之间的关系；覆盖只能由一个方法，或只能由一对方法产生关系。
4.   重载关系，是根据调用时的实参表与形参表来选择方法体的，覆盖关系，调用哪个方法则是根据对象的类型（对象存储空间，判断是父类还是子类）来决定。

### 多态

#### 前提条件

*    继承。多态发生一定要子类和父类之间。
*    覆盖。子类覆盖了父类的方法。
*    声明的变量类型是父类类型，但实例则指向子类实例。

多态发生时，Java虚拟机运行时根据引用变量指向的实例调用它的方法，而不是根据引用变量的类型调用。

### 使用

```java
public class Base{
    
    public type function(){
        
        // TODO
    }
}

public class Plus1 extends Base{
    
    public type function(){
        
        // TODO
    }
}

public class Plus2 extends Base{
    
    public type function(){
        
        // TODO
    }
}

// 多态
Base c_plus1=new Plus1();
Base c_plus2=new Plus2();
```

#### 引用类型检查

*    在运行时判断一个对象是否属于某个引用类型，这时可以使用instanceof运算符

```java
obj instanceof type;
```

如果obj对象是type引用类型实例则返回true，否则false

```java
if(obj instanceof type){
    
    // true
}else{
    
    // false
}
```

#### 引用类型转换

引用类型可以进行转换，但并不是所有的引用类型都能互相转换，只有属于同一棵继承层次树中的引用类型才可以转换。

引用类型转换也是通过小括号运算符实现，类型转换有两个方向：将父类引用类型变量转换为子类类型，这种转换称为向下转型（downcast）；将子类引用类型变量转换为父类类型，这种转换称为向上转型（upcast）。向下转型需要强制转换，而向上转型是自动的。

# Lambda表达式

*    Lambda表达式是一个匿名函数（方法）代码块，可以作为表达式、方法参数和方法返回值。

## 特点

*    **可选类型声明：**不需要声明参数类型，编译器可以统一识别参数值。
*    **可选的参数圆括号：**一个参数无需定义圆括号，但多个参数需要定义圆括号。
*    **可选的大括号：**如果主体包含了一个语句，就不需要使用大括号。
*    **可选的返回关键字：**如果主体只有一个表达式返回值则编译器会自动返回值，大括号需要指定明表达式返回了一个数值。

## 函数式接口

*    Lambda表达式实现的接口不是普通的接口，称为是函数式接口，这种接口只能有一个方法。如果接口中声明多个抽象方法，那么Lambda表达式会发生编译错误

>    The target type of this expression must be a functional interface

```java
//可计算接口
@FunctionalInterface
public interface interfacename {
	
    // 只有一个函数
    public type function(){
        
        // TODO
    }
}
```

```java
public static function(interfacename inter,[parameter]){
    
    // TODO
    // inter.function([parameter]);
}
```

## 语法

```java
(参数列表)->{
    
    // Lambda表达体
};
```

```java
(parameters) -> expression
```

## Lambda表达式简化形式

### 省略参数类型

*    Lambda表达式可以根据上下文环境推断出参数类型。

### 省略return和大括号

*    如果Lambda表达式体中只有一条语句，那么可以省略return和大括号

## 作为参数使用Lambda表达式

*    Lambda表达式一种常见的用途是作为参数传递给方法。这需要声明参数的类型声明为函数式接口类型。

## 访问变量

-    Lambda表达式可以访问所在外层作用域内定义的变量，包括：成员变量和局部变量。

### 访问成员变量

*    静态方法中不能访问实例成员变量
*    实例方法中能够访问静态成员变量和实例成员变量
     *    当访问实例成员变量或实例方法时可以使用this，如果不与局部变量发生冲突情况下可以省略this。

### 捕获局部变量

*    Lambda表达式中捕获变量时，会将变量当成final的，在Lambda表达式中不能修改那些捕获的变量。
*    不管这个变量是否显式地使用final修饰，它都不能在Lambda表达式中修改变量

## 方法引用

*    Java 8之后增加了双冒号“::”运算符，该运算符用于“方法引用”，注意不是调用方法。“方法引用”虽然没有直接使用Lambda表达式，但也与Lambda表达式有关，与函数式接口有关。

### 语法形式

```java
类型名::静态方法        // 静态方法的方法引用
实例名::实例方法        // 实例方法的方法引用
```

# 异常处理

## Throwable类

*    所有的异常类都直接或间接地继承于java.lang.Throwable类

### 方法

*    String getMessage()：获得发生异常的详细消息。 
*    void printStackTrace()：打印异常堆栈跟踪信息。 
*    String toString()：获得异常对象的描述。

```java
try {
    
    // TODO
} catch (Throwable throwable) {

    System.out.println("getMessage(): " + throwable.getMessage());
    System.out.println("toString(): " + throwable.toString());
    System.out.println("printStackTrace()输出信息如下: ");
    throwable.printStackTrace();
}
```

### Error和Exception

*    Throwable有两个直接子类：Error和Exception。

#### Error

*    Error是程序无法恢复的严重错误，程序员根本无能为力，只能让程序终止。

#### Exception

*    Exception是程序可以恢复的异常，它是程序员所能掌控的。

##### 受检查异常和运行时异常

###### 受检查异常

*    受检查异常是除RuntimeException以外的异常类。它们的共同特点是：编译器会检查这类异常是否进行了处理，即要么捕获（try-catch语句），要么不抛出（通过在方法后声明throws），否则会发生编译错误。它们种类很多，前面遇到过的日期解析异常ParseException。

###### 运行时异常

*    运行时异常是继承RuntimeException类的直接或间接子类。运行时异常往往是程序员所犯错误导致的，健壮的程序不应该发生运行时异常。它们的共同特点是：编译器不检查这类异常是否进行了处理，也就是对于这类异常不捕获也不抛出，程序也可以编译通过。由于没有进行异常处理，一旦运行时异常发生就会导致程序的终止，这是用户不希望看到的。

## 捕获异常

### try-catch语句

#### 结构

##### 单层

```java
try{
    // 可能会发生异常的语句
}catch(Throwable e){
    // 处理异常e
}catch(Throwable e){
    // 处理异常e
}catch(Throwable e){
    // 处理异常e
}
```

##### 嵌套

```java
try{
    
    // TODO
    
    try{
        
        // TODO
    }catch(Throwable e){
    	// 处理异常e
	}catch(Throwable e){
    	// 处理异常e
	}
}catch(Throwable e){
    // 处理异常e
}catch(Throwable e){
    // 处理异常e
}
```

##### 多重捕获

```java
try{
    
    // 可能会发生异常的语句
}catch(Exception1|Exception2){
    
    //TODO
}
```

#### try代码块

*    try代码块中应该包含执行过程中可能会发生异常的语句。一条语句是否有可能发生异常，这要看语句中调用的方法。
*    静态方法、实例方法和构造方法都可以声明抛出异常，凡是抛出异常的方法都可以通过try-catch进行捕获，当然运行时异常可以不捕获。

#### catch代码块

*    每个try代码块可以伴随一个或多个catch代码块，用于处理try代码块中所可能发生的多种异常。
*    在多个catch代码情况下，当一个catch代码块捕获到一个异常时，其他的catch代码块就不再进行匹配。

>    在捕获到异常之后，通过printStackTrace()语句打印异常堆栈跟踪信息，往往只是用于调试，给程序员提示信息。堆栈跟踪信息对最终用户是没有意义的，

## 释放资源

*    有时在try-catch语句中会占用一些非Java资源，需要程序员释放。为了确保这些资源能够被释放可以使用finally代码块或Java 7之后提供自动资源管理（Automatic Resource Management）技术。

### finally代码块

```java
try{
    // 可能会生成异常语句
}catch(Throwable e1){
    // 处理异常e1
}catch(Throwable e2){
    // 处理异常e2
}catch(Throwable eN){
    // 处理异常eN
}finally{
    // 释放资源
}
```

*    无论try正常结束还是catch异常结束都会执行finally代码块

### 自动资源管理

-    使用finally代码块释放资源会导致程序代码大量增加，一个finally代码块往往比正常执行的程序还要多。在Java 7之后提供自动资源管理（Automatic Resource Management）技术，可以替代finally代码块，优化代码结构，提高程序可读性。

```java
try(声明或初始化资源语句){
    // 可能会生成异常语句
}catch(Throwable e1){
    // 处理异常e1
}catch(Throwable e2){
    // 处理异常e2
}catch(Throwable eN){
    // 处理异常eN
}
```

*    在try语句后面添加一对小括号“()”，其中是声明或初始化资源语句，可以有多条语句语句之间用分号“;”分隔。

## throws与声明方法抛出异常

*    在一个方法中如果能够处理异常，则需要捕获并处理。但是本方法没有能力处理该异常，捕获它没有任何意义，则需要在方法后面声明抛出该异常，通知上层调用者该方法有可以发生异常。

```java
class className {
    
    [public | protected | private ] [static] [final | abstract] [native] [synchronized] type methodName([paramList]) [throws exceptionList] {
        
        // TODO
    }
}
```

*    其中参数列表之后的[throws exceptionList]语句是声明抛出异常。方法中可能抛出的异常（除了Error和RuntimeException及其子类外）都必须通过throws语句列出，多个异常之间采用逗号（,）分隔。

### 自定义异常类

```java
public class MyException extends Exception{
    public MyException{
        
        // TODO
    }
    
    public MyException(String message){

        super(message);
    }
}
```

*    自定义异常类一般需要提供两个构造方法，一个是无参数的默认构造方法，异常描述信息是空的；另一个是字符串参数的构造方法，message是异常描述信息，getMessage()方法可以获得这些信息。

### throw与显式抛出异常

```java
throw Throwable或其子类的实例
```

# 泛型

-    使用泛型可以最大限度地重用代码、保护类型的安全以及提高性能。泛型特性对Java影响最大是集合框架的使用。
-    强制类型转换是有风险的，如果不进行判断就臆断进行类型转换会发生ClassCastException异常。
-    在集合中如果没有使用泛型，Eclipse等IDE工具都会警告。

## 使用泛型

*    泛型对于Java影响最大就是集合了，Java 5之后所有的集合类型都可以有泛型类型，可以限定存放到集合中的类型。

### LIst

#### 声明

```java
List<type> container = new ArrayList<type>();
```

#### 迭代器

```java
Iterator<type> iter = container.iterator();
while(iter.hasNext()){
    // TODO
}
```

#### for-each

```java
for(type item:container){
    // TODO
}
```

### Map

#### 声明

```java
Map<type1,type2> container = new HashMap<type1,type2>();
```

#### 迭代器

```java
Iterator<Map.Entry<type1,type2>> iter = container.entrySet().iterator();
while(iter.hasNext()){
    
    Map.Entry<type1,type2> entry = iter.next();
    // TODO
}
```

#### for-each

```java
for (Map.Entry<type1, type2> entry : container.entrySet()) {
    // TODO
}
```

## 自定义泛型类

```java
public class name<T>{
    
    // TODO
}
```

## 泛型方法

```java
[public|protected|private] [static] <T> [void|type] functionname([parameter]){
    
    // TODO
}
```

# 文件管理

*    Java语言使用File类对文件和目录进行操作，查找文件时需要实现FilenameFilter或FileFilter接口。另外，读写文件内容可以通过FileInputStream、FileOutputStream、FileReader和FileWriter类实现，它们属于I/O流

## File类

### 构造方法

*    File(String path)：如果path是实际存在的路径，则该File对象表示的是目录；如果path是文件名，则该File对象表示的是文件。
*    File(String path, String name)：path是路径名，name是文件名。
*    File(File dir, String name)：dir是路径对象，name是文件名。

### 获得文件名

*    String getName( )：获得文件的名称，不包括路径。
*    String getPath( )：获得文件的路径。
*    String getAbsolutePath( )：获得文件的绝对路径。
*    String getParent( )：获得文件的上一级目录名。

### 文件属性测试

*    boolean exists( )：测试当前File对象所表示的文件是否存在。 
*    boolean canWrite( )：测试当前文件是否可写。
*    boolean canRead( )：测试当前文件是否可读。
*    boolean isFile( )：测试当前文件是否是文件。
*    boolean isDirectory( )：测试当前文件是否是目录。

### 文件操作

*    long lastModified( )：获得文件最近一次修改的时间。
*    long length( )：获得文件的长度，以字节为单位。
*    boolean delete( )：删除当前文件。成功返回 true，否则返回false。
*    boolean renameTo(File dest)：将重新命名当前File对象所表示的文件。成功返回 true，否则返回false。

### 目录操作

*    boolean mkdir( )：创建当前File对象指定的目录。
*    String[] list()：返回当前目录下的文件和目录，返回值是字符串数组。
*    String[] list(FilenameFilter filter)：返回当前目录下满足指定过滤器的文件和目录，参数是实现FilenameFilter接口对象，返回值是字符串数组。
*    File[] listFiles()：返回当前目录下的文件和目录，返回值是File数组。
*    File[] listFiles(FilenameFilter filter)：返回当前目录下满足指定过滤器的文件和目录，参数是实现FilenameFilter接口对象，返回值是File数组。
*    File[] listFiles(FileFilter filter)：返回当前目录下满足指定过滤器的文件和目录，参数是实现FileFilter接口对象，返回值是File数组。

对目录操作有两个过滤器接口：FilenameFilter和FileFilter。它们都只有一个抽象方法accept， 

*    FilenameFilter接口中的accept方法如下：
     *    boolean accept(File dir, String name)：测试指定dir目录中是否包含文件名为name的文件。
*    FileFilter接口中的accept方法如下：
     *    boolean accept(File pathname)：测试指定路径名是否应该包含在某个路径名列表中。