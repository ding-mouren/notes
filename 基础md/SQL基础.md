### SQL基础

#### SQL SELECT语句

```sql
选取表中一部分列：
	SELECT column_name,column_name
	FROM table_name;
选取表中所有的列：
	SELECT * FROM table_name;
从 "Websites" 表中选取 "name" 和 "country" 列：
	SELECT name,country FROM Websites;
```

#### SQL SELECT DISTINCT 语句

1. SELECT DISTINCT 语句用于返回唯一不同的值。
2. 在表中，一个列可能会包含多个重复值，有时您也许希望仅仅列出不同（distinct）的值。
3. DISTINCT 关键词用于返回唯一不同的值。

语法：

```sql
SELECT DISTINCT column_name,column_name
FROM table_name;
```

实例：

从 "Websites" 表的 "country" 列中选取唯一不同的值，也就是去掉 "country" 列重复值：

```sql
SELECT DISTINCT country FROM Websites;
```

#### SQL WHERE 子句

WHERE 子句用于提取那些满足指定条件的记录。

语法：

```sql
SELECT column_name,column_name
FROM table_name
WHERE column_name operator value;
```

实例：

从 "Websites" 表中选取国家为 "CN" 的所有网站：

```sql
SELECT * FROM Websites WHERE country='CN';
```

SQL 使用单引号来环绕文本值（大部分数据库系统也接受双引号）。在上个实例中 'CN' 文本字段使用了单引号。如果是数值字段，请不要使用引号。

#### SQL AND & OR 运算符

如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。

如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。

实例：

从 "Websites" 表中选取国家为 "CN" 且alexa排名大于 "50" 的所有网站：

```sql
SELECT * FROM Websites
WHERE country='CN'
AND alexa > 50;
```

从 "Websites" 表中选取国家为 "USA" 或者 "CN" 的所有客户：

```sql
SELECT * FROM Websites
WHERE country='USA'
OR country='CN';
```

从 "Websites" 表中选取 alexa 排名大于 "15" 且国家为 "CN" 或 "USA" 的所有网站：

```sql
SELECT * FROM Websites
WHERE alexa > 15
AND (country='CN' OR country='USA');
```

#### SQL ORDER BY 关键字

ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。

ORDER BY 关键字默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。

语法：

```sql
SELECT column_name,column_name
FROM table_name
ORDER BY column_name,column_name ASC|DESC;
```

实例：

从 "Websites" 表中选取所有网站，并按照 "alexa" 列排序：

```sql
SELECT * FROM Websites
ORDER BY alexa;
```

从 "Websites" 表中选取所有网站，并按照 "alexa" 列降序排序：：

```sql
SELECT * FROM Websites
ORDER BY alexa DESC;
```

#### SQL INSERT INTO 语句

INSERT INTO 语句可以有两种编写形式。

第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：

```sql
INSERT INTO table_name
VALUES (value1,value2,value3,...);
```

第二种形式需要指定列名及被插入的值：

```sql
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```

实例：

```sql
假设我们要向 "Websites" 表中插入一个新行：
	INSERT INTO Websites (name, url, alexa, country)
	VALUES ('百度','https://www.baidu.com/','4','CN');
将插入一个新行，但是只在 "name"、"url" 和 "country" 列插入数据（id 字段会自动更新）：
	INSERT INTO Websites (name, url, country)
	VALUES ('stackoverflow', 'http://stackoverflow.com/', 'IND');
```

#### SQL UPDATE 语句

UPDATE 语句用于更新表中已存在的记录。

语法：

```sql
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```

实例：

```sql
假设我们要把 "菜鸟教程" 的 alexa 排名更新为 5000，country 改为 USA：
	UPDATE Websites 
	SET alexa='5000', country='USA' 
	WHERE name='菜鸟教程';
```

警告：

在更新记录时要格外小心！在上面的实例中，如果我们省略了 WHERE 子句，如下所示：

```sql
UPDATE Websites
SET alexa='5000', country='USA'
```

执行以上代码会将 Websites 表中所有数据的 alexa 改为 5000，country 改为 USA。

执行没有 WHERE 子句的 UPDATE 要慎重，再慎重。

#### SQL DELETE 语句

DELETE 语句用于删除表中的记录。

语法：

```sql
	DELETE FROM table_name
	WHERE some_column=some_value;
```

注意：

请注意 SQL DELETE 语句中的 WHERE 子句！
WHERE 子句规定哪条记录或者哪些记录需要删除。如果您省略了 WHERE 子句，所有的记录都将被删除！

实例：

从 "Websites" 表中删除网站名为 "百度" 且国家为 CN 的网站 ：

```sql
DELETE FROM Websites
WHERE name='百度' AND country='CN';
```

删除所有数据：

```sql
DELETE FROM table_name;

或

DELETE * FROM table_name;
```

**注释：**在删除记录时要格外小心！因为您不能重来！

### SQL函数

#### SQL Aggregate 函数

SQL Aggregate 函数计算从列中取得的值，返回一个单一的值。

有用的 Aggregate 函数：

- AVG() - 返回平均值
- COUNT() - 返回行数
- FIRST() - 返回第一个记录的值
- LAST() - 返回最后一个记录的值
- MAX() - 返回最大值
- MIN() - 返回最小值
- SUM() - 返回总和

#### SQL Scalar 函数

SQL Scalar 函数基于输入值，返回一个单一的值。

有用的 Scalar 函数：

- UCASE() - 将某个字段转换为大写
- LCASE() - 将某个字段转换为小写
- MID() - 从某个文本字段提取字符，MySql 中使用
- SubString(字段，1，end) - 从某个文本字段提取字符
- LEN() - 返回某个文本字段的长度
- ROUND() - 对某个数值字段进行指定小数位数的四舍五入
- NOW() - 返回当前的系统日期和时间
- FORMAT() - 格式化某个字段的显示方式

### MySQL 教程

​	MySQL 是最流行的关系型数据库管理系统，在 WEB 应用方面 MySQL 是最好的 RDBMS(Relational Database Management System：关系数据库管理系统)应用软件之一。

#### RDBMS 术语

在我们开始学习MySQL 数据库前，让我们先了解下RDBMS的一些术语：

- **数据库:** 数据库是一些关联表的集合。
- **数据表:** 表是数据的矩阵。在一个数据库中的表看起来像一个简单的电子表格。
- **列:** 一列(数据元素) 包含了相同类型的数据, 例如邮政编码的数据。
- **行：**一行（=元组，或记录）是一组相关的数据，例如一条用户订阅的数据。
- **冗余**：存储两倍数据，冗余降低了性能，但提高了数据的安全性。
- **主键**：主键是唯一的。一个数据表中只能包含一个主键。你可以使用主键来查询数据。
- **外键：**外键用于关联两个表。
- **复合键**：复合键（组合键）将多个列作为一个索引键，一般用于复合索引。
- **索引：**使用索引可快速访问数据库表中的特定信息。索引是对数据库表中一列或多列的值进行排序的一种结构。类似于书籍的目录。
- **参照完整性:** 参照的完整性要求关系中不允许引用不存在的实体。与实体完整性是关系模型必须满足的完整性约束条件，目的是保证数据的一致性。

MySQL 为关系型数据库(Relational Database Management System), 这种所谓的"关系型"可以理解为"表格"的概念, 一个关系型数据库由一个或数个表格组成, 如图所示的一个表格:

![](C:\Users\丁会想\Desktop\0921_1.jpg)

- 表头(header): 每一列的名称;
- 列(col): 具有相同数据类型的数据的集合;
- 行(row): 每一行用来描述某条记录的具体信息;
- 值(value): 行的具体信息, 每个值必须与该列的数据类型相同;
- **键(key)**: 键的值在当前列中具有唯一性。

