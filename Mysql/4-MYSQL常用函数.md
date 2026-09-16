
## 常用数学函数
![[Pasted image 20260909084916.png]]



## 常用字符串函数
![[Pasted image 20260909084940.png]]


```
查询计科和软工各有多少人
查询前两位并统计人数并按照	前两位分组
SELECT LEFT(class, 2), COUNT(*) FROM stu GROUP BY LEFT(class, 2);

查询名字有4个字的学生信息
SELECT * FROM stu WHERE CHAR_LENGTH(`name`)=4;

查询成绩能够被10整除的考试信息
SELECT * FROM score WHERE MOD(score, 10)=0;
```

## 日期和时间函数
![[Pasted image 20260909091214.png]]

```
查询年龄在20岁以上的学生信息
SELECT * FROM stu WHERE TIMESTAMPDIFF(YEAR, birthday, NOW()) > 20;

查询今天过生日的学生信息
SELECT * FROM stu WHERE MONTH(birthday)=MONTH(NOW()) AND
DAYOFMONTH(birthday)=DAYOFMONTH(NOW());

查询本周过生日的学生信息
SELECT * FROM stu WHERE RIGHT(birthday, 5) > RIGHT(DATE_FORMAT(ADDDATE(NOW(), -
DAYOFWEEK(NOW())), '%Y-%m-%d'), 5) AND RIGHT(birthday, 5) <=
RIGHT(DATE_FORMAT(ADDDATE(NOW(),7-DAYOFWEEK(NOW())), '%Y-%m-%d'), 5);
```

## 条件判断函数

```
IF(条件, 表达式1, 表达式2)
如果条件满足，则使用表达式1,否则使用表达式2

SELECT id,stu_name,course, IF(score>=60, '及格','不及格') score FROM score;


IFNULL(字段, 表达式)
如果字段值为空，则使用表达式，否则，使用字段值

SELECT id,stu_name,course, IFNULL(score, '缺考') score FROM score;

```

```
CASE...WHEN 语句

CASE WHEN 条件1 THEN 表达式1 [WHEN 条件2 THEN 表达式2 ...] ELSE 表达式n END

如果条件1满足，则使用表达式1；【如果条件2满足，则使用表达式2， ... 】否则，使用表达式n。相当
于Java中的多重if..else语句


查询score表单如果course名字为java 返回成绩否则为0 并新建java表单来展示哦
SELECT (CASE WHEN (course = 'Java') THEN score ELSE 0 END) AS Java FROM score;
```


```

行转列：查询每位学生的各课程成绩
SELECT
stu_name,
course,
MAX(CASE course WHEN 'Java' THEN score ELSE 0 END) Java,
MAX(CASE course WHEN 'Html' THEN score ELSE 0 END) Html,
MAX(CASE course WHEN 'Jsp' THEN score ELSE 0 END) Jsp,
MAX(CASE course WHEN 'Spring' THEN score ELSE 0 END) Spring
FROM score
GROUP BY stu_name;
```

```
其他函数
FORMAT(X,D)，将数字X格式化，将X保留到小数点后D位，截断时要进行四舍五入。

SELECT FORMAT(1.2353,2);
```
系统信息函数
![[Pasted image 20260909093602.png]]

