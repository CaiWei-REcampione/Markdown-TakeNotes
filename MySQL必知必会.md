

# 目录

[toc]

# 了解SQL

SQL(发音为字母S-Q-L或sequel)是结构化查询语言(Structured QueryLanguage)的缩写。SQL是一种专门用来与数据库通信的语言。

与其他语言(如,英语以及Java和Visual Basic这样的程序设计语言)不一样, SQL由很少的词构成,这是有意而为的。设计SQL的目的是很好地完成一项任务,即提供一种从数据库中读写数据的简单有效的方法。

MysQL、Oracle以及Microsoft SQL Server等数据库是基于客户机-服务器的数据库。客户机-服务器应用分为两个不同的部分。服务器部分是负责所有数据访问和处理的一个软件。这个软件运行在称为数据库服务器的计算机上。

>    SQL语句和大小写	请注意, SQL语句**不区分大小写**,因此SELECT与select是相同的。同样,写成Select也没有关系。许多SQL开发人员喜欢对所有SQL关键字使用大写,而对所有列和表名使用小写,这样做使代码更易于阅读和调试。

# MySQL工具

如前所述, MySQL是一个客户机-服务器DBMS,因此,为了使用MysQL,需要有一个客户机,即你需要用来与MySQL打交道(给MysQL提供要执行的命令)的一个应用。

有许多客户机应用可供选择,但在学习MySQL (确切地说,在编写和测试MySQL脚本时),最好是使用专门用途的实用程序。特别是有3个工具需要提及。

*    MySQL命令行实用程序

mysql命令行实用程序是使用最多的实用程序之一,它对于快速测试和执行脚本非常有价值。

*    MySQL Administrator

MysQL Administrator (MySQL管理器)是一个图形交互客户机,用来简化MySQL服务器的管理。

*    MySQL Query Browser

MySQL Query Browser为一个图形交互客户机,用来编写和执行MySQL命令。

# 使用MySQL

## 连接

MySQL与所有客户机-服务器DBMS一样,要求在能执行命令之前登录到DBMS.登录名可以与网络登录名不相同(假定你使用网络),MySQL在内部保存自己的用户列表,并且把每个用户与各种权限关联起来。在最初安装MySQL时,很可能会要求你输入一个管理登录(通常为root)和一个口令。如果你使用的是自己的本地服务器,并且是简单地试验一下MySQL,使用上述登录就可以了。但现实中,管理登录受到密切保护(因为对它的访问授予了创建表、删除整个数据库、更改登录和口令等完全的权限)。

为了连接到MysQL,需要以下信息:

*    主机名(计算机名)
*    如果连接到本地MysQL服务器,为1ocalhost
*    端口(如果使用默认端口3306之外的端口)
*    一个合法的用户名
*    用户口令(如果需要)

## 选择数据库

在你最初连接到MySQL时,没有任何数据库打开供你使用。在你能执行任意数据库操作前,需要选择一个数据库。为此,可使用USE关键字。

*    关键字(key word)

作为MySQL语言组成部分的一个保留字。决不要用关键字命名一个表或列。

例如,为了使用crashcourse数据库,应该输入以下内容:

>    输入 USE crashcourse
>
>    输出 Database changed

分析 USE语句并不返回任何结果。依赖于使用的客户机,,显示某种形式的通知。

### 了解数据库和表

数据库、表、列、用户、权限等的信息被存储在数据库和表中(MySQL使用MySQL来存储这些信息)。不过,内部的表一般不直接访问。可用MySQL的SHOW命令来显示这些信息(MySQL从内部表中提取这些信息)。请看下面的例子:

#### SHOW DATABASES

```mysql
SHOW DATABASES;
```

SHOW DATABASES;返回可用数据库的一个列表。包含在这个列表中的可能是MySQL内部使用的数据库(如例子中的mysql和information_schema),当然,你自己的数据库列表可能看上去与这里的不一样。

#### SHOW TABLES

```mysql
SHOW TABLES;
```

为了获得一个数据库内的表的列表,使用SHOW TABLES

#### SHOW COLUMNS FROM

```mysql
SHOW COLUMNS FROM customers;
```

SHOW COLUMNS要求给出一个表名(这个例子中的FROM customers),它对每个字段返回一行,行中包含字段名、数据类型、是否允许NULL、键信息、默认值以及其他信息(如字段cust_id的auto increment)。

>    什么是自动增量? 	某些表列需要唯一值,例如,订单编号雇员ID或(如上面例子中所示的)顾客ID.在每个行添加到表中时,MySQL可以自动地为每个行分配下一个可用编号,不用在添加一行时手动分配唯一值(这样做必须记住最后一次使用的值),这个功能就是所谓的自动增量。如果需要它,则必须在用CREATE语句创建表时把它作为表定义的组成部分。我们将在第21章中介绍CREATE语句.

#### SHOW STATUS

```mysql
SHOW STATUS;
```

SHOW STATUS,用于显示广泛的服务器状态信息

#### SHOW CREATE

```mysql
SHOW CREATE DATABASE;
SHOW CREATE TABLE;
```

SHOW CREATE DATABASE和SHOW CREATE TABLE,分别用来显示创建特定数据库或表的MySQL语句

#### SHOW GRANTS

```mysql
SHOW GRANTS;
```

SHOW GRANTS,用来显示授予用户(所有用户或特定用户)的安全权限

#### SHOW WARINGS

```mysql
SHOW ERRPRS;
SHOW WARNINGS;
```

SHOW ERRORS和SHOW WARNINGS,用来显示服务器错误或警告消息

# 检索信息SELECT

SQL语句是由简单的英语单词构成的。这些单词称为关键字,每个SQL语句都是由一个或多个关键字构成的。大概,最经常使用的SQL语句就是SELECT语句了。它的用途是从一个或多个表中检索信息。为了使用SELECT检索表数据,必须至少给出两条信息-想选择什么,以及从什么地方选择。

## 检索单个列

```mysql
SELECT prod_name
FROM products;
```

分析上述语句利用SELECT语句从products表中检索一个名为prod_name的列。

所需的列名在SELECT关键字之后给出, FROM关键字指出从其中检索数据的表名。

## 检索多个列

```mysql
SELECT prod_id, prod_name, prod_price
FROM products;
```

与前一个例子一样,这条语句使用SELECT语句从表products中选择数据。在这个例子中,指定了3个列名,列名之间用逗号分隔。

## 检索所有列(*)

```mysql
SELECT *
FROM products;
```

如果给定一个通配符(*),则返回表中所有列。列的顺序一般是列在表定义中出现的顺序。但有时候并不是这样的,表的模式的变化(如添加或删除列)可能会导致顺序的变化。

## 检索不同的行

```mysql
SELECT DISTINCT vend_id
FROM products;
```

SELECT DISTINCT vend_id告诉MySQL只返回不同(唯一)的vend_id行,因此只返回4行。如果使用DISTINCT关键字,它必须直接放在列名的前面。

## 限制结果

```mysql
SELECT prod_name
FROM products
LIMIT 5;
```

SELECT语句返回所有匹配的行,它们可能是指定表中的每个行。为了返回第一行或前几行,可使用LIMIT子句。

此语句使用SELECT语句检索单个列。LIMIT 5指示MySQL返回不多于5行。

所以,带一个值的LIMIT总是从第一行开始,给出的数为返回的行数。带两个值的LIMIT可以指定从行号为第一个值的位置开始。

## 使用完全限定的表名

迄今为止使用的SQL例子只通过列名引用列。也可能会使用完全限定的名字来引用列(同时使用表名和列字)。请看以下例子:

```mysql
SELECT products.prod_name
FROM products;
```

这条SQL语句在功能上等于本章最开始使用的那一条语句,但这里指定了一个完全限定的列名。

表名也可以是完全限定的,如下所示:

```mysql
SELECT products.prod_name
FROM crashcourse.products;
```

# 排序检索数据

## 排序数据ORDER

关系数据库设计理论认为,如果不明确规定排序顺序,则不应该假定检索出的数据的顺序有意义。

为了明确地排序用SELECT语句检索出的数据,可使用ORDER BY子,句.ORDER BY子句取一个或多个列的名字,据此对输出进行排序。

```mysql
SELECT prod_name
FROM products
ORDER BY prod_name;
```

## 按多个列排序

为了按多个列排序,只要指定列名,列名之间用逗号分开即可(就像选择多个列时所做的那样)。

```mysql
SELECT prod_id, prod_price, prod_name
FROM products
ORDER BY prod_price, prod_name;
```

## 指定排序方向DESC

数据排序不限于升序排序(从A到Z)。这只是默认的排序顺序,还可以使用ORDER BY子句以降序(从2到A)顺序排序。为了进行降序排序,必须指定DESC关键字。

```mysql
SELECT prod_id, prod_price, prod_name
FROM products
ORDER BY prod_price DESC, prod_name;
```

<u>DESC关键字只应用到直接位于其前面的列名。</u>在上例中,只对prod-price列指定DESC,对prod-name列不指定。因此,prod_price列以降序排序, 而prod-name列(在每个价格内)仍然按标准的升序排序。

使用ORDER BY和LIMIT的组合,能够找出一个列中最高或最低的值。

```mysql
SELECT prod_price
FROM products
ORDER BY prod_price DESC
LIMIT 1;
```

# 过滤数据

数据库表一般包含大量的数据,很少需要检索表中所有行。通常只会根据特定操作或报告的需要提取表数据的子集。只检索所需数据需要指定搜索条件( search criteria ) ,搜索条件也称为过滤条件(filter condition) 。

## 使用WHERE子句

在SELECT语句中,数据根据WHERE子句中指定的搜索条件进行过滤。WHERE子句在表名(FROM子句)之后给出:

```mysql
SELECT prod_name, prod_price
FROM products
WHERE prod_price = 2.50;
```

这条语句从products表中检索两个列,但不返回所有行,只返回prod_price值为2.50的行

## WHERE子句操作符

| 操作符  |        说明        |
| :-----: | :----------------: |
|    =    |        等于        |
|   <>    |       不等于       |
|   !=    |       不等于       |
|    <    |        小于        |
|   <=    |      小于等于      |
|    >    |        大于        |
|   >=    |      大于等于      |
| BETWEEN | 在指定的两个值之间 |

## 检查单个值

 

```mysql
SELECT prod_name, prod_price
FROM products
WHERE prod_name = 'fuses';
```

检查WHERE prod_name= 'fuses'语句,它返回prod-namet值为Fuses的一行。MySQL在执行匹配时默认不区分大小写,所以fuses与Fuses匹配。

## 不匹配检查

```mysql
SELECT vend_id, prod_name
FROM products
WHERE vend_id <> 1003
```

>    何时使用引号	如果仔细观察上述WHERE子句中使用的条件,会看到有的值括在单引号内(如前面使用的'fuses '),而有的值未括起来。单引号用来限定字符串。如果将值与串类型的1列进行比较,则需要限定引号,用来与数值列进行比较的值不用引号。

## 范围值检查BETWEEN X AND Y

为了检查某个范围的值,可使用BETWEEN操作符。

```mysql
SELECT prod_name, prod_price
FROM products
WHERE prod_price BETWEEN 5 AND 10;
```

从这个例子中可以看到,在使用BETWEEN时,必须指定两个值——所需范围的低端值和高端值。这两个值必须用AND关键字分隔。BETWEEN匹配范围中所有的值,包括指定的开始值和结束值。

## 空值检查

在创建表时,表设计人员可以指定其中的列是否可以不包含值。在一个列不包含值时,称其为包含空值NULL

```mysql
SELECT prod_name
FROM products
WHERE prod_price IS NULL;
```

>    NULL与不匹配	在通过过滤选择出不具有特定值的行时,你可能希望返回具有NULL值的行。但是,不行。因为未知具有特殊的含义,数据库不知道它们是否匹配,所以在匹配过滤或不匹配过滤时不返回它们。
>
>    <u>因此,在过滤数据时,一定要验证返回数据中确实给出了被过滤列具有NULL的行。</u>

# 数据过滤

## 组合WHERE子句

### AND操作符

为了通过不止一个列进行过滤,可使用AND操作符给WHERE子句附加条件。

```mysql
SELECT prod_id, prod_price, prod_name
FROM products
WHERE vend_id = 1003 AND prod_price <=10;
```

### OR操作符

OR操作符与AND操作符不同,它指示MySQL检索匹配任一条件的行。

```mysql
SELECT prod_name, prod_price
FROM products
WHERE vend_id = 1002 OR vend_id = 1003;
```

## 计算次序

SQL (像多数语言一样)在处理0R操作符前,优先处理AND操作符。换句话说,由于AND在计算次序中优先级更高,操作符被错误地组合了。

此问题的解决方法是使用圆括号明确地分组相应的操作符。

```mysql
SELECT prod_name, prod_price
FROM products
WHERE (vend_id = 1002 OR vend_id =1003) AND prod_price >=10;
```

## IN操作符

圆括号在WHERE子句中还有另外一种用法。IN操作符用来指定条件范围,范围中的每个条件都可以进行匹配。IN取合法值的由逗号分隔的清单,全都括在圆括号中。

```mysql
SELECT prod_name, prod_price
FROM products
WHERE vend_id IN (1002,1003)
ORDER BY prod_name;
```

此SELECT语句检索供应商1002和1003制造的所有产品。IN操作符后跟由逗号分隔的合法值清单,整个清单必须括在圆括分析号中。

如果你认为IN操作符完成与OR相同的功能,那么你的这种猜测是对的。下面的SQL语句完成与上面的例子相同的工作:

```mysql
SELECT prod_name, prod_price
FROM products
WHERE vend_id = 1002 OR vend_id = 1003
ORDER BY prod_name;
```

其优点具体如下

*    在使用长的合法选项清单时, IN操作符的语法更清楚且更直观。
*    在使用IN时,计算的次序更容易管理(因为使用的操作符更少)。
*    IN操作符一般比OR操作符清单执行更快。
*    IN的最大优点是可以包含其他SELECT语句,使得能够更动态地建立WHERE子句。

>    IN WHERE子句中用来指定要匹配值的清单的关键字,功能与OR相当。

## NOT操作符

WHERE子句中的NOT操作符有且只有一个功能,那就是否定它之后所跟的任何条件。

<u>NOT WHERE子句中用来否定后跟条件的关键字。</u>

```mysql
SELECT prod_name, prod_price
FROM products
WHERE vend_id NOT IN (1002,1003)
ORDER BY prod_name;
```

MySQL支持使用NOT对IN, BETWEEN和EXISTS子句取反,这与多数其他DBMS允许使用NOT对各种条件取反有很大的差别。

# 用通配符进行过滤

>    通配符(wildcard)	用来匹配值的一部分的特殊字符。
>
>    搜索模式(search pattern)	由字面值、通配符或两者组合构成的搜索条件。

## 百分号(%)通配符

最常使用的通配符是百分号(%)。在搜索串中,%表示任何字符出现任意次数。例如,为了找出所有以jet起头的产品,可使用以下SELECT语句:

```mysql
SELECT prod_id, prod_name
FROM products
WHERE prod_name LIKE "%anvil%";
```

搜索模式,%anvil%'表示匹配任何位置包含文本anvil的值,而不论它之前或之后出现什么字符。

## 下划线(_)通配符

另一个有用的通配符是下划线(_)。下划线的用途与%一样,但下划线只匹配单个字符而不是多个字符。

```mysql
SELECT prod_id, prod_name
FROM products
WHERE prod_name LIKE '_ ton anvil';
```

## 使用通配符的技巧

正如所见, MySQL的通配符很有用。但这种功能是有代价的:通配符搜索的处理一般要比前面讨论的其他搜索所花时间更长。这里给出一些使用通配符要记住的技巧。

*    不要过度使用通配符。如果其他操作符能达到相同的目的,应该使用其他操作符。
*    在确实需要使用通配符时,除非绝对有必要,否则不要把它们用在搜索模式的开始处。把通配符置于搜索模式的开始处,搜索起来是最慢的。
*    仔细注意通配符的位置。如果放错地方,可能不会返回想要的数据

# 用正则表达式进行搜索REGEXP

## 基本字符匹配

```mysql
SELECT prod_name
FROM products
WHERE prod_name REGEXP '1000'
ORDER BY prod_name;
```

除关键字LIKE被REGEXP替代外,这条语句看上去非常像使用LIKE的语句,它告诉MySQL: REGEXP后所跟的东西作为正则表达式(与文字正文1000匹配的一个正则表达式)处理。

```mysql
SELECT prod_name
FROM products
WHERE prod_name REGEXP '.000'
ORDER BY prod_name;
```

## 进行OR匹配

为搜索两个串之一(或者为这个串,或者为另一个串),使用|.

```mysql
SELECT prod_name
FROM products
WHERE prod_name REGEXP '1000|2000'
ORDER BY prod_name;
```



## 匹配几个字符之一

匹配任何单一字符。但是,如果你只想匹配特定的字符，可通过指定一组用[和]括起来的字符来完成,如下所示:

```mysql
SELECT prod_name
FROM products
WHERE prod_name REGEXP '[123] Ton'
ORDER BY prod_name;
```

使用了正则表达式[123] Ton, [123]定义一组字符,它的意思是匹配1或2或3,因此, 1 ton和12 ton都匹配且返回(没有3 ton)。

## 匹配范围集合

可用来定义要匹配的一个或多个字符。例如,下面的集合将匹配数字0到9:[0123456789]

为简化这种类型的集合,可使用-来定义一个范围。

```mysql
SELECT prod_name
FROM products
WHERE prod_name REGEXP '[1-5] Ton'
ORDER BY prod_name;
```

## 匹配特殊字符

正则表达式语言由具有特定含义的特殊字符构成。我们已经看到.、[]、|和-等,还有其他一些字符。请问,如果你需要匹配这些字符,应该怎么办呢?例如,如果要找出包含.字符的值,怎样搜索?请看下面的例子:

```mysql
SELECT vend_name
FROM vendors
WHERE vend_name REGEXP '.'
ORDER BY vend_name;
```

为了匹配特殊字符,必须用\\\\为前导。\\\\-表示查找-, \\\\.表示查找.

```mysql
SELECT vend_name
FROM vendors
WHERE vend_name REGEXP '\\.'
ORDER BY vend_name;
```

| 元字符 |   说明   |
| :----: | :------: |
| \\\\f  |   换页   |
| \\\\n  |   换行   |
| \\\\r  |   回车   |
| \\\\t  |   制表   |
| \\\\v  | 纵向制表 |

## 匹配字符类

|     类     |                    说明                    |
| :--------: | :----------------------------------------: |
| [:alnum:]  |               任意字母和数字               |
| [:alpha:]  |                  任意字符                  |
| [:blank:]  |                 空格和制表                 |
| [:cntrl:]  |               ASCII控制字符                |
| [:digit:]  |                  任意数字                  |
| [:graph:]  |       与[:print:]相同，但不包括空格        |
| [:lower:]  |                任意小写字母                |
| [:print:]  |               任意可打印字符               |
| [:punct:]  | 既不在[:alnum:]又不在[:cntrl:]中的任意字符 |
| [:space:]  |         包括空格在内的任意空白字符         |
| [:upper:]  |                任意大写字母                |
| [:xdigit:] |              任意十六进制数字              |

## 匹配多个实例

目前为止使用的所有正则表达式都试图匹配单次出现。如果存在一个匹配,该行被检索出来,如果不存在,检索不出任何行。但有时需要,对匹配的数目进行更强的控制。例如,你可能需要寻找所有的数,不管数中包含多少数字,或者你可能想寻找一个单词并且还能够适应一个尾随的s (如果存在),等等。

| 元字符 |         说明         |
| :----: | :------------------: |
|   *    |    0个或多个匹配     |
|   +    |    1个或多个匹配     |
|   ?    |     0个或1个匹配     |
|  {n}   |    指定数目的匹配    |
|  {n,}  | 不少于指定数目的匹配 |
| {n,m}  |    匹配数目的范围    |

```mysql
SELECT prod_name
FROM products
WHERE prod_name REGEXP '[[:digit:]]{4}'
ORDER BY prod_name;
```

 [:digit:]匹配任意数字,因而它为数字的一个集合。{4}确切地要求它前面的字符(任意数字)出现4次,所以[[:digit:]]{4}匹配连在一起的任意4位数字。

```mysql
SELECT prod_name
FROM products
WHERE prod_name REGEXP '\\([0-9] sticks?\\)'
ORDER BY prod_name;
```

## 定位符

| 元字符  |    说明    |
| :-----: | :--------: |
|    ^    | 文本的开始 |
|   $$    | 文本的结尾 |
| [[:<:]] |  词的开始  |
| [[:>:]] |  词的结尾  |

```mysql
SELECT prod_name
FROM products
WHERE prod_name REGEXP '^[0-9\\.]'
ORDER BY prod_name;
```

# 创建计算字段

## 拼接(Concat)

将值联结到一起构成单个值。解决办法是把两个列拼接起来。在MySQL的SELECT语句中,可使用<u>Concat ()</u>函数来拼接两个列。

```mysql
SELECT Concat(vend_name,' (',vend_country,')')
FROM vendors
ORDER BY vend_name;
```

Concat ()拼接串,即把多个串连接起来形成一个较长的串。

Concat()需要一个或多个指定的串,各个串之间用逗号分隔。

上面的SELECT语句连接以下4个元素:

-    存储在vend-name列中的名字;
-    包含一个空格和一个左圆括号的串;
-    存储在vend_country列中的国家;
-    包含一个右圆括号的串。

```mysql
SELECT Concat(RTrim(vend-name), ' (', RTrim(vend_country), ')')
FROM vendors
ORDER BY vend_name;
```

<u>RTrim()函数去掉值右边的所有空格。</u>通过使用RTrim(),各,个列都进行了整理。

### 使用别名AS

SQL支持列别名。别名(alias)是一个字段或值的替换名。别名用AS关键字赋予。

```mysql
SELECT Concat(RTrim(vend_name),' (',RTrim(vend_country),')') AS
vend_title
FROM vendors
ORDER BY vend_name;
```

## 执行算术计算

| 操作符 | 说明 |
| ------ | ---- |
| +      | 加   |
| -      | 减   |
| *      | 乘   |
| /      | 除   |

# 使用数据处理函数

## 函数

### 使用函数

大多数SQL实现支持以下类型的函数。

-    用于处理文本串(如删除或填充值,转换值为大写或小写)的文本函数。

-    用于在数值数据上进行算术操作(如返回绝对值,进行代数运算)的数值函数。

-    用于处理日期和时间值并从这些值中提取特定成分(例如,返回两个日期之差,检查日期有效性等)的日期和时间函数。

-    返回DBMS正使用的特殊信息(如返回用户登录信息,检查版本细节)的系统函数。

### 文本处理函数

```mysql
SELECT vend_name, Upper(vend_name) AS vend_name_upcase
FROM vendors
ORDER BY vend_name;
```

<u>正如所见, Upper()将文本转换为大写</u>

|    函数    |       说明        |
| :--------: | :---------------: |
|   Left()   | 返回串左边的字符  |
|  Length()  |   返回串的长度    |
|  Locate()  | 找出串的一个子串  |
|  Lower()   |  将串转换为小写   |
|  LTrim()   | 去掉串左边的空格  |
|  Right()   | 返回串右边的字符  |
|  RTrim()   | 去掉串右边的空格  |
| Soundex()  | 返回串的SOUNDEX值 |
| SubSting() |  返回子串的字符   |
|  Upper()   |  将串转换为大写   |

SOUNDEX需要做进一步的解释。SOUNDEX是一个将任何文本串转换为描述其语音表示的字母数字模式的算法。SOUNDEX考虑了类似的发音字符和音节,使得能对串进行发音比较而不是字母比较。虽然SOUNDEX不是SQL概念,但MySQL (就像多数DBMS一样)都提供对SOUNDEX的支持。

```mysql
SELECT cust_name, cust_contact
FROM cunstomers
WHERE Soundex(cust_contact) = 'Y. Lie';
```

## 日期和时间处理函数

| 函数          | 说明                          |
| ------------- | ----------------------------- |
| AddDate()     | 增加一个日期(天、周等)        |
| AddTime()     | 增加一个时间(时、分等)        |
| CurDate()     | 返回当前日期                  |
| CurTime()     | 返回当前时间                  |
| Date()        | 返回日期时间的日期部分        |
| DateDiff()    | 计算两个日期之差              |
| Date_Add ()   | 高度灵活的日期运算函数        |
| Date_Format() | 返回一个格式化的日期或时间串  |
| Day()         | 返回一个日期的天数部分        |
| DayofWeek()   | 对于一个日期,返回对应的星期几 |
| Hour()        | 返回一个时间的小时部分        |
| Minute()      | 返回一个时间的分钟部分        |
| Month()       | 返回一个日期的月份部分        |
| Now()         | 返回当前日期和时间            |
| Second()      | 返回一个时间的秒部分          |
| Time()        | 返回一个日期时间的时间部分返  |
| Year()        | 回一个日期的年份部分函数      |

首先需要注意的是MySQL使用的日期格式。无论你什么时候指定日期,不管是插入或更新表值还是用WHERE子句进行过滤,日期必须为格式yyyy-mm-dd

```mysql
SELECT cust_id, order_num
FROM orders
WHERE Date (order_date) BETWEEN '2005-09-01' AND 2005-09-30';
```

## 数值处理函数

|  函数  |        说明        |
| :----: | :----------------: |
| Abs()  | 返回一个数的绝对值 |
| Cos()  | 返回一个角度的余弦 |
| Exp()  | 返回一个数的指数值 |
| Mod()  |  返回除操作的余数  |
|  Pi()  |     返回圆周率     |
| Rand() |   返回一个随机数   |
| Sin()  | 返回一个角度的正弦 |
| sqrt() | 返回一个数的平方根 |
| Tan()  | 返回一个角度的正切 |

# 汇总数据

### SQL聚集函数

| 函数    | 说明             |
| ------- | ---------------- |
| AVG()   | 返回某列的平均值 |
| COUNT() | 返回某列的行数   |
| MAX()   | 返回某列的最大值 |
| MIN()   | 返回某列的最小值 |
| SUM()   | 返回某列值之和   |

## AVG()

AVG()通过对表中行数计数并计算特定列值之和,求得该列的平均值。AVG()可用来返回所有列的平均值,也可以用来返回特定列或行的平均值。

```mysql
SELECT AVG(prod_price) AS avg_price 
FROM products;
```

此SELECT语句返回值avg_Price,它包含products表中所有产品的平均价格。

## COUNT()

COUNT()函数进行计数。可利用COUNT ()确定表中行的数目或符合特定条件的行的数目。

COUNT ()函数有两种使用方式。

使用COUNT (*)对表中行的数目进行计数,不管表列中包含的是空值(NULL)还是非空值。

使用COUNT (column)对特定列中具有值的行进行计数,忽略NULL值。

```mysql
SELECT COUNT(*) AS numcust
FROM customers;
```

利用COUNT(*)对所有行计数,不管行中各列有什么值。计数值在num_cust中返回。

## MAX()

MAX()返回指定列中的最大值。MAX()要求指定列名

```mysql
SELECT MAX(prod_price) AS max_price
FROM products;
```

MAX()返回products表中最贵的物品的价格。

## MIN()

MIN()的功能正好与MAX ( )功能相反,它返回指定列的最小值。与MAX()一样, MIN ()要求指定列名

```mysql
SELECT MIN(prod price) As minprice
FROM products;
```

MIN()返回products表中最便宜物品的价格。

## SUM()

SUM()用来返回指定列值的和(总计)。

```mysql
SELECT SUM(quantity) As items_ordered
FROM orderitems
WHERE order_num = 20005;
```

函数SUM (quantity)返回订单中所有物品数量之和, WHERE子句保证只统计某个物品订单中的物品。

## 聚集不同值DISTINCT

-    对所有的行执行计算,指定ALL参数或不给参数(因为ALL是默认行为);

-    只包含不同的值,指定DISTINCT参数。

```mysql
SELECT AVG(DISTINCT prod_price) AS avg_price 
FROM products
WHERE vend_id = 1003;
```

## 组合聚集函数

目前为止的所有聚集函数例子都只涉及单个函数。但际上SELECT语句可根据需要包含多个聚集函数。

```mysql
SELECT COUNT() AS numitems 
	MIN(prod_price) AS price_min,
	MAX(prod price) AS price_max,
	AVG(prod price) AS price_avg 
FROM products;
```

# 分组数据

## 创建分组GROUP BY

分组是在SELECT语句的GROUP BY子句中建立的。

```mysql
SELECT vend_id, COUNT(*) AS num_prods
FROM products
GROUP BY vend_id;
```

上面的SELECT语句指定了两个列, vend_id包含产品供应商的ID, num_prods为计算字段(用COUNT (*)函数建立), GROUP BY子句指示MySQL按vend_id排序并分组数据。这导致对每个vendid而不是整个表计算num_prods一次。

在具体使用GROUP BY子句前,需要知道一些重要的规定。

-    GROUP BY子句可以包含任意数目的列。这使得能对分组进行嵌套,为数据分组提供更细致的控制。
-    如果在GROUP BY子句中嵌套了分组,数据将在最后规定的分组上进行汇总。换句话说,在建立分组时,指定的所有列都一起计算(所以不能从个别的列取回数据)。
-    GROUP BY子句中列出的每个列都必须是检索列或有效的表达式(但不能是聚集函数)。如果在SELECT中使用表达式,则必须在GROUP BY子句中指定相同的表达式。不能使用别名。
-    除聚集计算语句外, SELECT语句中的每个列都必须在GROUP BY子句中给出。
-    如果分组列中具有NULL值,则NULL将作为一个分组返回。如果列中有多行NULL值,它们将分为一组。
-    <u>GROUP BY子句必须出现在WHERE子句之后, ORDER BY子句之前。</u>

## 过滤分组HAVING

HAVING非常类似于WHERE,事实上, 目前为止所学过的所有类型的WHERE子句都可以用HAVING来替代。唯一的差别是WHERE过滤行,而HAVING过滤分组。

```mysql
SELECT COUNT(*) AS orders
FROM orders
GROUP BY cust_id
HAVING COUNT(*) >= 2;
```

这条SELECT语句的前3行类似于上面的语句。最后一行增加了HAVING子句,它过滤COUNT (*) >=2 (两个以上的订单)的那些分组。

## 分组和排序

| GROUP BY                                                     | ORDER BY                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 排序产生的输出任意列都可以使用(甚至非选择的列也可以使用)不一定需要 | 分组行。但输出可能不是分组的顺序只可能使用选择列或表达式列,而且必须使用每个选择列表达式如果与聚集函数一起使用列(或表达式) ,则必须使用 |

## SELECT子句顺序

| 子句     | 说明               | 是否必须使用           |
| -------- | ------------------ | ---------------------- |
| SELECT   | 要返回的列或表达式 | 是                     |
| FROM     | 从中检索数据的表   | 仅在从表选择数据时使用 |
| WHERE    | 行级过滤           | 否                     |
| GROUP BY | 分组说明           | 仅在按组计算聚集时使用 |
| HAVING   | 组级过滤           | 否                     |
| ORDER BY | 输出排序顺序       | 否                     |
| LIMIT    | 要检索的行数       | 否                     |

# 使用子查询

## 子查询

SELECT语句是SQL的查询。迄今为止我们所看到的所有SELECT语句都是简单查询,即从单个数据库表中检索数据的单条语句。

## 利用子查询进行过滤

在WHERE子句中使用子查询能够编写出功能很强并且很灵活的SQL语句。对于能嵌套的子查询的数目没有限制,不过在实际使用时由于性能的限制,不能嵌套太多的子查询。

```mysql
SELECT cust_name, cust_contact
FROM customers
WHERE cust_id IN (SELECT cust_id
                  FROM orders
                  WHERE order_num IN (SELECT order_num
                                      FROM orderitems
                                      WHERE prod_id = 'TNT2');
```

## 作为计算字段使用子查询

```mysql
SELECT cust_name cust_state(SELECT COUNT(*)
                            FROM orders
                            WHERE cust_id =cust_id) AS orders
FROM customers 
ORDER BY cust_name;
```

# 联结表

<u>SQL最强大的功能之一就是能在数据检索查询的执行中联结(join)表。</u>联结是利用SQL的SELECT能执行的最重要的操作,很好地理解联结及其语法是学习SQL的一个极为重要的组成部分。

在能够有效地使用联结前,必须了解关系表以及关系数据库设计的一些基础知识。

## 创建联结

联结的创建非常简单,规定要联结的所有表以及它们如何关联即可。

```mysql
SELECT vend_name, prod_name, prod_price
FROM vendors, products
WHERE vendors.vend_id = products.vend_id
ORDER BY vend_name, prod_name:
```

我们来考察一下此代码.SELECT语句与前面所有语句一样指定要检索的列。这里,最大的差别是所指定的两个列(prod-name和prod price)在一个表中,而另一个列(vend-name )在另一个表中。

>    笛卡儿积(cartesian product)	<u>由没有联结条件的表关系返回的结果为笛卡儿积。</u>检索出的行的数目将是第一个表中的行数乘以第二个表中的行数。

## 内部联结INNER JOIN

目前为止所用的联结称为<u>等值联结</u>(equijoin),它基于两个表之间的"相等测试。这种联结也称为内部联结。其实,对于这种联结可以使用稍微不同的语法来明确指定联结的类型。

```mysql
SELECT vend_name, prod_name, prod_price
FROM vendors INNER JOIN products
ON vendors.vend_id = products.vend_id;
```

在使用这种语法时,联结条件用特定的ON子句而不是WHERE子句给出。传递给ON的实际条件与传递给WHERE的相同。

## 联结多个表

SQL对一条SELECT语句中可以<u>联结的表的数目没有限制</u>。创建联结的基本规则也相同。首先列出所有表,然后定义表之间的关系。

```mysql
SELECT prod_name, vend_name, prod_price, quantity
FROM orderitems, products, vendors
WHERE products.vend_id = vendors.vend_id
AND orderitems.prod_id = products.prod_id 
AND order_num = 20005;
```

# 创建高级联结

## 使用表别名AS

别名除了用于列名和计算字段外, SQL还允许给表名起别名。这样做有两个主要理由:

-    缩短SQL语句;

-    允许在单条SELECT语句中多次使用相同的表。

```mysql
SELECT cust_name, cust_contact
FROM customers AS c, orders AS o, orderitems AS oi
WHERE c.cust_id=o.cust_id
AND oi.order_num = o.order_num
AND prod_id='TNT2';
```

## 使用不同类型的联结

### 自联结

使用表别名的主要原因之一是能在单条SELECT语句中不止一次引用相同的表。

```mysql
SELECT p1.prod_id, p1.prod_name
FROM products AS p1, products AS p2
WHERE p1.vend_id =p2.vend_id
AND p2.prod_id = 'DTNTR';
```

此查询中需要的两个表实际上是相同的表,因此products表在FROM子句中出现了两次。虽然这是完全合法的,但<u>对products的引用具有二义性</u>,因为MySQL不知道你引用的是products表中的哪个实例。为解决此问题,使用了表别名。products的第一次出现为别名p1,第二次出现为别名p2,现在可以将这些别名用作表名。

### 自然联结

无论何时对表进行联结,应该至少有一个列出现在不止一个表中(被联结的列)。<u>标准的内部联结返回所有数据,甚至相同的列多次出现。<u>自然联结排除多次出现,使每个列只返回一次。</u>

自然联结是这样一种联结,其中你只能选择那些唯一的列。这一般是通过对表使用通配符(SELECT *),对所有其他表的列使用明确的子集来完成的。

```mysql
SELECT C.*, o.order_num, o.order_date,
	oi.prod_id, oi.quantity, oi.item_price
FROM customers AS c, orders AS o, orderitems AS oi
WHERE c.cust_id = o.cust_id
AND oi.order_num=o.order_num
AND prod_id= 'FB';
```

### 外部联结OUTER JOIN

许多联结将一个表中的行与另一个表中的行相关联。但有时候会需要包含没有关联行的那些行。

外部联结使用了关键字OUTER JOIN来指定联结的类型(而不是在WHERE子句中指定)。但是,与内部联结关联两个表中的行不同的是,外部联结还包括没有关联行的行。在使用OUTER JOIN语法时,必须使用RIGHT或LEFT关键字指定包括其所有行的表(<u>RIGHT指出的是OUTER JOIN右边的表,而LEFT指出的是OUTER JOIN左边的表</u>)。

```mysql
SELECT customers.cust_id, orders.order_num
FROM customers LEFT OUTER JOIN orders
ON customers.cust_id = orders.cust_id;
```

```mysql
SELECT customers.cust_id, orders.order_num
FROM customers RIGHT OUTER JOIN orders
ON orders.cust_id = customers.cust_id;
```

## 使用带聚集函数的联结COUNT()

```mysql
SELECT customers.cust_name, 
	customers.cust_id,
	COUNT(orders.order_num) AS num_ord
FROM customers INNER JOIN orders
ON customers.cust_id = orders.cust_id
GROUP BY customers.cust_id;
```

```mysql
SELECT customers.cust_name,
	customers.cust_id,
	COUNT (orders.order_num) AS num_ord
FROM customers LEFT OUTER JOIN orders
ON customers.cust_id = orders.cust_id
GROUP BY customers.cust_id;
```

## 使用联结和联结条件

-    注意所使用的联结类型。一般我们使用内部联结,但使用外部联结也是有效的。
-    保证使用正确的联结条件,否则将返回不正确的数据。
-    应该总是提供联结条件,否则会得出笛卡儿积。
-    在一个联结中可以包含多个表,甚至对于每个联结可以采用不同的联结类型。虽然这样做是合法的,一般也很有用,但应该在一起测试它们前,分别测试每个联结。这将使故障排除更为简单。t