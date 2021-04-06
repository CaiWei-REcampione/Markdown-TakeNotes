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

# 组合查询

多数SQL查询都只包含从一个或多个表中返回数据的单条SELECT语句。MySQL也允许执行多个查询(多条SELECT语句),并将结果作为单个查询结果集返回。这些组合查询通常称为并(union )或复合查询(compound query)。

有两种基本情况,其中需要使用组合查询:

-    在单个查询中从不同的表返回类似结构的数据

-    对单个表执行多个查询,按单个查询返回数据

## 组合查询UNION

可用<u>UNION</u>操作符来组合数条SQL查询。利用UNION,可给出多条SELECT语句,将它们的结果组合成单个结果集。

```mysql
SELECT vend_id, prod_id, prod_price
FROM products
WHERE prod_price <= 5;
```

```mysql
SELECT vend_id, prod_id, prod_price
FROM products
WHERE vend id IN (1001, 1002);
```

为了组合这两条语句,按如下进行:

```mysql
SELECT vend_id, prod_id, prod_price
FROM products
WHERE prod_price <= 5
UNION
SELECT vend_id, prod_id, prod_price
FROM products
WHERE vend_id IN (1001,1002);
```

### UNION规则

正如所见,并是非常容易使用的。但在进行并时有几条规则需要注意。

-    UNION必须由两条或两条以上的SELECT语句组成,语句之间用关键字UNION分隔(因此,如果组合4条SELECT语句,将要使用3个UNION关键字)。
-    <u>UNION中的每个查询必须包含相同的列、表达式或聚集函数(不过各个列不需要以相同的次序列出)。</u>
-    列数据类型必须兼容:类型不必完全相同,但必须是DBMS可以隐含地转换的类型(例如,不同的数值类型或不同的日期类型)。如果遵守了这些基本规则或限制,则可以将并用于任何数据检索任务。

### 包含或取消重复的行UNION ALL

UNION从查询结果集中自动去除了重复的行(换句话说,它的行为与单条SELECT语句中使用多个WHERE子句条件一样)。

```mysql
SELECT vend_id, prod_id, prod_price
FROM products
WHERE prod price <= 5
UNION ALL
SELECT vend_id, prod_id, prod_price
FROM products
WHERE vend_id IN (1001,1002);
```

>    UNION与WHERE	UNION几乎总是完成与多个WHERE条件相同的工作. UNION ALL为UNION的一种形式,它完成WHERE子句完成不了的工作。如果确实需要每个条件的匹配行全部出现(包括重复行),则必须使用UNION ALL而不是WHERE.

### 对组合查询结果排序ORDER BY

SELECT语句的输出用ORDER BY子句排序。<u>在用UNION组合查询时,只能使用一条ORDER BY子句,它必须出现在最后一条SELECT语句之后。</u>对于结果集,不存在用一种方式排序一部分,而又用另一种方式排序另一部分的情况,因此不允许使用多条ORDER BY子句。

```mysql
SELECT vend_id, prod_id, prod_price
FROM products
WHERE prod price <= 5
UNION
SELECT vend_id, prod_id, prod_price
FROM products
WHERE vend id IN (1001,1002)
ORDER BY vend_id, prod_price;
```

# 全文本搜索

## 启用全文本搜索支持

般在创建表时启用全文本搜索。CREATE TABLE语句接受FULLTEXT子句,它给出被索引列的一个逗号分隔的列表。

## 进行全文本搜索Match() Against()

在索引之后,使用两个函数<u>Match ()</u>和<u>Against ()</u>执行全文本搜索,其中

-    Match()指定被搜索的列,
-    Against()指定要使用的搜索表达式

```mysql
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against ('rabbit');
```

此SELECT语句检索单个列note_text。由于WHERE子句,一全文本搜索被执行。Match (note-text)指示MySQL针对指定的列进行搜索, Against ('rabbit')指定词rabbit作为搜索文本。由于有两行包含词rabbit,这两个行被返回。

<u>搜索不区分大小写 除非使用BINARY方式否则全文本搜索不区分大小写。</u>

事实是刚才的搜索可以简单地用LIKE子句完成,如下所示

```mysql
SELECT note_text
FROM productnotes
WHERE note_text LIKE '%rabbit%';
```

## 使用查询扩展

查询扩展用来设法<u>放宽所返回的全文本搜索结果的范围</u>。

这也是查询扩展的一项任务。在使用查询扩展时, MySQL对数据和索引进行两遍扫描来完成搜索:

*    首先,进行一个基本的全文本搜索,找出与搜索条件匹配的所有行
*    其次, MySQL检查这些匹配行并选择所有有用的词(我们将会简要地解释MySQL如何断定什么有用,什么无用)。
*    再其次, MySQL再次进行全文本搜索,这次不仅使用原来的条件,而且还使用所有有用的词。

```mysql
SELECT note_text
FROM productnotes
WHERE Match(note-text) Against('anvils' WITH QUERY EXPANSION);
```

## 布尔文本搜索IN BOOLEAN MODE

MySQL支持全文本搜索的另外一种形式,称为布尔方式(booleanmode)。

*    要匹配的词;
*    要排斥的词(如果某行包含这个词,则不返回该行,即使它包含其他指定的词也是如此)
*    排列提示(指定某些词比其他词更重要,更重要的词等级更高)
*    表达式分组
*    另外一些内容

```mysql
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('heavy -rope*' IN BOOLEAN MODE);
```

这次只返回一行。这一次仍然匹配词heavy,但-rope* 明确地指示MySQL排除包含rope* (任何以rope开始的词,包括ropes)的行

| 布尔操作符 | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| +          | 包含,词必须存在                                              |
| -          | 排除,词必须不出现                                            |
| >          | 包含,而且增加等级值                                          |
| <          | 包含,且减少等级值                                            |
| ()         | 把词组成子表达式(允许这些子表达式作为一个组被包含、排除、排列等) |
| ~          | 取消一个词的排序值                                           |
| *          | 词尾的通配符                                                 |
| ""         | 定义一个短语(与单个词的列表不一样,它匹配整个短语以便包含或排除这个短语) |

```mysql
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('+rabbit +bait' IN BOOLEAN MODE);
```

这个搜索匹配包含词rabbit和bait的行。

---

```mysql
SELECT note_text
FROM productnotes
WHERE Match(notetext) Against ('rabbit bait' IN BOOLEAN MODE);
```

没有指定操作符,这个搜索匹配包含rabbit和bait中的至少一个词的行。

---

```mysql
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('"rabbit bait"' IN BOOLEAN MODE);
```

这个搜索匹配短语rabbit bait而不是匹配两个词rabbit和bait.

---

```mysql
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('>rabbit <carrot' IN BOOLEAN MODE);
```

匹配rabbit和carrot,增加前者的等级,降低后者的等级。

---

```mysql
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('+safe +(<combination)' IN BOOLEAN MODE);
```

这个搜索匹配词safe和combination,降低后者的等级。

# 插入数据

## 数据插入INSERT

顾名思义, INSERT是用来插入(或添加)行到数据库表的。插入可以用几种方式使用:

*    插入完整的行;
*    插入行的一部分:
*    插入多行;
*    插入某些查询的结果。

## 插入完整的行INSERT INTO

把数据插入表中的最简单的方法是使用基本的INSERT语法,它要求指定表名和被插入到新行中的值。

```mysql
INSERT INTO customers(cust_name,
                      cust_contact,
                      cust_emai1,
                      cust_address,
                      cust_city,
                      cust_state,
                      cust_zip, 
                      cust_country)
                      VALUES('Pep E. LaPew',
                             NULL,
                             NULL,
                             '100 Main Street',
                             'Los Angeles',
                             'CA",
                             '90046',
                             'USA');
```

## 插入多个行

```mysql
INSERT INTO customers(cust_name,
                      cust_address,
                      cust_city,
                      cust_state,
                      cust_zip,
                      cust_country)
                      VALUES('Pep E. LaPew',
                             '100 Main Street',
                             'Los Angeles',
                             'CA',
                             '90046',
                             'USA'
                            ),
                            ('M. Martian',
                             '42 Galaxy way',
                             'New York',
                             'NY',
                             '11213',
                             'USA'
                            ):
```

## 插入检索出的数据INSERT SELECT

```mysql
INSERT INTO customers(cust_id,
                      cust_contact,
                      cust_email,
                      cust_name,
                      cust_address,
                      cust_city,
                      cust_state,
                      cust_zip,
                      cust_country)
                      SELECT cust_id,
                     cust_contact,
                     cust_email,
                     cust_name,
                     cust_address,
                     cust_city,
                     cust_state,
                     cust_zip, 
                     cust_country 
                FROM custnew;
```

这个例子使用INSERT SELECT从custnew中将所有数据导入customers. SELECT语句从custnew检索出要插入的值,而不是列出它们。SELECT中列出的每个列对应于customers表名后所跟的列表中的每个列。这条语句将插入多少行有赖于custnew表中有多少行。如果这个表为空,则没有行被插入(也不产生错误,因为操作仍然是合法的)。如果这个表确实含有数据,则所有数据将被插入到customers。

# 更新和删除数据

## 更新数据UPDATE SET

为了更新(修改)表中的数据,可使用UPDATE语句。可采用两种方式使用UPDATE:

-    更新表中特定行
-    更新表中所有行

基本的UPDATE语句由3部分组成,分别是:

*    要更新的表;
*    列名和它们的新值
*    确定要更新行的过滤条件

```mysql
UPDATE customers
SET cust_email = 'elmer@fudd.com'
WHERE cust_id =10005;
```

```mysql
UPDATE customers
SET cust_name = 'The Fudds',
cust_email = 'elmer@fudd. com'
WHERE cust_id = 10005;
```

在更新多个列时,只需要使用单个SET命令,每个“列-值”对之间用逗号分隔(最后一列之后不用逗号)。

## 删除数据DELETE

为了从一个表中删除(去掉)数据,使用DELETE语句。可以两种方式使用DELETE:

*    从表中删除特定的行;
*    从表中删除所有行。

```mysql
DELETE FROM customers 
WHERE cust_id =10006;
```

## 更新和删除的指导原则

下面是许多SQL程序员使用UPDATE或DELETE时所遵循的习惯。

*    除非确实打算更新和删除每一行,否则绝对不要使用不带WHERE子句的UPDATE或DELETE语句。
*    保证每个表都有主键,尽可能像WHERE子句那样使用它(可以指定各主键、多个值或值的范围)。
*    UPDATE或DELETE使用WHERE子句前,应该先用SELECT进行测试,保证它过滤的是正确的记录,以防编写的WHERE子句不正确。
*    使用强制实施引用完整性的数据库,这样MysQL将不允许删除具有与其他表相关联的数据的行。

# 创建和操纵表

## 创建表CREATE TABLE

MySQL不仅用于表数据操纵,而且还可以用来执行数据库和表的所有操作,包括表本身的创建和处理。

一般有两种创建表的方法:

-    使用具有交互式创建和管理表的工具;
-    表也可以直接用MySQL语句操纵。

为了用程序创建表,可使用SQL的CREATE TABLE语句。

```mysql
CREATE TABLE customers 
(
    cust_id int NOT NULL AUTO_INCREMENT,
    cust_name char (50) NOT NULL, 
    cust_address char(50) NULL, 
    cust-city char(50) NULL, 
    cust_state char(5) NULL, 
    cust_zipchar(10) NULL,
    cust_country char(50) NULL, 
    cust_contact char(50) NULL, 
    cust_email char(255) NULL,
    PRIMARY KEY (cust_id)
) ENGINE-InnoDB;
```

## 使用NULL值

NULL值就是没有值或缺值。允许NULL值的列也允许在插入行时不给出该列的值。不允许NULL值的列不接受该列没有值的行,换句话说,在插入或更新行时,该列必须有值。每个表列或者是NULL列,或者是NOT NULL列,这种状态在创建时由表的定义规定。

```mysql
CREATE TABLE orders 
(
    order_num int NOT NULL AUTO_INCREMENT,
    order_date datetime NOT NULL, 
    custid int NOT NULL,
    PRIMARY KEY (order_num)
)ENGINE=InnoDB;
```

```mysql
CREATE TABLE vendors
(
    vend_id int NOT NULL AUTO_INCREMENT, 
    vend_name char(50) NOT NULL,
    vend_address char(50) NULL,
    vend_city char(50) NULL,
    vend_state char(5) NULL,
    vend_zip char(10) NULL,
    vend_country char(50) NULL,
    PRIMARY KEY (vend_id)
) ENGINE=InnoDB;
```

NOT NULL将阻止插入没有值的列。如果试图插入没有值的列,将返回错误,且插入失败。

## 主键PRIMARY KEY

再介绍正如所述,主键值必须唯一。即,表中的每个行必须具有唯一的主键值。如果主键使用单个列,则它的值必须唯一。

如果使用多个列,则这些列的组合值必须唯一。

迄今为止我们看到的CREATE TABLE例子都是用单个列作为主键。其中主键用以下的类似的语句定义:

```mysql
PRIMARY KEY (vend_id)
```

为创建由多个列组成的主键,应该以逗号分隔的列表给出各列名

```mysql
CREATE TABLE orderitems
(
    order_num intNOT NULL,
    order_item int NOT NULL,
    prod_id char(10) NOT NULL, 
    quantity intNOT NULL,
    item_price decimal (8,2) NOT NULL, 
    PRIMARY KEY (order_num, order_item)
) ENGINE=InnoDB;
```

## 使用AUTO_INCREMENT

```mysql
cust_id int NOT NULL AUTO_INCREMENT,
```

AUTO-INCREMENT告诉MySQL,本列每当增加一行时自动增量。每次执行一个INSERT操作时, MySQL自动对该列增量(从而才有这个关键字AUTO_INCREMENT),给该列赋予下一个可用的值。这样给每个行分配一个唯一的cust_id,从而可以用作主键值。

## 指定默认值DEFAULT

```mysql
CREATE TABLE orderitems
(
    order_num int NOT NULL,
    order_item int NOT NULL，
    prod-id char(10) NOT NULL，
    quantity int NOT NULL DEFAULT 1,
    item_price decimal(8,2) NOT NULL，
    PRIMARY KEY (order_num, order_item)
)ENGINE=InnoDB;
```

## 引擎类型

迄今为止使用的CREATE TABLE语句全都以ENGINE=InnoDB语句结束。

与其他DBMS一样, MysQL有一个具体管理和处理数据的内部引擎。在你使用CREATE TABLE语句时,该引擎具体创建表,而在你使用SELECT语句或进行其他数据库处理时,该引擎在内部处理你的请求。

多数时候,此引擎都隐藏在DBMS内,不需要过多关注它。但MySQL与其他DBMS不一样,它具有多种引擎。它打包多个引擎,这些引擎都隐藏在MySQL,执行CREATE TABLE和SELECT等命令。多种引擎具有各自不同的功能和特性,为不同的任务选择正确的引擎能获得良好的功能和灵活性。

-    InnoDB是一个可靠的事务处理引擎,它不支持全文本搜索;
-    MEMORY在功能等同于MyISAM,但由于数据存储在内存(不是磁盘)中,速度很快(特别适合于临时表)
-    MyISAM是一个性能极高的引擎,它支持全文本搜索,但不支持事务处理。

>    外键不能跨引擎混用引擎类型有一个大缺陷。外键不能跨引擎,即使用一个引擎的表不能引用具有使用不同引擎的表的外键。

## 更新表ALTER TABLE

为了使用ALTER TABLE更改表结构,必须给出下面的信息:

在ALTER TABLE之后给出要更改的表名(该表必须存在,否则将出错);

给表添加一个列

```mysql
ALTER TABLE vendors 
ADD vend_phone CHAR(20);'
```

删除刚刚添加的列

```mysql
ALTER TABLE Vendors 
DROP COLUMN vend_phone;
```

## 删除表DROP TABLE

```mysql
DROP TABLE customers2;
```

## 重命名表RENAMA TABLE

```mysql
RENAME TABLE customers2 TO customers;
```

# 使用视图

视图是虚拟的表。与包含数据的表不一样,视图只包含使用时动态检索数据的查询。

-    重用SQL语句。
-    简化复杂的SQL操作。在编写查询后,可以方便地重用它而不必知道它的基本查询细节。
-    使用表的组成部分而不是整个表。
-    保护数据。可以给用户授予表的特定部分的访问权限而不是整个表的访问权限。
-    更改数据格式和表示。视图可返回与底层表的表示和格式不同的数据。

## 视图的规则和限制

下面是关于视图创建和使用的一些最常见的规则和限制。

-    与表一样,视图必须唯一命名(不能给视图取与别的视图或表相同的名字)。
-    对于可以创建的视图数目没有限制。
-    为了创建视图,必须具有足够的访问权限。这些限制通常由数据库管理人员授予。
-    视图可以嵌套,即可以利用从其他视图中检索数据的查询来构造个视图。
-    ORDER BY可以用在视图中,但如果从该视图检索数据SELECT中也含有ORDER BY,那么该视图中的ORDER BY将被覆盖。
-    视图不能索引,也不能有关联的触发器或默认值。
-    视图可以和表一起使用。

## 使用视图CREATE VIEW

-    视图用CREATE VIEW语句来创建。使用SHOW CREATE VIEW viewname;来查看创建视图的语句。
-    用DROP删除视图,其用法为DROP VIEW viewname
-    更新视图时,可以先用DROP再用CREATE,可以直接用CREATEOR REPLACE VIEW。如果要更新的视图不存在,则第2条更新语句会创建一个视图;如果要更新的视图存在,则第2条更新语句会替换原有视图。

```mysql
CREATE VIEW productcustomers AS
SELECT cust_name, cust_contact, prod_id
FROM customers, orders, orderitems
WHERE customers.cust_id = orders.cust_id 
AND orderitems.order_num = orders.order_num;
```

视图极大地简化了复杂SQL语句的使用。利用视图,可一次性编写基础的SQL,然后根据需要多次使用。

## 用视图重新格式化检索出的数据

```mysql
SELECT Concat(RTrim(vendname), ' (', RTrim(vend_country), ')') 
AS vend_title
FROM vendors
ORDER BY vend name;
```

```mysql
CREATE VIEW vendorlocations AS
SELECT Concat (RTrim(vend_name), ' (', RTrim(vend_country), ')')
AS vend_title
FROM vendors
ORDER BY vend_name;
```

## 用视图过滤不想要的数据WHERE IS NOT

```mysql
CREATE VIEW customeremaillist AS
SELECT cust_id, cust_name, cust_email
FROM customers
WHERE cust_email IS NOT NULL;
```

## 使用视图与计算字段

```mysql
SELECT prod_id, 
	quantity,
	item_price,
	quantity*item_price AS expanded_price 
FROM orderitems
WHERE order_num = 20005;
```

转换为一个视图

```mysql
CREATE VIEW orderitemsexpanded AS 
SELECT order_num,
	prod_id,
	quantity,
	item_price,
	quantity*item_price AS expanded_price 
FROM orderitems;
```

```mysql
SELECT *
FROM orderitemsexpanded
WHERE order_num = 20005;
```

## 更新视图

通常,视图是可更新的(即,可以对它们用INSERT, UPDATE和DELETE)。更新一个视图将更新其基表。如果你对视图增加或删除行,实际上是对其基表增加或删除行。

但是,并非所有视图都是可更新的。基本上可以说,如果MySQL不能正确地确定被更新的基数据,则不允许更新(包括插入和删除)。这实际上意味着,如果视图定义中有以下操作,则不能进行视图的更新:

-    分组(使用GROUP BY和HAVING);
-    联结;
-    子查询:
-    并;
-    聚集函数(Min()、Count ()、Sum()等);
-    DISTINCT;
-    导出(计算)列。

# 使用存储过程PROCEDURE

-    通过把处理封装在容易使用的单元中,简化复杂的操作。
-    由于不要求反复建立一系列处理步骤,这保证了数据的完整性。如果所有开发人员和应用程序都使用同一(试验和测试)存储过程,则所使用的代码都是相同的。这一点的延伸就是防止错误。需要执行的步骤越多,出错的可能性就越大。防止错误保证了数据的一致性。
-    简化对变动的管理。如果表名、列名或业务逻辑(或别的内容)有变化,只需要更改存储过程的代码。使用它的人员甚至不需要知道这些变化。这一点的延伸就是安全性。通过存储过程限制对基础数据的访问减少了数据讹误(无意识的或别的原因所导致的数据讹误)的机会。
-    提高性能。因为使用存储过程比使用单独的SQL语句要快。
-    存在一些只能用在单个请求中的MySQL元素和特性,存储过程可以使用它们来编写功能更强更灵活的代码

## 执行存储过程CALL

MySQL称存储过程的执行为调用,因此MySQL执行存储过程的语句为CALL, CALL接受存储过程的名字以及需要传递给它的任意参数。

```mysql
CALL productpricing(
    @pricelow,
    @pricehigh,
    @priceaverage
);
```

## 创建存储过程CREATE PROCEDURE BEGIN END

```mysql
CREATE PROCEDURE productpricing()
BEGIN
	SELECT Avg(prod_price) AS priceaverage
	FROM products;
END;
```

## 删除存储过程DROP PROCEDURE

```mysql
DROP PROCEDURE productpricing;
```

>    仅当存在时删除	如果指定的过程不存在,则DROPPROCEDURE将产生一个错误。当过程存在想删除它时(如果过程不存在也不产生错误)可使用DROP PROCEDURE IF EXISTS.

## 使用参数

```mysql
CREATE PROCEDURE productpricing(
    OUT pl DECIMAL(8, 2),
    OUT ph DECIMAL(8, 2),
    OUT pa DECIMAL(8, 2)
)
BEGIN
SELECT Min(prod_price)
INTO p1
FROM products;
SELECT Max(prod_price)
INTO ph
FROM products;
SELECT Avg(prod_price)
INTO pa
FROM products;
END
```

关键字OUT指出相应的参数用来从存储过程传出一个值(返回给调用者),MySQL支持IN (传递给存储过程)、OUT (从存储过程传出,如这里所用)和INOUT (对存储过程传入和传出)类型的参数。存储过程的代码位于BEGIN和END语句内,如前所见,它们是一系列SELECT语句,用来检索值,然后保存到相应的变量(通过指定INTO关键字)。

```mysql
CALL productpricing(
    @pricelow,
    @pricehigh,
    @priceaverage
);
```

## 建立智能存储过程

```mysql
-- Name: ordertotal
-- Parameters: onumber = order number
--                       taxable =0 if not taxable, 1 if taxable
--                       ototal = order total variable

CREATE PROCEDURE ordertotal(
    IN onumber INT,
    IN taxable BOOLEAN,
    OUT ototal DECIMAL (8,2)
) COMMENT 'Obtain order total, optionally adding tax' 
BECIN

	-- Declare variable for total
    DECLARE total DECIMAL (8,2);
    -- Declare tax percentage 
    DECLARE taxrate INT DEFAULT 6;
    
    -- Get the order totalSELECT 
    Sum(item price*quantity) 
    FROM orderitems
    WHERE order num = onumber 
    INTO total;
    
    -- Is this taxable?
    IF taxable THEN
    	-- Yes, so add taxrate to the total
    	SELECT total+(total/100*taxrate) INTO total;
    END IF;
    
    -- And finally, save to out variable 
    SELECT total INTO ototal;
END:
```

```mysql
CALL ordertotal (20005, o, @total);
SELECT @total;
```

## 检查存储过程SHOW

为显示用来创建一个存储过程的CREATE语句,用SHOW CREATEPROCEDURE 语句:

```mysql
SHOW CREATE PROCEDURE ordertota1;
```

# 使用游标

## 创建游标DECLARE CURSOR FOR SELECT FROM

游标用DECLARE语句创建, DECLARE命名游标,并定义相应的SELECT语句,根据需要带WHERE和其他子句。

```mysql
CREATE PROCEDURE processorders()
BEGIN
	DECLARE ordernumbers CURSOR
	FOR
	SELECT order_num FROM orders;
END;
```

## 打开和关闭游标OPEN CLOSE

游标用OPEN CURSOR语句来打开:

```mysql
OPEN ordernumbers;
```

游标处理完成后,应当使用如下语句关闭游标:

```mysql
CLOSE ordernumbers;
```

## 使用游标数据FETCH

在一个游标被打开后,可以使用FETCH语句分别访问它的每一行。FETCH指定检索什么数据(所需的列),检索出来的数据存储在什么地方。它还向前移动游标中的内部行指针,使下一条FETCH语句检索下一行(不重复读取同一行)。

```mysql
CREAJE PROCEDURE processorders() 
BEGIN
	-- Declare local variables 
	DECLARE o INT;
	
	-- Declare the cursor
	DECLARE ordernumbers CURSOR 
	FOR
	SELECT order_num FROM orders;
	
	-- Open the cursor 
	OPEN ordernumbers;
	
	-- Get order number
	FETCH ordernumbers INTO o;
	
	-- Close the cursor 
	CLOSE ordernumbers;
END;
```

```mysql
CREATE PROCEDURE processorders() 
BEGIN

	-- Declare local variables 
	DECLARE done BOOLEAN DEFAULT 0;
	DECLARE o INT;
	
	-- Declare the cursor 
	DECLARE ordernumbers CURSOR
	FOR
	SELECT order_num FROM orders;
	
	-- Declare continue handler
	DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET done=1;
	
	-- Open the cursor 
	OPEN ordernumbers;
	
	-- Loop through all rows 
	REPEAT
	
		-- Get order number
		FETCH ordernumbers INTO o;
		
	-- End of 1oop
	UNTIL done END REPEAT;
	
	-- Close the cursor 
	CLOSE ordernumbers;

END;
```

# 触发器TRIGGER

## 创建触发器CREATE TRIGGER AFTER ON

在创建触发器时,需要给出4条信息:

-    唯一的触发器名:
-    触发器关联的表;
-    触发器应该响应的活动(DELETE, INSERT或UPDATE);
-    触发器何时执行(处理之前或之后)。

```mysql
CREATE TRIGGER newproduct AFTER INSERT ON products 
FOR EACH ROW SELECT 'Product added';
```

CREATE TRIGGER用来创建名为newproduct的新触发器。触发器可在一个操作发生之前或之后执行,这里给出了AFTER INSERT,所以此触发器将在INSERT语句成功执行后执行。这个触发器还指定FOR EACH ROW,因此代码对每个插入行执行。

## 删除触发器DROP TRIGGER

为了删除一个触发器,可使用DROP TRIGGER语句,如下所示:

```mysql
DROP TRIGGER newproduct;
```

## 使用触发器

### INSERT触发器CREATE TRIGGER AFTER INSERT ON

-    在INSERT触发器代码内,可引用一个名为NEW的虚拟表,访问被插入的行;
-    在BEFORE INSERT触发器中, NEW中的值也可以被更新(允许更改被插入的值);
-    对于AUTO_INCREMENT列, NEW在INSERT执行之前包含0,在INSERT执行之后包含新的自动生成值。

```mysql
CREATE TRIGGER neworder AFTER INSERT ON orders 
FOR EACH ROW SELECT NEW.order_num;
```

### DELETE触发器

# 管理事务处理

事务处理( transaction processing)可以用来维护数据库的完整性,它保证成批的MySQL操作要么完全执行,要么完全不执行.

>    事务(transaction)指一组SQL语句;
>
>    回退(ro1lback)指撤销指定SQL语句的过程;
>
>    提交(commit)指将未存储的SQL语句结果写入数据库表;
>
>    保留点(savepoint)指事务处理中设置的临时占位符(placeholder),你可以对它发布回退(与回退整个事务处理不同)。

## 控制事务处理

MysQL使用下面的语句来标识事务的开始:

```mysql
START TRANSACTION
```

### 使用ROLLBACK

MysQL的ROLLBACK命令用来回退(撤销) MySQL语句

```mysql
SELECT FROM ordertotals;
START TRANSACTION;
DELETE FROM ordertotals;
SELECT FROM * ordertotals;
ROLLBACK;
SELECT * FROM ordertotals;
```

### 使用COMMIT

一般的MySQL语句都是直接针对数据库表执行和编写的。这就是所谓的隐含提交(implicit commit),即提交(写或保存)操作是自动进行的。

<u>但是,在事务处理块中,提交不会隐含地进行。</u>为进行明确的提交,使用COMMIT语句,如下所示:

```mysql
START TRANSACTION;
DELETE FROM orderitems WHERE order_num = 20010;
DELETE FROM orders WHERE order_num = 20010;
COMMIT;
```

### 使用保留点SAVEPOINT ROLLBACK TO

简单的ROLLBACK和COMMIT语句就可以写入或撤销整个事务处理。,但是,只是对简单的事务处理才能这样做,更复杂的事务处理可能需要部分提交或回退。

为了支持回退部分事务处理,必须能在事务处理块中合适的位置放置占位符。这样,如果需要回退,可以回退到某个占位符。

这些占位符称为保留点。为了创建占位符,可如下使用SAVEPOINT语句:

```mysql
SAVEPOINT delete1;
```

```mysql
ROLLBACK TO deletel;
```

## 更改默认的提交行为

```mysql
SET autocommit=0;
```

# 全球化和本地化

数据库表被用来存储和检索数据。不同的语言和字符集需要以不同的方式存储和检索。因此, MySQL需要适应不同的字符集(不同的字母和字符),适应不同的排序和检索数据的方法。

## 字符集和校对顺序

显示所有可用的字符集以及每个字符集的描述和默认校对

```mysql
SHOW CHARACTER SET;
```

查看所支持校对的完整列表

```mysql
SHOW COLLATION;
```

# 安全管理

## 访问控制ROOT

不要使用root 应该严肃对待root登录的使用。仅在绝对需,要时使用它(或许在你不能登录其他管理账号时使用),<u>不应该在日常的MySQL操作中使用root</u>.

## 管理用户USE

MySQL用户账号和信息存储在名为mysql的MySQL数据库中。一般不需要直接访问mysql数据库和表(你稍后会明白这一点),但有时需要直接访问。需要直接访问它的时机之一是在需要获得所有用户账号列表时。为此,可使用以下代码:

```mysql
USE mysql;
SELECT user FROM user;
```

## 创建用户账号CREATE USER

```mysql
CREATE USER ben IDENTIFIED BY 'p@$$word'
```

## 删除用户账号DROP USER

```mysql
DROP USER bforta;
```

## 设置访问权限GRANT

为看到赋予用户账号的权限,使用<u>SHOW GRANTS FOR</u>

```mysql
SHOW GRANTS FOR bforta;
```

为设置权限,使用GRANT语句。

GRANT要求你至少给出以下信息:

-    要授予的权限
-    被授予访问权限的数据库或表
-    用户名

```mysql
GRANT SELECT ON crashcourse.* TO bforta;
```

GRANT的反操作为REVOKE,用它来撤销特定的权限

```mysql
REVOKE SELECT ON crashcourse.* FROM bforta;
```



|          权限           |                             说明                             |
| :---------------------: | :----------------------------------------------------------: |
|           ALL           |                  除GRANT OPTION外的所有权限                  |
|          ALTER          |                       使用ALTER TABLE                        |
|                         |             使用ALTER PROCEDURE和DROP PROCEDURE              |
|         CREATE          |                       使用CREATE TABLE                       |
|     CREATE ROUTINE      |                     使用CREATE PROCEDURE                     |
| CREATE TEMPORARY TABLES |                  使用CREATE TEMPORARY TABLE                  |
|       CREATE USER       | 使用CREATE USER, DROP USER, RENAME USER和REVOKE ALL PRIVILEGES |
|       CREATE VIEW       |                       使用CREATE VIEW                        |
|         DELETE          |                          使用DELETE                          |
|          DROP           |                        使用DROP TABLE                        |
|         EXECUTE         |                      使用CALL和存储过程                      |
|          FILEG          |          使用SELECT INTO OUTFILE和LOAD DATA INFILE           |
|       RANT OPTION       |                      使用GRANT和REVOKE                       |
|          INDEX          |                 使用CREATE INDEX和DROP INDEX                 |
|         INSERT          |                          使用INSERT                          |
|       LOCK TABLES       |                       使用LOCK TABLES                        |
|         PROCESS         |                  使用SHOW FULL PROCESSLIST                   |
|         RELOAD          |                          使用FLUSH                           |
|   REPLICATION CLIENT    |                       服务器位置的访问                       |
|    REPLICATION SLAVE    |                        由复制从属使用                        |
|         SELECT          |                          使用SELECT                          |
|        SHOW DATA        |                      使用SHOW DATABASES                      |
|     BASESSHOW VIEW      |                     使用SHOW CREATE VIEM                     |
|        SHUTDOWN         |           使用mysqladmin shutdown (用来关闭MySQL)            |
|          SUPER          | 使用CHANGE MASTER, KILL, LOGS, PURGE. MASTER和SET GLOBAL,还允许mysqladmin调试登录 |
|         UPDATE          |                          使用UPDATE                          |
|          USAGE          |                          无访问权限                          |

## 更改口令SET PASSWORD

```mysql
SET PASSWORD FOR bforta = Password('n3w p@ssword');
```

# 数据库维护

## 刷新未写数据FLUSH TABLES

## 进行数据库维护

-    ANALYZE TABLE,用来检查表键是否正确。

```mysql
ANALYZE TABLE orders;
```

-    CHECK TABLE用来针对许多问题对表进行检查。在MyISAM表上还对索引进行检查。CHECK TABLE支持一系列的用于MyISAM表的方式。CHANGED检查自最后一次检查以来改动过的表。EXTENDED执行最彻底的检查, FAST只检查未正常关闭的表, MEDIUM检查所有被删除的链接并进行键检验, QUICK只进行快速扫描。

```mysql
CHECK TABLE orders, orderitems;
```

## 诊断启动问题

-    --help显示帮助-一个选项列表
-    --safe-mode装载减去某些最佳配置的服务器
-    --verbose显示全文本消息(为获得更详细的帮助消息与--help联合使用)
-    --version显示版本信息然后退出

## 日志文件

*    错误日志。它包含启动和关闭问题以及任意关键错误的细节。此日志通常名为hostname. err,位于data目录中。此日志名可用--log-error命令行选项更改。
*    查询日志。它记录所有MySQL活动,在诊断问题时非常有用。此日志文件可能会很快地变得非常大,因此不应该长期使用它。此日志通常名为hostname.log,位于data目录中。此名字可以用--log命令行选项更改。
*    二进制日志。它记录更新过数据(或者可能更新过数据)的所有语句。此日志通常名为hostname-bin,位于data目录内。此名字可以用--log-bin命令行选项更改。注意,这个日志文件是MySQL5中添加的,以前的MySQL版本中使用的是更新日志。
*    缓慢查询日志。顾名思义,此日志记录执行缓慢的任何查询。这·个日志在确定数据库何处需要优化很有用。此日志通常名为hostname-slow.log ,位于data目录中。此名字可以用--log-slow-queries命令行选项更改。 

# 改善性能

*    首先, MySQL (与所有DBMS一样)具有特定的硬件建议。在学习和研究MySQL时,使用任何旧的计算机作为服务器都可以。但对用于生产的服务器来说,应该坚持遵循这些硬件建议。
*    一般来说,关键的生产DBMS应该运行在自己的专用服务器上。
*    MySQL是用一系列的默认设置预先配置的,从这些设置开始通常是很好的。但过一段时间后你可能需要调整内存分配、缓冲区大小等。(为查看当前设置,可使用SHOW VARIABLES;和SHOwSTATUS; )
*    MySQL一个多用户多线程的DBMS,换言之,它经常同时执行多个任务。如果这些任务中的某一个执行缓慢,则所有请求都会执行缓慢。如果你遇到显著的性能不良,可使用SHOW PROCESSLIST显示所有活动进程(以及它们的线程ID和执行时间)。你还可以用KILL命令终结某个特定的进程(使用这个命令需要作为管理员登录)。
*    总是有不止一种方法编写同一条SELECT语句。应该试验联结、并、子查询等,找出最佳的方法。
*    使用EXPLAIN语句让MySQL解释它将如何执行一条SELECT语句。
*    一般来说,存储过程执行得比一条一条地执行其中的各条MySQL语句块。
*    应该总是使用正确的数据类型。决不要检索比需求还要多的数据。换言之,不要用SELECT * (除非你真正需要每个列)。
*    有的操作(包括INSERT)支持一个可选的DELAYED关键字,如果使用它,将把控制立即返回给调用程序,并且一旦有可能就实际执行该操作。
*    在导入数据时,应该关闭自动提交。你可能还想删除索引(包括FULLTEXT索引),然后在导入完成后再重建它们。
*    必须索引数据库表以改善数据检索的性能。确定索引什么不是一件微不足道的任务,需要分析使用的SELECT语句以找出重复的WHERE和ORDER BY子句。如果一个简单的WHERE子句返回结果所花的时间太长,则可以断定其中使用的列(或几个列)就是需要索引的对象。
*    你的SELECT语句中有一系列复杂的OR条件吗?通过使用多条SELECT语句和连接它们的UNION语句,你能看到极大的性能改进。
*    索引改善数据检索的性能,但损害数据插入、删除和更新的性能,如果你有一些表,它们收集数据且不经常被搜索,则在有必要之.前不要索引它们。(索引可根据需要添加和删除。)
*    LIKE很慢。一般来说,最好是使用FULLTEXT而不是LIKE.数据库是不断变化的实体。
*    一组优化良好的表一会儿后可能就面目全非了。由于表的使用和内容的更改,理想的优化和配置也会改变。
*    最重要的规则就是,每条规则在某些条件下都会被打破。

## MySQL逻辑架构

*    客户端
*    连接/线程处理
*    查询缓存
*    解析器
*    优化器

最上层的服务并不是MySQL所独有的,大多数基于网络的客户端/服务器的工具或者服务都有类似的架构。

第二层架构。大多数MySQL的核心服务功能都在这一层,包括查询解析、分析、优化、缓存以及所有的内置函数(例如, 日期、时间、数学和加密函数),所有跨存储引擎的功能都在这一层实现:存储过程、触发器、视图等。

第三层包含了<u>存储引擎</u>。存储引擎负责MySQL中数据的存储和提取。服务器通过API与存储引擎进行通信。这些接口屏蔽了不同存储引擎之间的差异,使得这些差异对上层的查询过程透明。存储引擎API包含几十个底层函数,用于执行诸如“开始一个事务”或者“根据主键提取一行记录”等操作。但存储引擎不会去解析SQL,不同存储引擎之间也不会相互通信,而只是简单地响应上层服务器的请求。

## 连接管理与安全性

每个客户端连接都会在服务器进程中拥有一个<u>线程</u>,这个连接的查询,只会在这个单独的线程中执行,该线程只能轮流在某个CPU核心或者CPU中运行。服务器会负责缓存线程,因此不需要为每一个新建的连接创建或者销毁线程。

当客户端(应用)连接到MySQL服务器时,服务器需要对其进行认证。<u>认证基于用户名、原始主机信息和密码。</u>如果使用了安全套接字(SSL),的方式连接,还可以使用X. 509证书认证。一旦客户端连接成功,服务器会继续验证该客户端是否具有执行某个特定查询的权限(例如,是否允许客户端对world数据库的Country表执行SELECT语句)。

### 优化与执行

MySQL会解析查询,并创建内部<u>数据结构</u>(解析树),然后对其进行各种优化,包括重写查询、决定表的读取顺序,以及选择合适的索引等。

用户可以通过特殊的<u>关键字提示(hint)优化器</u>,影响它的决策过程。也可以请求优化器解释(explain)优化过程的各个因素,使用户可以知道服务器是如何进行优化决策的,并提供一个参考基准,便于用户重构查询和schema、修改相关配置,使应用尽可能高效运行。

## 并发控制

服务器层

存储引擎层

### 读写锁

在处理并发读或者写时,可以通过实现一个由两种类型的锁组成的锁系统来解决问题。这两种类型的锁通常被称为<u>共享锁(shared lock)</u>和<u>排他锁(exclusivelock)</u> ,也叫读锁(read lock)和写锁(write lock)。

读锁是共享的,或者说是相互不阻塞的。多个客户在同一时刻可以同时读取同一个资源,而互不干扰。

写锁则是排他的,也就是说一个写锁会阻塞其他的写锁和读锁,这是出于安全策略的考虑,只有这样,才能确保在给定的时间里,只有一个用户能执行写入,并防止其他用户读取正在写入的同一资源。

### 锁粒度

任何时候,在给定的资源上,锁定的数据量越少,则系统的并发程度越高,只要相互之间不发生冲突即可。

<u>加锁需要消耗资源</u>。锁的各种操作,包括获得锁、检查锁是,否已经解除、释放锁等,都会增加系统的开销。如果系统花费大量的时间来管理锁,而不是存取数据,那么系统的性能可能会因此受到影响。

所谓的锁策略,就是在锁的开销和数据的安全性之间寻求平衡,这种平衡当然也会影响到性能。

### 表锁(table lock)

<u>表锁是MySQL中最基本的锁策略,并且是开销最小的策略。</u>

表锁会锁定整张表。一个用户在对表进行写操作(插入、删除、更新等)前,需要先获得写锁,这会阻塞其他用户对该表的所有读写操作。只有没有写锁时,其他读取的用户才能获得读锁,读锁之间是不相互阻塞的。

在特定的场景中,表锁也可能有良好的性能。另外,<u>写锁也比读锁有更高的优先级</u>,因此一个写锁请求可能会被插入到读锁队列的前面(写锁可以插入到锁队列中读锁的前面,反之读锁则不能插入到写锁的前面)。尽管存储引擎可以管理自己的锁, MySQL本身还是会使用各种有效的表锁来实现不同的目的。

### 行级锁(row lock)

<u>行级锁可以最大程度地支持并发处理，同时也带来了最大的锁开销。</u>众所周知,在InnoDB和XtraDB,以及其他一些存储引擎中实现了行级锁。行级锁只在存储引擎层实现,而MySaL服务器层没有实现。服务器层完全不了解存储引擎中的锁实现。

## 事务

<u>事务就是一组原子性的SQL查询,或者说一个独立的工作单元。</u>如果数据库引擎能够成功地对数据库应用该组查询的全部语句,那么就执行该组查询。如果其中有任何一条语句因为崩溃或其他原因无法执行,那么所有的,语句都不会执行。<u>也就是说,事务内的语句,要么全部执行成功,要么全部执行失败。</u>

可以用START TRANSACTION语句开始一个事务,然后要么使用COMMIT提交事务将修改的数据持久保留,要么使用ROLLBACK撤销所有的修改。

```mysql
START TRANSACTION;
SELECT balance FROM checking WHERE customer_id = 10233276;
UPDATE checking SET balance = balance - 200.00 WHERE customer_id = 10233276;
UPDATE savings SET balance = balance + 200.00 WHERE customer_id = 10233276;
COMMIT;
```

*    原子性(atomicity)

一个事务必须被视为一个不可分割的最小工作单元,整个事务中的所有操作要么全部提交成功,要么全部失败回滚,对于一个事务来说,不可能只执行其中的一部分操作,这就是事务的原子性。

*    一致性(consistency)

数据库总是从一个一致性的状态转换到另外一个一致性的状态。

*    隔离性(isolation)

通常来说,一个事务所做的修改在最终提交以前,对其他事务是不可见的。

*    持久性(durability)

一旦事务提交,则其所做的修改就会永久保存到数据库中。此时即使系统崩溃,修改的数据也不会丢失。持久性是个有点模糊的概念,因为实际上持久性也分很多不同的级别。有些持久性策略能够提供非常强的安全保障,而有些则未必。而且不可能有能做到100%的持久性保证的策略。

### 隔离级别

*    READ UNCOMMITTED (未提交读)

在READ UNCOMMITTED级别,事务中的修改,即使没有提交,对其他事务也都是可见的。事务可以读取未提交的数据,这也被称为<u>脏读</u>(Dirty Read)。这个级别会导致很多问题,从性能上来说, READUNCOMMITTED不会比其他的级别好太多,但却缺乏其他级别的很多好处,除非真的有非常必要的理由,在实际应用中一般很少使用。

*    READ COMMITTED (提交读)

大多数数据库系统的默认隔离级别都是READ COMMITTED (但MySQL不是)。READ COMMITTED满足前面提到的隔离性的简单定义:一个事务开始时,只能“看见”已经提交的事务所做的修改。换句话说,一个事务从开始直到提交之前,所做的任何修改对其他事务都是不可见的。这个级别有时候也叫做<u>不可重复读</u>(nonrepeatable read) ,因为两次执行同样的查询,可能会得到不一样的结果。

*    REPEATABLE READ (可重复读)

REPEATABLE READ解决了脏读的问题。该级别保证了在同一个事务中多次读取同样记录的结果是一致的。但是理论上,可重复读隔离级别还是无法解决另外一个<u>幻读(Phantom Read)</u>的问题。所谓幻读,指的是<u>当某个事务在读取某个范围内的记录时,另外一个事务又在该范围内插入了新的记录,当之前的事务再次读取该范围的记录时,会产生幻行(Phantom Row)</u>, InnoDB和XtraDB存储引擎通过多版本并发控制(MvCC, Multiversion Concurrency Control)解决了幻读的问题。

*    SERIALIZABLE (可串行化)

SERIAL IZABLE是最高的隔离级别。它通过强制事务串行执行,<u>避免了前面说的幻读的问题</u>。简单来说, SERIAL IZABLE会在读取的每一行数据上都加锁,所以可能导致大量的超时和锁争用的问题。实际应用中也很少用到这个隔离级别,只有在非常需要确保数据的一致性而且可以接受没有并发的情况下,才考虑采用该级别。

| 隔离级别         | 脏读可能性 | 不可重复读可能性 | 幻读可能性 | 加锁读 |
| ---------------- | ---------- | ---------------- | ---------- | ------ |
| READ UNCOMMITTED | √          | √                | √          | ×      |
| READ COMMITTED   | ×          | √                | √          | ×      |
| REPEATABLE READ  | ×          | ×                | √          | ×      |
| SERIALIZABLE     | ×          | ×                | ×          | √      |

### 死锁

<u>死锁是指两个或者多个事务在同一资源上相互占用,并请求锁定对方占用的资源,从而导致恶性循环的现象。</u>当多个事务试图以不同的顺序锁定资源时,就可能会产生死锁。多个事务同时锁定同一个资源时,也会产生死锁。

为了解决这种问题,数据库系统实现了各种死锁检测和死锁超时机制。还有一种解决方式,就是当查询的时间达到锁等待超时的设定后放弃锁请求,这种方式通常来说不太好。InnoDB目前处理死锁的方法是,将持有最少行级排他锁的事务进行回滚(这是相对比较简单的死锁回滚算法)。

<u>锁的行为和顺序是和存储引擎相关的</u>。以同样的顺序执行语句,有些存储引擎会产生死锁,有些则不会。<u>死锁的产生有双重原因:有些是因为真正的数据冲突,这种情况通常很难避免,但有些则完全是由于存储引擎的实现方式导致的。</u>

<u>死锁发生以后,只有部分或者完全回滚其中一个事务,才能打破死锁。</u>·对于事务型的系统,这是无法避免的,所以应用程序在设计时必须考虑如何处理死锁。大多数情况下只需要重新执行因死锁回滚的事务即可。



# leetcode例题

## 1913. 查询学生学籍信息

编写一个 SQL 语句，满足条件：无论 students 是否有学籍 (enrollments) 信息，学生都需要根据如下两个表提供以下信息：

-    student_name,
-    phone,
-    hometown,
-    address

表定义 1: students (学生表)

|     列名     |     类型     |   注释   |
| :----------: | :----------: | :------: |
|      id      | int unsigned |   主键   |
| student_name |   varchar    | 学生姓名 |
|    phone     |   varchar    | 学生电话 |

表定义 2: enrollments (学籍表)

|    列名    |     类型     |  注释   |
| :--------: | :----------: | :-----: |
|     id     | int unsigned |  主键   |
| student_id | int unsigned | 学生 id |
|  hometown  |   varchar    |  家乡   |
|  address   |   varchar    |  地址   |

### 样例

**样例一：**

表内容 1: schedules

|  id  | student_name |    phone    |
| :--: | :----------: | :---------: |
|  1   |    Li Lei    | 13888888888 |
|  2   |  Han Meimei  | 13999999999 |
|  3   |     Amy      | 13788889999 |

表内容 2: enrollments

|  id  | student_id |   hometown    |    address    |
| :--: | :--------: | :-----------: | :-----------: |
|  1   |     1      | Shi Jiazhuang |   Hang Zhou   |
|  2   |     2      |   Heng Shui   |   Tang Shan   |
|  3   |     3      |   Cang Zhou   | Shi Jiazhuang |

返回：

| student_name |    phone    |   hometown    |    address    |
| :----------: | :---------: | :-----------: | :-----------: |
|    Li Lei    | 13888888888 | Shi Jiazhuang |   Hang Zhou   |
|  Han Meimei  | 13999999999 |   Heng Shui   |   Tang Shan   |
|     Amy      | 13788889999 |   Cang Zhou   | Shi Jiazhuang |

**样例二：**

表内容 1: students

|  id  | student_name |    phone    |
| :--: | :----------: | :---------: |
|  1   |    Li Lei    | 13888888888 |
|  2   |  Han Meimei  | 13999999999 |
|  3   |     Amy      | 13788889999 |
|  4   |    Jason     | 13788789999 |

表内容 2: enrollments

|  id  | student_id |   hometown    |    address    |
| :--: | :--------: | :-----------: | :-----------: |
|  1   |     1      | Shi Jiazhuang |   Hang Zhou   |
|  2   |     2      |   Heng Shui   |   Tang Shan   |
|  3   |     3      |   Cang Zhou   | Shi Jiazhuang |
|  4   |     1      |  Guang Zhou   |   Shi Hezi    |

应该返回:

| student_name |    phone    |   hometown    |    address    |
| :----------: | :---------: | :-----------: | :-----------: |
|    Li Lei    | 13888888888 | Shi Jiazhuang |   Hang Zhou   |
|  Han Meimei  | 13999999999 |   Heng Shui   |   Tang Shan   |
|     Amy      | 13788889999 |   Cang Zhou   | Shi Jiazhuang |
|    Li Lei    | 13888888888 |  Guang Zhou   |   Shi Hezi    |
|    Jason     | 13788789999 |     null      |     null      |

```sql
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
select s.student_name, s.phone, e.hometown, e.address
from students s
left join enrollments e
on s.id = e.student_id
```

## 1920. 查找重名的同学

编写一个 SQL 语句，查找 students 表中所有重名同学的名字。

表定义: students (学生表)

| 列名 |     类型     |   注释   |
| :--: | :----------: | :------: |
|  id  | int unsigned |   主键   |
| name |   varchar    | 学生姓名 |

### 样例

**样例一：**

表内容: students

|  id  |   name    |
| :--: | :-------: |
|  1   |  DaMing   |
|  2   |    Amy    |
|  3   | HanMeimei |
|  4   |    Amy    |

你的 SQL 查询应该返回以下结果：

| name |
| :--: |
| Amy  |

**样例二：**

表内容: students

|  id  |  name  |
| :--: | :----: |
|  1   | DaMing |
|  2   |  Amy   |
|  3   | DaMing |
|  4   |  Amy   |

你的 SQL 查询应该返回以下结果：

|  name  |
| :----: |
|  Amy   |
| DaMing |

```sql
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
select name from students
group by name
having count(*) > 1
```

## 1921. 从不充值的玩家

某游戏数据库包含两个表，用户 (users) 表和充值 (recharges) 表，编写一个 SQL 语句，找出所有从未充值的玩家。

表定义 1: users (用户表)

| 列名 |     类型     |   注释   |
| :--: | :----------: | :------: |
|  id  | int unsigned |   主键   |
| name |   varchar    | 用户姓名 |

表定义 2: recharges (充值表)

|  列名   |     类型     |  注释   |
| :-----: | :----------: | :-----: |
|   id    | int unsigned |  主键   |
| user_id |     int      | 用户 id |

### 样例

**样例一：**

表内容 1: users

|  id  |     name     |
| :--: | :----------: |
|  1   | XiaoXuesheng |
|  2   |     Mike     |
|  3   |     John     |
|  4   |    Maria     |

表内容 2: recharges

|  id  | user_id |
| :--: | :-----: |
|  1   |    3    |
|  2   |    1    |

按照上述要求，你的查询应该返回：

| player |
| :----: |
|  Mike  |
| Maria  |

**样例二：**

表内容 1: users

|  id  |     name     |
| :--: | :----------: |
|  1   | XiaoXuesheng |
|  2   |     Mike     |
|  3   |     John     |

表内容 2: recharges

|  id  | user_id |
| :--: | :-----: |
|  1   |    3    |
|  2   |    1    |

按照上述要求，你的查询应该返回：

| player |
| :----: |
|  Mike  |

### 注意事项

提示：

1.   你可以通过学习 SQL 联合查询相关知识来解决这个问题
2.   返回的列名：player

```sql
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
select name as player 
from users u 
where id 
not in (select user_id from recharges)
```

## 1924. 推荐学理科的同学

如果一个学生的数学超过 90 分，或者理综超过 95 分，那么就推荐这个学生去学理科。
请编写一个 SQL 语句，输出表中所有适合学理科学生的姓名、数学成绩及理综成绩。

-    cst (comprehensive science test 理综)

表定义: student_scores (学生成绩表)

|  列名   |  类型   |     注释     |
| :-----: | :-----: | :----------: |
|  name   | varchar |   学生姓名   |
| chinese |   int   | 学生语文分数 |
|  math   |   int   | 学生数学分数 |
| english |   int   | 学生英语分数 |
|   cst   |   int   | 学生理综分数 |

### 样例

**样例一：**

表内容: student_scores

|   name   | chinese | math | english | cst  |
| :------: | :-----: | :--: | :-----: | :--: |
| KangKang |   95    |  91  |   89    |  97  |
|   Jane   |   90    |  93  |   98    |  98  |
| Micheal  |   85    |  76  |   93    |  92  |
|  Maria   |   88    |  89  |   95    |  94  |
|  LiHua   |   30    |  13  |   19    |  23  |

根据上表，我们应该输出：

|   name   | math | cst  |
| :------: | :--: | :--: |
| KangKang |  91  |  97  |
|   Jane   |  93  |  98  |

**样例二：**

表内容: student_scores

|   name   | chinese | math | english | cst  |
| :------: | :-----: | :--: | :-----: | :--: |
| KangKang |   95    |  90  |   89    |  97  |
|   Jane   |   90    |  90  |   98    |  95  |

根据上表，我们应该输出：

|   name   | math | cst  |
| :------: | :--: | :--: |
| KangKang |  90  |  97  |

```mysql
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
select name, math, cst
FROM student_scores e
where e.math>90 or e.cst>95
```

## 1923. 增长的疫情感染人数

编写一个 SQL 语句，来查找与前一天的日期相比美国的新增病例数更高的所有日期的 id。

表定义: new_cases (新增疫情)

|      列名       |     类型     |     注释     |
| :-------------: | :----------: | :----------: |
|       id        | int unsigned |     主键     |
|      date       |     date     |     日期     |
| increased_count |     int      | 新增感染人数 |

### 样例

**样例一：**

表内容: new_cases

|  id  |    date    | increased_count |
| :--: | :--------: | :-------------: |
|  1   | 2020-12-25 |     100994      |
|  2   | 2020-12-26 |     216858      |
|  3   | 2020-12-27 |     152102      |
|  4   | 2020-12-28 |     189044      |

在运行你的 SQL 语句之后，应返回：

|  id  |
| :--: |
|  2   |
|  4   |

-    说明：
     -    2020-12-26 美国的新增病例数比前一天高（100994 -> 216858）
     -    2020-12-28 美国的新增病例数比前一天高（152102 -> 189044）

**样例二：**

表内容: new_cases

|  id  |    date    | increased_count |
| :--: | :--------: | :-------------: |
|  1   | 2011-12-25 |     100994      |
|  2   | 2011-12-26 |     296858      |
|  3   | 2011-12-27 |     152102      |
|  4   | 2011-12-28 |     149044      |

在运行你的 SQL 语句之后，应返回：

|  id  |
| :--: |
|  2   |

-    说明：
     -    2011-12-26 美国的新增病例数比前一天高（100994 -> 296858）

### 注意事项

返回结果**不要求顺序**

```sql
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
select a.id 
from new_cases as a,new_cases as b
where a.id = b.id + 1 and a.increased_count > b.increased_count
```

## 1926. 热门的英雄

编写一个 SQL 语句，找出所有英雄热度为非 T3 (不热门)的并且 id 为奇数的英雄，结果请按 ban 率由大到小排列。
Tx (x = 0, 1 ,2, ...) 表示英雄的热度，其中，T0 表示热门英雄，T1 表示次热门英雄，T2 表示正常热度英雄，T3 表示不热门英雄，T4 及以后表示冷门英雄。

表定义: heroes (英雄表)

|    列名    |     类型     |     注释     |
| :--------: | :----------: | :----------: |
|     id     | int unsigned |     主键     |
|    name    |   varchar    |   英雄名字   |
| popularity |   varchar    | 英雄热门等级 |
|    ban     |    float     | 英雄被禁概率 |

### 样例

**样例一：**

表内容: heroes

|  id  |    name    | popularity |  ban  |
| :--: | :--------: | :--------: | :---: |
|  1   |   Lv Bu    |     T0     | 0.90  |
|  2   | Ju Youjing |     T1     | 0.24  |
|  3   |  Ma Chao   |     T1     | 10.26 |
|  4   |  Guan Yu   |     T2     | 1.56  |
|  5   | Meng Tian  |     T3     | 2.10  |

对于上面的例子，正确的输出为：

|  id  |  name   | popularity | probability |
| :--: | :-----: | :--------: | :---------: |
|  1   | Ma Chao |     T1     |   10.26%    |
|  2   |  Lv Bu  |     T0     |    0.90%    |

**样例二：**

表内容: heroes

|  id  |    name    | popularity |  ban  |
| :--: | :--------: | :--------: | :---: |
|  1   |   Lv Bu    |     T3     | 0.90  |
|  2   | Ju Youjing |     T1     | 0.24  |
|  3   |  Ma Chao   |     T1     | 10.26 |
|  4   |  Guan Yu   |     T2     | 1.56  |

对于上面的例子，正确的输出为：

|  id  |  name   | popularity | probability |
| :--: | :-----: | :--------: | :---------: |
|  1   | Ma Chao |     T1     |   10.26%    |

### 注意事项

请注意，所返回的 probability 需要带上百分号 (%)

```sql
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
select id, name, popularity, concat(ban,'%') as probability
from heroes
where popularity!='T3' and id%2=1
order by ban desc
```

## 1927. 硬币翻面

给定一个 coins 表，其中的 side 属性表示硬币的正反面，p 表示正面 (positive)，n 表示反面 (negative)
交换所有的 p 和 n 值（例如，将所有 p 值改为 n，反之亦然）。
要求只使用一个**更新 (UPDATE)** 语句，并且**没有**中间的临时表。

表定义: coins (硬币表)

| 列名 |     类型     |   注释   |
| :--: | :----------: | :------: |
|  id  | int unsigned |   主键   |
| side |   varchar    | 硬币的面 |

### 样例

**样例一：**

表内容: coins

|  id  | side |
| :--: | :--: |
|  1   |  p   |
|  2   |  n   |
|  3   |  p   |
|  4   |  n   |

运行你所编写的 SQL 语句之后，将会得到以下表：

|  id  | side |
| :--: | :--: |
|  1   |  n   |
|  2   |  p   |
|  3   |  n   |
|  4   |  p   |

**样例二：**

表内容: coins

|  id  | side |
| :--: | :--: |
|  1   |  p   |
|  2   |  n   |

运行你所编写的 SQL 语句之后，将会得到以下表：

|  id  | side |
| :--: | :--: |
|  1   |  n   |
|  2   |  p   |

### 注意事项

提示：

1.   你可以通过学习 SQL 语句中的 **UPDATE 语句**和**条件判断相关知识**来解决该问题。
2.   只能写一个 UPDATE 语句，请不要编写任何 SELECT 语句。
3.   我们会单独验证数据库中的数据是否都被修改为如下的信息。

```sql
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
update coins
set side='m'
where side='p';

update coins
set side='p'
where side='n';

update coins
set side='n'
where side='m';
```

## 1931.  寻找特定的患者

描述

patients 表中保存了所有患者信息和感染他们的人 (infected_by_id)
编写一个 SQL 语句，返回一个列表，列表中出现的名字需要满足条件：感染他们的人的 id **不是2**

表定义: patients (患者表)

|      列名      |     字段     |   注释    |
| :------------: | :----------: | :-------: |
|       id       | int unsigned |   主键    |
|      name      |   varchar    | 患者姓名  |
| infected_by_id |     int      | 感染者 id |

样例

**样例一：**

表内容: patients

|  id  |   name   | infected_by_id |
| :--: | :------: | :------------: |
|  1   |   Amy    |      null      |
|  2   |   Bob    |      null      |
|  3   | Catalina |       2        |
|  4   |   Deng   |      null      |
|  5   |  Eason   |       1        |
|  6   |  Frank   |       2        |

在运行你的 SQL 语句之后，表应返回：

| name  |
| :---: |
|  Amy  |
|  Bob  |
| Deng  |
| Eason |

**样例二：**

表内容: patients

|  id  |   name   | infected_by_id |
| :--: | :------: | :------------: |
|  1   |   Amy    |      null      |
|  2   |   Bob    |      null      |
|  3   | Catalina |       2        |

在运行你的 SQL 语句之后，表应返回：

| name |
| :--: |
| Amy  |
| Bob  |

```sql
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
select name
from patients
where  infected_by_id is null or infected_by_id<>2;
```

## 1941.  寻找直角三角形

描述

李华的作业是判断三条线段是否可以构成直角三角形
假设表 line_segments 保存了所有由三条长度为 a, b, c 的线段构成的组，请你帮李华写一个 SQL 语句，来判断每组线段是否可以组成一个直角三角形

表定义: line_segments (线段表)

| 列名 |     类型     |    注释    |
| :--: | :----------: | :--------: |
|  id  | int unsigned |    主键    |
|  a   |     int      | a 线段长度 |
|  b   |     int      | b 线段长度 |
|  c   |     int      | c 线段长度 |

样例

**样例一：**

表内容: line_segments

|  id  |  a   |  b   |  c   |
| :--: | :--: | :--: | :--: |
|  1   |  3   |  4   |  5   |
|  2   |  10  |  20  |  15  |
|  3   |  1   |  2   |  10  |

在运行你的 SQL 语句之后，表应返回：

|  id  |  a   |  b   |  c   | right_triangle |
| :--: | :--: | :--: | :--: | :------------: |
|  1   |  3   |  4   |  5   |      Yes       |
|  2   |  10  |  20  |  15  |       No       |
|  3   |  1   |  2   |  10  |       No       |

**样例二：**

表内容: line_segments

|  id  |  a   |  b   |  c   |
| :--: | :--: | :--: | :--: |
|  1   |  6   |  6   |  6   |
|  2   |  5   |  12  |  13  |

在运行你的 SQL 语句之后，表应返回：

|  id  |  a   |  b   |  c   | right_triangle |
| :--: | :--: | :--: | :--: | :------------: |
|  1   |  6   |  6   |  6   |       No       |
|  2   |  5   |  12  |  13  |      Yes       |

```cpp
-- Write your SQL Query here --
-- example: SELECT * FROM XX_TABLE WHERE XXX --
SELECT *,
IF
( POW( a, 2 ) + POW( b, 2 ) = POW( c, 2 ), 'Yes', 'No' ) AS 'right_triangle'
FROM
line_segments
```



## 2045.  输出 Hello LintCode

描述

请编写 SQL 语句，返回 "Hello LintCode!" 语句，不用在意返回结果集的列名

表定义：无

样例

表内容：（无）

在运行你的 SQL 语句之后，表应返回：

| Hello LintCode! |
| --------------- |
| Hello LintCode! |

```cpp
-- Write your SQL Query here --
SELECT "Hello LintCode!"
```



## 2046.  查询课程创建日期按 ‘年-月-日 时：分：秒’ 显示

描述

请编写 SQL 语句，查询 `courses` 表，查询课程创建时间，按照 ’年-月-日 时：分：秒’ 的格式返回结果，返回列名显示为 `DATE_FORMAT`。

表定义: courses（课程表）

|     列名      |     类型     |     注释     |
| :-----------: | :----------: | :----------: |
|      id       | int unsigned |     主键     |
|     name      |   varchar    |   课程名称   |
| student_count |     int      |   学生总数   |
|  created_at   |     date     | 课程创建时间 |
|  teacher_id   |     int      |   讲师 id    |

查询返回列名需要与样例输出的列名大小写一致

样例

样例一：

表内容：courses

| **id** | **name**                | **student_count** | **created_at**     | **teacher_id** |
| ------ | ----------------------- | ----------------- | ------------------ | -------------- |
| 1      | Senior Algorithm        | 880               | 2020-6-1 09:03:12  | 4              |
| 2      | System Design           | 1350              | 2020-7-18 10:03:12 | 3              |
| 3      | Django                  | 780               | 2020-2-29 12:03:12 | 3              |
| 4      | Web                     | 340               | 2020-4-22 13:03:12 | 4              |
| 5      | Big Data                | 700               | 2020-9-11 16:03:12 | 1              |
| 6      | Artificial Intelligence | 1660              | 2018-5-13 18:03:12 | 3              |
| 7      | Java P6+                | 780               | 2019-1-19 13:03:12 | 3              |
| 8      | Data Analysis           | 500               | 2019-7-12 13:03:12 | 1              |
| 10     | Object Oriented Design  | 300               | 2020-8-8 13:03:12  | 4              |
| 12     | Dynamic Programming     | 2000              | 2018-8-18 20:03:12 | 1              |

在运行你的 SQL 语句之后，表应返回：

| **DATE_FORMAT**     |
| ------------------- |
| 2020-06-01 09:03:12 |
| 2020-07-18 10:03:12 |
| 2020-02-29 12:03:12 |
| 2020-04-22 13:03:12 |
| 2020-09-11 16:03:12 |
| 2018-05-13 18:03:12 |
| 2019-01-19 13:03:12 |
| 2019-07-12 13:03:12 |
| 2020-08-08 13:03:12 |
| 2018-08-18 20:03:12 |

样例二：

表内容：courses

| **id** | **name**                | **student_count** | **created_at** | **teacher_id** |
| ------ | ----------------------- | ----------------- | -------------- | -------------- |
| 1      | Senior Algorithm        | 880               | null           | 4              |
| 2      | System Design           | 1350              | null           | 3              |
| 3      | Django                  | 780               | null           | 3              |
| 4      | Web                     | 340               | null           | 4              |
| 5      | Big Data                | 700               | null           | 1              |
| 6      | Artificial Intelligence | 1660              | null           | 3              |
| 7      | Java P6+                | 780               | null           | 3              |
| 8      | Data Analysis           | 500               | null           | 1              |
| 10     | Object Oriented Design  | 300               | null           | 4              |
| 12     | Dynamic Programming     | 2000              | null           | 1              |

在运行你的 SQL 语句之后，表应返回：

| **DATE_FORMAT** |
| --------------- |
| null            |
| null            |
| null            |
| null            |
| null            |
| null            |
| null            |
| null            |
| null            |
| null            |

>    样例二中课程表中没有课程创建时间，所以统计结果为空。

```cpp
-- Write your SQL Query here -- 
-- example: SELECT * FROM XX_TABLE WHERE XXX --
select DATE_FORMAT(created_at,'%Y-%m-%d %H:%i:%s') DATE_FORMAT 
from courses;
```

## DATE_FORMAT() 用法

我们在SQL中使用 `DATE_FORMAT()` 方法来格式化输出 date/time。
需要注意的是 `DATE_FORMAT()` 函数返回的是**字符串**格式。

**语法**

```
SELECT DATE_FORMAT(date,format);
```

其中

`date` 一个有效日期。

`format` 是 date/time 的输出格式。

# 参考

*    高性能MySQL
*    MySQL必知必会

