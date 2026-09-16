
DML全称为Data Manipulation Language，表示数据操作语言。主要体现于对表数据的增删改操作。因此DML仅包括INSERT、UPDATE和DELEETE语句。

# INSERT 插入数据
``` 
-- 需要注意，VALUES后的字段值必须与表名后的字段名一一对应
INSERT INTO 表名(字段名1, 字段名2, ..., 字段名n) VALUES(字段值1, 字段值2, ..., 字段值
n);

插入简写
INSERT INTO 表名 VALUES(字段值1, 字段值2, ..., 字段值n)

-- 一次性插入多条数据
INSERT INTO 表名(字段名1, 字段名2, ..., 字段名n) VALUES(字段值1, 字段值2, ..., 字段值
n),(字段值1, 字段值2, ..., 字段值n), ... , (字段值1, 字段值2, ..., 字段值n);


INSERT INTO 表名 VALUES(字段值1, 字段值2, ..., 字段值n), (字段值1, 字段值2, ..., 字段值
n), ..., (字段值1, 字段值2, ..., 字段值n)
```
# UPDATE语句 更新表数据
```
UPDATE 表名 SET 字段名1=字段值1[,字段名2=字段值2, ..., 字段名n=字段值n] [WHERE 修改条件]
逻辑运算符和java差不多 && || 也可以用and OR
```

# DELETE语句 删除数据
```
DELETE FROM 表名 [WHERE 删除条件];
```

# TRUNCATE语句 清空数据
```
-- 清空表中数据
TRUNCATE [TABLE] 表名;
```