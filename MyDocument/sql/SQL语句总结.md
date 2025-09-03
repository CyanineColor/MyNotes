
1.创建数据库和创建表都是CREATE

```
CREATE DATABASE xxx;
```

```
CREATE TABLE xxxx(
```

2.删除数据库和表都是DROP

```
DROP DATABASE xxx;
```

3.给表添加主键

```
ALTER TABLE 表名 ADD PRIMARY KEY(列名);
```

4.基础增删改查

```
SELECT * FROM 表名;（把星号换成具体列名即查具体列）
```

5.模糊查找LIKE

```
--通配符：下滑线匹配任意单个字符，百分号%匹配所有
```

6.范围查找

```
--像between 、>、<等 
```

7.多值查找IN

```
SELECT * FROM 表 WHERE 列 IN ('A','B','C');
```

8.子查询（嵌套查询）

```
SELECT * FROM 表A WHERE 列 IN 
```

9.是否存在EXISTS或NOT EXISTS  

```
SELECT * FROM 表A 
```

exists的用法和in很像，当我们不在意后面这个条件的值是多少，而只在意存不存在时，用exists比in的性能会更好一点。

10.多表关联查询  

INNER JOIN（只看每个表中都有的）、LEFT JOIN（把左边的表作为基准）

```
SELECT * FROM 表A
```

```
SELECT*FROM 表A
```

当仅通过一张表无法满足查询要求时，会进行多表关联，写join语句时，首先要清楚两张表之间的关系，找到合适的关联字段，切不可认为只要是两张表中都有的字段就能关联，这样可能导致笛卡尔积。当掌握了两张表的关联时，其实多种表的关联也是同样道理，一个串一个。在select或者where后面要清楚该列是来源于哪张表的，不要把关系搞错。也不建议一个sql语句串联很多表。

11.聚合函数

常用的聚合函数有count计数、sum求和、avg求平均、max最大值、min最小值：

```
SELECT SUM(amount) AS total_sales FROM sales;
```

聚合函数将多行汇总成一行，得到的是一个值，可以配合GROUP BY使用，将所有数据分成几组，分别汇总得出每组的值：

```
SELECT Gender,COUNT(*) 
```

对聚合后的结果指定条件可以使用HAVING:

```
SELECT CourseNumber,AVG(Score) FROM dbo.Score 
```

12.只显示前N条数据TOP（或者LIMIT）：

```
SELECT TOP 10 * FROM dbo.Student;
```

13.去掉重复值DISTINCT

```
SELECT DISTINCT Name FROM dbo.Student
```

14.两张表相加UNION

```
SELECT product_id,product_name FROM dbo.Product
```

使用UNION将两张表相加时要注意列数和列的数据类型必须要一致。UNION默认会去掉两张表合并后重复的记录，UNION ALL不会去重。

15.常用日期函数

GETDATE()：获取当前系统时间

YEAR,MONTH,DAY这些可以返回一个时间的具体部分

DATEADD：可以对日期进行加减计算

DATEDIFF：可以返回两个日期之间的差值

```
SELECT DATEADD(DAY,10,GETDATE()) AS '十天后'
```

16.常用算术函数

加（+）减（-）乘（*）除（/）、ABS（绝对值）、MOD(求余)、ROUND(四舍五入)等

```
SELECT ROUND(3.1415926,2);---结果3.1400000
```

17.常用字符串函数

字符串函数是对字符串进行替换、截取、简化等操作。

拼接：concat

```
SELECT Province ,City ,
```

获取字符串长度：len或length

字符串替换：replace

```
--将Department这列中的‘系’替换成‘学院’
```

字符串的截取：substring

```
--将名字中的第一字截取出来作为姓
```

18.自定义函数

除了上述这些数据库内置的函数，也可以自己定义函数，语法是：

```
CREATE FUNCTION 函数名
```

即指明传入和传出的参数是什么，中间写明函数的逻辑处理语句。

19.视图：

视图可以理解成一张表，只不过它是一张虚拟表，其本身并不存储数据，而是基于一个或多个基础表的查询结果定义而成（它底层对应SELECT查询语句）。

创建视图使用的是CREATE VIEW语句：

```
CREATE VIEW view_name
```

20.索引：

索引是一种用于快速查询和检索数据的数据结构，就相当于书的目录。创建索引的语法是:

```
CREATE INDEX index_name ON table_name (column_name);
```

可以分为聚集索引和非聚集索引，聚集索引和表中数据的物理存储顺序一致，在一个表中只能有一个聚集索引，一般是主键。索引虽然会提升查询性能，但也会降低插入和更新的速度，所以并不是越多越好，建议一张表上的索引最多不超过5个。同时有很多情况会导致索引失效，写SQL语句时要注意合理利用索引。

21.窗口函数：

窗口函数是在 SQL 查询中对一组相关联的记录进行计算而返回一个值的函数。与普通的聚合函数（如SUM, AVG等）类似，但有一个关键区别：窗口函数不会将多行合并成单行输出，而是保留原始的行数，并在每行上附加计算结果。这意味着你可以在同一行中同时看到原始数据和聚合结果。

窗口函数的语法结构通常为：

```
函数名() OVER ( [partition by] order by() )
```

例如用于排序的窗口函数：ROW_NUMBER()、RANK()

原本出处引用-https://mp.weixin.qq.com/s/T6tZjr_8I3h3Ao7i70nwbA