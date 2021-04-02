# 1913. 查询学生学籍信息

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

# 1920. 查找重名的同学

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

# 1921. 从不充值的玩家

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

# 1924. 推荐学理科的同学

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

# 1923. 增长的疫情感染人数

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

# 1926. 热门的英雄

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

# 1927. 硬币翻面

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

# 1931.  寻找特定的患者

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

# 1941.  寻找直角三角形

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



# 2045.  输出 Hello LintCode

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



# 2046.  查询课程创建日期按 ‘年-月-日 时：分：秒’ 显示

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

