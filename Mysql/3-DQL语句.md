DQL全称是Data Query Language，表示数据查询语言。体现在数据的查询操作上，因此，DQL仅包括SELECT语句

# SELECT语句 查询
```
SELECT ALL/DISTINCT * | 字段名1 AS 别名1[,字段名1 AS 别名1, ..., 字段名n AS 别名n]
FROM 表名 WHERE 查询条件
```
ALL表示查询所有满足条件的记录，可以省略；DISTINCT表示去掉查询结果中重复的记录
AS可以给数据列、数据表取一个别名

#  比较操作符

![[Pasted image 20260909081815.png]]

### 比较操作符一般在末尾表示条件
```
例子:SELECT * FROM course WHERE name IS NULL;查询name为空的
	SELECT * FROM course WHERE score BETWEEN 2 AND 4; 查询score在2到4之间的
	SELECT * FROM course WHERE name LIKE '%v%';查询name中存在v字符的
	SELECT * FROM course WHERE `number` IN (1, 3, 5);查询number符合135其中一个
```

# 分组

## 分组查询
```
SELECT ALL/DISTINCT * | 字段名1 AS 别名1[,字段名1 AS 别名1, ..., 字段名n AS 别名n]
FROM 表名 WHERE 查询条件 GROUP BY [分组条件]字段名1，字段名2,..., 字段名n
```
```
例子:SELECT * FROM student WHERE score>80 GROUP BY sex;
	从学生表查询成绩在80分以上的学生信息并按性别分组
	
	SELECT * FROM student WHERE score BETWEEN 60 AND 80 GROUP BY sex, age;
	从学生表查询成绩在60~80之间的学生信息并按性别和年龄分组
```
## 聚合函数
COUNT() ：统计满足条件的数据总条数
SUM()：只能用于数值类型的字段或者表达式，计算该满足条件的字段值的总和
AVG()：只能用于数值类型的字段或者表达式，计算该满足条件的字段值的平均值
MAX()：只能用于数值类型的字段或者表达式，计算该满足条件的字段值的最大值
MIN()：只能用于数值类型的字段或者表达式，计算该满足条件的字段值的最小值
```
从学生表查询成绩在80分以上的学生人数
SELECT COUNT(*) total FROM student WHERE score>80;

从学生表查询不及格的学生人数和总成绩
SELECT COUNT(*) totalCount, SUM(score) totalScore FROM student WHERE
score<60;

从学生表查询男生、女生、其他类型的学生的平均成绩
SELECT sex, AVG(score) avgScore FROM student GROUP BY sex;

从学生表查询学生的最大年龄
SELECT MAX(age) FROM student;

从学生表查询学生的最低分
SELECT MIN(score) FROM student;
```

## 分组查询结果筛选
```
SELECT ALL/DISTINCT * | 字段名1 AS 别名1[,字段名1 AS 别名1, ..., 字段名n AS 别名n]
FROM 表名 WHERE 查询条件 GROUP BY 字段名1，字段名2,..., 字段名n HAVING [分组后筛选] 筛选条件

分组后如果还需要满足其他条件，则需要使用HAVING子句来完成。
```

```
从学生表查询年龄在20~30之间的学生信息并按性别分组，找出组内平均分在74分以上的组
SELECT * FROM student WHERE age BETWEEN 20 AND 30 GROUP BY sex HAVING
avg(score)>74;
```

## 排序
```
SELECT ALL/DISTINCT * | 字段名1 AS 别名1[,字段名1 AS 别名1, ..., 字段名n AS 别名n]
FROM 表名 WHERE 查询条件 ORDER BY 字段名1 ASC|DESC，字段名2 ASC|DESC,..., 字段名n
ASC|DESC

ORDER BY 必须位于WHERE 条件之后
```

```
从学生表查询年龄在18~30岁之间的学生信息并按成绩从高到低排列，如果成绩相同，则按年龄从小到大排列

SELECT * FROM student WHERE age BETWEEN 18 AND 30 ORDER BY score DESC, age ASC;
```

## 分页
```
SELECT ALL/DISTINCT * | 字段名1 AS 别名1[,字段名1 AS 别名1, ..., 字段名n AS 别名n]
FROM 表名 WHERE 查询条件 LIMIT 偏移量, 查询条数


LIMIT的第一个参数表示偏移量，也就是跳过的行数。
LIMIT的第二个参数表示查询返回的最大行数，可能没有给定的数量那么多行.
```
```

从学生表分页查询成绩及格的学生信息，每页显示3条，查询第2页学生信息
SELECT * FROM student WHERE score>=60 LIMIT 3, 3;
```

## **如果一个查询中包含分组、排序和分页，那么它们之间必须按照分组->排序->分页的先后顺序排列**
