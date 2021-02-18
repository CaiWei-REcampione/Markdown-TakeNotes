

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

# 检索信息

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

## 检索所有列

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

SELECT DISTINCT vend-id告诉MySQL只返回不同(唯一)的vend_id行,因此只返回4行。如果使用DISTINCT关键字,它必须直接放在列名的前面。

