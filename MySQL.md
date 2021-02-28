# MySQL

[toc]

## 1. 准备工作

### 1.1启动与连接数据库

- cmd

  ```bash
  mysql -u (username) -p -h (myserver) -P (端口号) 
  ```

- mysql command

  ```
  输入密码即可
  ```

### 1.2 创建数据源

- WorkBench  (create schema)

  ![image-20210201125839185](C:\Users\LiaoLong\AppData\Roaming\Typora\typora-user-images\image-20210201125839185.png)

- 运行sql脚本

  ```bash
  source D:\LiaoLong\SQL\mysql_scripts\create.sql
  source D:\LiaoLong\SQL\mysql_scripts\populate.sql
  ```

## 2.SQL语法语句

- 分号**；**用来结束SQL语句，但可以不必每一句都加分号

- 不区分大小写，但好习惯是关键字大写
- 空格会被忽略
- 行数从0开始计数

### 2.1使用数据库

```bash
USE crashcourse;
```

#### 2.1.1 显示可用数据库列表

```bash
SHOW DATABASES;
```

#### 2.1.2 显示数据库内的表

```bash
SHOW TABLES;   #(先USE 选择数据库)
```

#### 2.1.3 显示表列1

```bash
SHOW COLUMNS FROM customers;
```

#### 2.1.4 显示表列2

```bash
DESCRIBE customers;
```

#### 2.1.5 显示广泛的服务器状态

```bash
SHOW STATUS;
```

#### 2.1.6 显示授予用户

```bash
SHOW GRANTS;
```

#### 2.1.7 显示错误/警告

```bash
SHOW ERROS/WARNINGS;
```

#### 2.1.8 帮助

```bash
HELP SHOW;
```

#### 2.1.9 和过滤模式信息

```bash
INFORMATION_SCHEMA;
```

### 2.2 SELECT

#### 2.2.1 检索单个列

```bash
SELECT prod_name 
FROM products; # 检索出来的数据排序不确定
```

#### 2.2.2 检索多个列

```bash
SELECT prod_id, prod_name, prod_price 
FROM products;
```

#### 2.2.3 检索所有列

```bash
SELECT *
FROM products;  # 非必需，不必检索所有列，但可以以此检索出不确定的列名
```

#### 2.2.4 检索不同的行（distinct)

```bash
SELECT DISTINCT vend_id  
FROM products;   # distinct 放于列前，应用于所有列
```

### 2.3 限制结果（limit）

```bash
# 1
SELECT prod_name
FROM products
LIMIT 5;

# 2
SELECT prod_name
FROM products
LIMIT 4, 5;   # 第4行开始，输出5行

## 表中只有3行却要输出5行时，输出3行
## 等价语句
LIMIT 4，5  =  LIMIT 5 OFFSET 4
```

### 2.4 完全限定的表名

```bash
# 1
SELECT products.prod_name
FROM products;

# 2
SELECT products.prod_name
FROM crashcourse.products;
```

### 2.5 排序数据（older by）

```bash
# 按字母顺序排序
SELECT prod_name
FROM products
ORDER BY prod_name;  # 可以选择按非显示列进行排序
```

#### 2.5.1 按多个列排序

```bash
SELECT prod_id, prod_price, prod_name
FROM products
ORDER BY prod_price, prod_name;
```

#### 2.5.2 指定排序方向（DESC）

```bash
# 1 
SELECT prod_id, prod_price, prod_name
FROM products
ORDER BY prod_price DESC;

# 2  多个列都有降序排序时，每个列都要指定DESC关键字
SELECT prod_id, prod_price, prod_name
FROM products
ORDER BY prod_price DESC, prod_name;

#3 ASC：升序排序

#4 字母A，a的先后顺序默认是一样的，但数据库管理员可以人为改变这种顺序
#5 
```

#### 2.5.3 ORDER BY 与 LIMIT结合

```bash
# 1.price最大值
# ORDER BY 在 FROM 之后，DESC在ORDER BY之后
SELECT prod_price
FROM products
ORDER BY prod_price DESC
LIMIT 1;
```

### 2.6 搜索过滤(WHERE条件语句)

```bash
# 1.条件操作符
=
<>   不等于
!=   不等于
<
<=
>
>=
BETWEEN 在指定的两个值之间
```

#### 2.6.1 where (在order by之前 )

```bash
# 1.表名之后给出
SELECT prod_name, prod_price
FROM products
WHERE prod_price = 2.50;

# 2.检测单个值
SELECT prod_name, prod_price
FROM products
WHERE prod_name = 'fuses'; # 不区分大小写

# 3.不匹配检查 
SELECT vend_id, prod_name
FROM products
WHERE vend_id <> 1003; # 不能过滤掉NULL值
  # 或者
SELECT vend_id, prod_name
FROM products
WHERE vend_id != 1003; # 不能过滤掉NULL值

# 4.范围检查between
SELECT prod_name, prod_price
FROM products
WHERE prod_price BETWEEN 5 AND 10;

# 5.空值检查 is null
SELECT prod_name
FROM products
WHERE prod_price IS NULL;
```

#### 2.6.2 组合WHERE子句

```bash
# 1.AND
SELECT prod_id, prod_price, prod_name
FROM products
WHERE vend_id = 1003 AND prod_price <= 10;

# 2.OR
SELECT prod_name, prod_price
FROM products
WHERE vend_id = 1002 OR vend_id = 1003;

# 3.计算次序问题 : AND优先
SELECT prod_name, prod_price
FROM products
WHERE vend_id = 1002 OR vend_id = 1003 AND prod_price >= 10;
```

#### 2.6.3 IN操作符

```bash
SELECT prod_name, prod_price
FROM products
WHERE vend_id IN (1002, 1003)
ORDER BY prod_name;

# in可以和or相互转换
# 相比or，in的优点
  1.选项清单较长时，in更清楚直观
  2.计算次序容易管理
  3.比or快
  4.in可以包含其他SELECT语句
```

#### 2.6.4 NOT操作符

```bash
SELECT prod_name, prod_price
FROM products
WHERE vend_id NOT IN (1002, 1003)
ORDER BY prod_name;

# 在MySQL中，NOT可以对IN、BETWEEN、EXISTS子句取反
```

### 2.7 通配符(结合LIKE)

```bash
 % ：表示任何字符出现任意次数(即可为零)，不可匹配null
 	 尾空格会干扰%的匹配，可以在最后再加一个%
 _ : 匹配单个字符,不能多也不能少
 
 ## 注意
  # 不能过度使用通配符
  # 最好不要通配符放在搜索模式的开始处，否则会使得搜索变慢
  # 注意通配符的位置
```

#### 2.7.1 LIKE

```bash
## 对于LIKE，匹配是完全匹配，即列值要一个字符都不能有差别才可以返回该行
# 1.使用一个%
SELECT prod_id, prod_name
FROM products
WHERE prod_name LIKE 'jet%'; # 可根据MySQL的配置方式，使得字母区分大小写

# 2.使用两个%
SELECT prod_id, prod_name
FROM products
WHERE prod_name LIKE '%anvil%';

# 3.使用_
SELECT prod_id, prod_name
FROM products
WHERE prod_name LIKE '_ ton anvil';
```

#### 2.7.2 正则表达式

```bash
## REGEXP
 # .  ：匹配任意字符（一个）
 # 匹配不区分大小写
 # |  ： （正则）| (正则) 两者满足其一即可
 # [123]: 匹配1或2或3
 SQL中\\用来转义
 # \\f换页
 # \\n换行
 # \\r回车
 # \\t制表
 # \\v纵向制表
 # \\\  表示 \
 字符类
 # [:alnum:] : [a-zA-Z0-9]
 # [:alpha:] : [a-zA-Z]
 # [:blank:] : 空格和制表
 # [:cntrl:] : ASCII控制字符（ASCII 0到31和127）
 # [:digit:] : [0-9]
 # [:graph:] : 与[:print:]相同，但不包括空格
 # [:lower:] : [a-z]
 # [:print:] : 任意可打印字符
 # [:punct:] : 不是[:alnum:]也不是[:cntrl:]
 # [:space:] : 空白字符（空格、\\f、\\n、\\r、\\t、\\v）
 # [:upper:] : [A-Z]
 # [:xdigit:] : [a-fA-F0-9]
 数量
 # *
 # +
 # ?
 # {n}
 # {n,}
 # {n,m}
 定位符
 # ^ : 文本的开始
 # $ ： 文本的结尾
 # [[:<:]] : 词的开始
 # [[:>:]] : 词的结尾
```

#### 2.7.3 基本字符匹配

```bash
# 1
SELECT prod_name
FROM products
WHERE prod_name REGEXP '1000'
ORDER BY prod_name;

# 2  .
SELECT prod_name
FROM products
WHERE prod_name REGEXP '.000'
ORDER BY prod_name;

# like与正则表达式的区别
SELECT prod_name
FROM products
WHERE prod_name LIKE '1000'  # 不返回
ORDER BY prod_name;

SELECT prod_name
FROM products
WHERE prod_name REGEXP '1000'  #模糊匹配，返回一行
ORDER BY prod_name;

# |
SELECT prod_name
FROM products
WHERE prod_name REGEXP '1000|2000';

# [123]
SELECT prod_name
FROM products
WHERE prod_name REGEXP '[123] ton'
ORDER BY prod_name;

# [1-5]
SELECT prod_name
FROM products
WHERE prod_name REGEXP '[1-5] ton'
ORDER BY prod_name;

# \\.  MySQL中\\用来转义
SELECT vend_name
FROM vendors
WHERE vend_name REGEXP '\\.'
ORDER BY vend_name;

# 匹配多个,stick或者sticks
SELECT prod_name
FROM products
WHERE prod_name REGEXP '\\([0-9] sticks?\\)'
ORDER BY prod_name;

# 匹配4为数字
SELECT prod_name
FROM products
WHERE prod_name REGEXP '[[:digit:]]{4}'
ORDER BY prod_name;

# 文本起始
SELECT prod_name
FROM products
WHERE prod_name REGEXP '^[0-9\\.]'
ORDER BY prod_name;

# 正则表达式测试
SELECT 'hello' REGEXP '[0-9]';  # 返回0（匹配失败）1（匹配成功）
```

### 2.8 创建计算字段

```bash
#####
```

#### 2.8.1 拼接Concat()

```bash
# concat():多数DBMS使用+或者||来实现拼接，MySQL使用Concat()
SELECt Concat(vend_name, ' (', vend_country, ')')
FROM vendors
ORDER BY vend_name;
```

#### 2.8.2 RTrim()

```bash
## 删除右侧多余空格
SELECT Concat(RTrim(vend_name), ' (', RTrim(vend_country), ')')
FROM vendors
ORDER BY vend_name;

## 删除左侧多余空格
LTrim()

## 删除两侧多余空格
Trim()
```

#### 2.8.3 使用别名 AS

```bash
# 起别名，给客户机应用引用
SELECT Concat(RTrim(vend_name), ' (', RTrim(vend_country), ')') AS
vend_title
FROM vendors
ORDER BY vend_name;
```

#### 2.8.4 算术计算

```bash
SELECT prod_id, 
	   quantity, 
	   item_price,
	   quantity*item_price AS expanded_price
FROM orderitems
WHERE order_num = 20005;
```

### 2.9 使用数据处理函数

```bash
# 函数移植性不强
```

#### 2.9.1 文本处理函数

```bash
# Upper()   转换为大写
SELECT vend_name, Upper(vend_name) AS vend_name_upcase
FROM vendors
ORDER BY vend_name;

# Left()       返回串左边的字符

# Length()     返回串长度
# Locate()     找出串中的一个字串
# Lower()      转换为小写
# LTrim()      去掉左边空格
# Right()      返回串右边的字符
# RTrim()      去掉右边空格
# Soundex()    返回串的SOUNDEX值
SELECT cust_name, cust_contact
FROM customers
WHERE Soundex(cust_contact) = Soundex('Y.Lie');
# SubString()  返回子串的字符
# Upper()      转换为大写
```

#### 2.9.2 日期与时间处理

```bash
日期格式
# yyyy-mm-dd  首选日期格式
# MySQL的处理方式：00-69 ---> 2000-2069, 70-99 ---> 1970-1999
SELECT cust_id, order_num
FROM orders
WHERE order_date = '2005-09-01';

日期处理函数
# AddDate()     
# AddTime()
# CurDate()
# CurTime()
# Date()
SELECT cust_id, order_num
FROM orders
WHERE Date(order_date) = '2005-09-01';

SELECT cust_id, order_num
FROM orders
WHERE Date(order_date) BETWEEN '2005-09-01' AND '2005-09-30';

SELECT cust_id, order_num
FROM orders 
WHERE Year(order_date) = 2005 AND Month(order_date) = 9;
# DateDiff()
# Date_Add()
# Date_Format()
# Day()
# DayOfWeek()
# Hour()
# Minite()
# Month()
# Now()
# Second()
# Time()
# Year()
```

#### 2.9.3 数值处理函数

```bash
# Abs()
# Cos()
# Exp()
# Mod()
# Pi()       返回圆周率
# Rand()
# Sin()
# Sqrt()
# Tan()
```

### 2.10汇总数据

```bash
## ALL
## DISTINCT
```

#### 2.10.1 聚集函数

```bash
# AVG()  忽略列值为NULL的行
SELECT AVG(prod_price) AS avg_price
FROM products;

SELECT AVG(prod_price) AS avg_price
FROM products
WhERE vend_id = 1003;
# COUNT()  返回某列的行数，忽略NULL
SELECT COUNT(*) AS num_cust  # 使用*号，NULL值不会忽略
FROM customers;

SELECT COUNT(cust_email) AS num_cust
FROM customers;   # 忽略NULL值
# MAX()   忽略NULL，文本数据也可以MAX
SELECT MAX(prod_price) AS max_price
FROM products;
# MIN()  忽略NULL
# SUM()  忽略NULL
SELECT SUM(quantity) AS items_ordered
FROM orderitems
WHERE order_num = 20005;
```

#### 2.10.2 聚集与DISTINCT

```bash
#
SELECT AVG(DISTINCT prod_price) AS avg_price
FROM products
WHERE vend_id =1003;

# 对于COUNT(),需要指定列名，不能用于COUNT(*)
SELECT COUNT(DISTINCT prod_price) AS avg_price
FROM products
WHERE vend_id =1003;
```

#### 2.10.3 组合聚集函数

```bash
SELECT COUNT(*) AS num_items,
	   MIN(prod_price) AS price_min,
	   Max(prod_price) AS price_max,
	   AVG(prod_price) AS price_avg
FROM products;
```

### 2.11 分组数据

```bash

```

#### 2.11.1 GROUP BY

```bash
SELECT vend_id, COUNT(*) AS num_prods
FROM products
GROUP BY vend_id;

SELECT vend_id, COUNT(*) AS num_prods
FROM products
GROUP BY vend_id WITH ROLLUP;

# GROUP BY子句可以包含任意数目的列。这使得能对分组进行嵌套，为数据分组提供更细致的控制。
# 如果在GROUPBY子句中嵌套了分组，数据将在最后规定的分组上进行汇总。换句话说，在建立分组时，指定的所有列都一起计算（所以不能从个别的列取回数据）。
# GROUP BY子句中列出的每个列都必须是检索列或有效的表达式（但不能是聚集函数）。如果在SELECT中使用表达式，则必须在GROUP BY子句中指定相同的表达式。不能使用别名。
# 除聚集计算语句外，SELECT语句中的每个列都必须在GROUPBY子句中给出。
# 如果分组列中具有NULL值，则NULL将作为一个分组返回。如果列中有多行NULL值，它们将分为一组。
# GROUP BY子句必须出现在WHERE子句之后，ORDER BY子句之前。
# 使用ROLLUP 使用WITH ROLLUP关键字，可以得到每个分组以及每个分组汇总级别（针对每个分组）的值，如下所示：
```

#### 2.11.2 HAVING 

```bash
1. 对分组操作,把分组看成一个新的表，挑选满足条件的组
2. HAVING和WHERE的差别这里有另一种理解方法，WHERE在数据分组前进行过滤，HAVING在数据分组后进行过滤。这是一个重要的区别，WHERE排除的行不包括在分组中。这可能会改变计算值，从而影响HAVING子句中基于这些值过滤掉的分组。
```

```bash
# 1
SELECT cust_id, COUNT(*) AS orders
FROM orders
GROUP BY cust_id
HAVING COUNT(*) >= 2;

# 2
SELECT vend_id, COUNT(*) AS num_prods
FROM products
WHERE prod_price >= 10
GROUP BY vend_id
HAVING COUNT(*) >= 2;
```

#### 2.11.3 分组与排序

![image-20210202124706607](C:\Users\LiaoLong\AppData\Roaming\Typora\typora-user-images\image-20210202124706607.png)

```bash
## GROUP BY子句后，应该也给出ORDER BY 子句，不能仅依赖GROUP BY排序数据

# 1
SELECT order_num, SUM(quantity*item_price) AS ordertotal
FROM orderitems
GROUP BY order_num
HAVING SUM(quantity*item_price) >= 50
ORDER BY ordertotal;
```

#### 2.11.4 SELECT子句顺序

|   子句   |        说明        |      是否必须使用      |
| :------: | :----------------: | :--------------------: |
|  SELECT  | 要返回的列或表达式 |           是           |
|   FROM   |  从中检索数据的表  | 仅在从表选择数据时使用 |
|  WHERE   |      行级过滤      |           否           |
| GROUP BY |      分组说明      | 仅在按组计算聚集时使用 |
|  HAVING  |      组级过滤      |           否           |
| ORDER BY |    输出排序顺序    |           否           |
|  LIMIT   |    要检索的行数    |           否           |

### 2.12 子查询

```bash

```

#### 2.12.1 利用子查询过滤

```bash
# 1  包含TNT2的订单号
SELECT order_num
FROM orderitems
WHERE prod_id = 'TNT2';

# 2 具有#1订单号的客户ID
SELECT cust_id
FROM orders
WHERE order_num IN (20005, 20007);

# 3  （#1  #2）组合
SELECT cust_id
FROM orders
WHERE order_num IN (SELECT order_num
					FROM orderitems
					WHERE prod_id = 'TNT2');
# 4

```

#### 2.12.2 作为计算字段使用子查询

```bash
# 1
SELECT COUNT(*) AS orders
FROM orders
WHERE cust_id = 10001;

# 2  相关子查询
SELECT cust_name,
       cust_state,
       (SELECT COUNT(*)
       FROM orders
       WHERE orders.cust_id = customers.cust_id) AS orders
FROM customers
ORDER BY cust_name;
```

### 2.13 连接表

```bash
# 主键
# 外键
# 可伸缩性
# 维护引用完整性
# 笛卡尔积
# 叉联结
```

#### 2.13.1 创建联结

```bash
# 应该保证所有联结都有where子句
SELECT vend_name, prod_name, prod_price
FROM vendors, products
WHERE vendors.vend_id = products.vend_id  # where子句很重要
ORDER BY vend_name, prod_name;
```

#### 2.13.2 内部联结(INNER JOIN)

```bash
# ANSI SQL规范首选INNER JOIN
SELECT vend_name, prod_name, prod_price
FROM vendors INNER JOIN products
ON vendors.vend_id = products.vend_id;
```

#### 2.13.3 联结多个表

```bash
#  考虑到性能问题，不要联结不必要的表
SELECT prod_name, vend_name, prod_price, quantity
FROM orderitems, products, vendors
WHERE products.vend_id = vendors.vend_id
  AND orderitems.prod_id = products.prod_id
  AND order_num = 20005;
```

### 2.16 高级联结

```bash

```

#### 2.16.1 使用表别名

```bash
# 可以不止一次引用表别名，即可以给一个表起多个名字
SELECT cust_name, cust_contact
FROM customers AS c, orders AS o, orderitems AS oi
WHERE c.cust_id = o.cust_id
  AND oi.order_num = o.order_num
  AND prod_id = 'TNT2';
  
```

#### 2.16.2 自联结

```bash
# 有时候处理自联结远比处理子查询要快得多
SELECT p1.prod_id, p1.prod_name
FROM products AS p1, products AS p2
WHERE p1.vend_id = p2.vend_id
  AND p2.prod_id = 'DTNTR';
```

#### 2.16.3 自然联结

```bash
SELECT c.*, o.order_num, o.order_date
	   oi.prod_id, oi.quantity, oi.item_price
FROM customers AS c, orders AS o, orderitems AS oi
WHERE c.cust_id = o.cust_id
  AND oi.order_num = o.order_num
  AND prod_id = 'FB';
```

#### 2.16.4 外部联结（LEFT OUTER JOIN）

```bash
# MySQL没有简化字符*=和=*
SELECT customers.cust_id, orders.order_num
FROM customers RIGHT OUTER JOIN orders
ON customers.cust_id = orders.cust_id;
```

#### 2.16.5 使用带聚集函数的联结

```bash
SELECT customers.cust_name
	   customers.cust_id
	   COUNT(orders.order_name) AS num_ord
FROM customers INNER JOIN orders
ON customers.cust_id = orders.cust_id
GROUP BY customers,cust_id;
```

#### 2.16.6 使用联结和联结条件

```bash
#  一般使用内部联结
#  需提供联结条件，否则笛卡尔积
#  
#
#
```

### 2.17 组合查询

```bash
# 并或复合查询
```

#### 2.17.1 创建组合查询

```bash
# UNION 可应用于不同的表
# UNION 必须由两条或两条以上的SELECT语句
#       SELECT包含相同的列、表达式或聚集函数（可以不同的顺序列出）
#       列数据兼容
SELECT vend_id, prod_id, prod_price
FROM products
WHERE prod_price <= 5
UNION
SELECT vend_id, prod_id, prod_price
FROM products
WHERE vend_id IN (1001, 1002);
```

#### 2.17.2 包含或取消重复的行

```bash
# UNION默认将重复的行取消
# 若有需要，可以返回所有匹配行
SELECT vend_id, prod_id, prod_price
FROM products
WHERE prod_price <= 5
UNION ALL
SELECT vend_id, prod_id, prod_price
FROM  products
WHERE vend_id IN (1001, 1002);
```

#### 2.17.3 对组合查询结果排序

```bash
# UNION组合查询，只能有一个ORDER BY子句，且再最后，对全部结果进行排序
SELECT vend_id, prod_id, prod_price
FROM products
WHERE prod_price <= 5
UNION 
SELECT vend_id, prod_id, prod_price
FROM  products
WHERE vend_id IN (1001, 1002)
ORDER BY vend_id, prod_price;
```

### 2.18 全文本搜索

```bash
# MyISAM 支持全文本搜索
# InnoDB  不支持全文本搜索
# MySQL带有一个内建的非用词（stopword）列表，这些词在索引全文本数据时总是被忽略
# 50% 规则： 一个词出现在50%以上的行中，则将它作为一个非用词忽略，此规则不用于IN BOOLEAN MODE

# 邻近操作符  暂未知情况
```

#### 2.18.1 启用全文本搜索

```bash
# 创建表时（CREATE TABLE）启用
# 导入数据到一个新表时，因为更新一个索引需要时间，故先导入所有数据后再修改表，有助于更快地导入数据

CREATE TABLE productnotes 
(
	note_id     int 		 NOT NULL  AUTO_INCREMENT, 
	prod_id     char(10)	 NOT NULL, 
	note_date   datetime     NOT NULL, 
	note_text   text         NULL, 
	PRIMARY  KEY(note_id), 
	FULLTEXT(note_text)
)ENGINE=MyISAM;
```

#### 2.18.2 进行全文本搜索

```bash
# Match() 传递给Match的值应与FULLTEXT()中的值相同，多指定多个列，次序也要一致
# 除非BINARY方式，否则不区分大小写
# Against()

# 1
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('rabbit'); # 返回结果排列次序取决于匹配度

# 2 匹配度
SELECT note_text, 
       Match(note_text) Against('rabbit') AS rank
FROM productnotes;
```

#### 2.18.3 使用查询扩展

```bash
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('anvils' WITH QUERY EXPANSION);
```

#### 2.18.4 布尔文本搜索

```bash
# 没有FULLTEXT索引也可以使用， 但很慢
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('heavy -rope*' IN BOOLEAN MODE);

#
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('+rabbit +bait' IN BOOLEAN MODE);

#  >  <
SELECT note_text FROM productnotes 
WHERE Match(note_text)  Against('>rabbit <carrot' IN BOOLEAN MODE);
```

| 布尔操作符 |                             说明                             |
| :--------: | :----------------------------------------------------------: |
|     +      |                       包含，词必须存在                       |
|     -      |                      排除，词必须不出现                      |
|     >      |                     包含，并且增加等级值                     |
|     <      |                     包含，并且减少等级值                     |
|    （）    | 把词组成子表达式（允许这些子表达式作为一个组被包含、<br/>排除、排列等） |
|     ~      |                      取消一个词的排序值                      |
|     *      |                          刺猬通配符                          |
|    " "     | 定义一个短语（与单个词的列表不一样，它匹配整个短语以便包含或排除这个短语） |

### 2.19 插入数据

```bash

```

#### 2.19.1 插入完整的行

```bash
# 不安全
INSERT INTO customers VALUES(NULL, 'Pep E. LaPew', '100 Main Street', 'Los Angeles', 'CA','90046','USA',NULL,NULL);

# 安全
INSERT INTO customers(cust_name, cust_address, cust_city, cust_state, cust_zip, cust_country, cust_contact, cust_email) VALUES(NULL, 'Pep E. LaPew', '100 Main Street', 'Los Angeles', 'CA','90046','USA',NULL,NULL);

# 插入时可省略一些列而不给其赋值，省略的列应可以为NULL或者设置了默认值

# 降低INSERT的优先级
INSERT LOW_PRIORITY INTO  # 也适用于UPDATE、DELETE
```

#### 2.19.2 插入多个行

```bash
# 将插入的值用逗号隔开，插入多行时，应使用该方法
INSERT INFO customers VALUES(NULL, 'Pep E. LaPew', '100 Main Street', 'Los Angeles', 'CA','90046','USA',NULL,NULL), (...插入的值...);
```

#### 2.19.3 插入检索出的数据

```bash
# 将SELECT结果插入表中

```

### 2.20 UPDATE和DELETE

```mysql
# UPDATE
UPDATE customers
SET cust_email = 'elmer@fudd.com'
WHERE cust_id = 10005;

UPDATE customers
SET cust_name = 'The Fudds',
	cust_email = 'elmer@fudd.com'
WHERE cust_id = 10005;

# IGNORE  忽略更新错误继续更新
UPDATE IGNORE customers

# DELETE  只是删除表的行内容，不会删除表本身
DELETE FROM customers
WHERE cust_id = 10006;

# TRUNCATE
TRUNCATE TABLE 删除原来的表，并创建一个新表


#### 使用原则
除非确实打算更新和删除每一行，否则绝对不要使用不带WHERE子句的UPDATE或DELETE语句。

保证每个表都有主键（如果忘记这个内容，请参阅第15章），尽可能像WHERE子句那样使用它（可以指定各主键、多个值或值的范围）。

在对UPDATE或DELETE语句使用WHERE子句前，应该先用SELECT进行测试，保证它过滤的是正确的记录，以防编写的WHERE子句不正确。

使用强制实施引用完整性的数据库（关于这个内容，请参阅第15章），这样MySQL将不允许删除具有与其他表相关联的数据的行。
```

### 2.21 创建和操纵表

```bash
# PRIMARY KEY
  可以有多个
  不可为NULL允许列
  可在表创建后定义
```

#### 2.21.1 auto_increment 

```bash
# 自动增量，添加行时，自动为该行分配下一个可用编号  # 修饰列（属性）

# 每个表只允许一个AUTO_INCREMENT列，且必须被索引（如成为主键）

# 返回最后一个auto_increment值
SELECT last_insert_id()
```

#### 2.21.2 指定默认值

```bash
DEFAULT 1
```

#### 2.21.3 引擎类型

```bash
# 1 InnoDB
事务处理引擎，不支持全文本搜索

# 2 MEMORY
与MyISAM功能相同，数据存储在内存中，速度快

# 3 MyISAM
支持全文本搜索，不支持事务处理

## 注意
外键不能跨引擎
```

#### 2.21.4 更新表（结构）

```bash
# 添加列
ALTER TABLE vendors
ADD vend_phone CHAR(20);

# 删除列
ALTER TABLE vendors
DROP COLUMN vend_phone;

# 定义外键
ALTER TABLE orderitems 
ADD CONSTRAINT fk_orderitems_orders 
FOREICN KEY(order_num)REFERENCES orders (order_num); 

ALTER TABLE orderitems 
ADD CONSTRAINT fk_orderitems_products 
FOREICN KEY (prod_id)
REFERENCES products (prod_id); 

ALTER TABLE orders ADD CONSTRAINT fk_orders_customers 
FOREIGN KEY (cust_id)
REFERENCES cuStomers (cust_id); 

ALTER TABLE products ADD CONSTRAINT fk_products_vendors FOREICN KEY (vend_id)REFERENCES vendors (vend_id);
```

#### 2.21.5 删除表

```bash
DROP TABLE customers2;
```

#### 2.21.6 重命名表

```bash
RENAME TABLE customers2 To customers;

RENAME TABLE backup_customers TO customers,
			 backup_vendors TO vendors,
			 backup_products TO products;
```

### 2.22 使用视图

```bash
# 视图创建
CREATE VIEW

# 查看创建视图的语句
SHOW CREATE VIEW viewname;

# 删除视图
DROP VIEW viewname;

# 更新视图
CREATE OR REPLACE VIEW
```

#### 2.22.1 视图简化复杂的联结

```bash
# 创建
CREATE VIEW productcustomers AS
SELECT cust_name, cust_contact, prod_id
FROM customers, orders, orderitems
WHERE customers.cust_id = orders.cust_id
  AND orderitems.order_num = orders.order_num;
  
# 使用视图
SELECT cust_name, cust_contact
FROM productcustomers
WHERE prod_id = 'TNT2';

```

#### 2.22.2 用视图格式化检索出的数据

```bash
CREATE VIEW vendorlocatios AS
SELECT Concat(Rtrim(vend_name), '(', RTrim(vend_country), ')')
       AS vend_title
FROM vendors
ORDER BY vend_name;

SELECT * 
FROM vendorlocatios;
```

#### 2.22.3 用视图过滤不想要的数据

```bash
CREATE VIEW customeremaillist AS
SELECT cust_id, cust_name, cust_email
FROM customers
WHERE cust_email IS NOT NULL;

SELECT *
FROM customeremaillist;
```

#### 2.22.4 使用视图与计算字段

```bash
CREATE VIEW orderitemsexpanded AS
SELECT order_num,
       prod_id,
       quantity,
       item_price,
       quantity*item_price AS expanded_price
FROM orderitems;

SELECT * 
FROM orderitemsexpanded 
WHERE order_num = 20005;
```

#### 2.22.5 更新视图

```bash
# 更新的是基表

# 不能更新的视图（有以下操作）
分组
联结
子查询
并
聚集函数
DISTINCT
导出（计算）列
```

### 2.23 使用存储过程

```bash

```

#### 2.23.1  创建和执行存储过程（CALL）

```bash
# 在mysql命令行，应该先临时更改语句分隔符
DELIMITER //

# 创建（命令行执行）
CREATE PROCEDURE productpricing()   # 括号内填的是参数
BEGIN
	SELECT Avg(prod_price) AS priceaverage
	FROM products;
END //

# 执行
CALL productpricing();  # 如果有参数，括号内以“@参数”的形式并以逗号分隔添加参数
```

#### 2.23.2 删除存储过程

```bash
DROP PROCEDURE productpricing;

DROP PROCEDURE IF EXISTS productpricing;  # 不存在过程也不会报错
```

#### 2.23.3 过程中使用参数

```bash
# 创建
CREATE PROCEDURE productpricing(
	OUT pl DECIMAL(8, 2),
	OUT ph DECIMAL(8, 2),
	OUT pa DECIMAL(8, 2)
)
BEGIN
	SELECT Min(prod_price)
	INTO pl
	FROM products;
	SELECT Max(prod_price)
	INTO ph
	FROM products;
	SELECT Avg(prod_price)
	INTO pa
	FROM products;
END //

# 执行
CALL productpricing(@pl,    # call的时候参数可以不和过程中的参数名字一致
					@ph,    # 实际存储的参数应该是call中的参数名字
					@pa);

# 显示
SELECT @pa;

# IN/OUT
CREATE PROCEDURE ordertotal(
	IN onumber INT,
	OUT ototal DECIMAL(8, 2)
)
BEGIN
	SELECT Sum(item_price*quantity)
	FROM orderitems
	WHERE order_num = onumber
	INTO ototal;
END //

CALL ordertotal(20005, @total);
```

#### 2.23.4 建立智能存储过程

```bash
#  -- 表示注释
# SHOW PROCEDURE STATUS可以显示comment后面的信息
# declare : 声明局部变量

-- Name: ordertotal
-- Parameters: onumber = order number
-- 			   taxable = 0 if not taxable, 1 if taxable
--             ototal  = order total variable

CREATE PROCEDURE ordertotal(
	IN onumber INT,
	IN taxable BOOLEAN,
	OUT ototal DECIMAL(8, 2)
) COMMENT 'Obtain order total, optionally adding tax'    
BEGIN
	
	-- Declare variable for total
	DECLARE total DECIMAL(8, 2);
	-- Declare tax percentage
	DECLARE taxrate INT DEFAULT 6;
	
	-- Get the order total
	SELECT Sum(item_price*quantity)
	FROM orderitems
	WHERE order_num = onumber
	INTO total;
	
	-- Is this taxable?
	IF taxable THEN
		-- Yes, so add taxrate to the total
		SELECT total + (total/100*taxrate) INTO total;
	END IF;
	
	-- And finally, save to out variable
	SELECT total INTO ototal;
	
END //
```

#### 2.24.5 检查存储过程

```bash
SHOW CREATE PROCEDURE ordertotal;

SHOW PROCEDURE STATUS; # 此时会列出所有存储过程

SHOW PROCEDURE STATUS LIKE 'ordertotal';  # 利用like过滤存储过程
```

### 2.25 使用游标

```bash
# MySQL游标只能用于存储过程（和函数）

# 使用步骤
## 在能够使用游标前，必须声明（定义）它。这个过程实际上没有检索数据，它只是定义要使用的SELECT语句。
## 一旦声明后，必须打开游标以供使用。这个过程用前面定义的SELECT语句把数据实际检索出来。
## 对于填有数据的游标，根据需要取出（检索）各行。
## 在结束游标使用时，必须关闭游标。
```

#### 2.25.1创建游标

```mysql
CREATE PROCEDURE processorders()
BEGIN
	DECLARE ordernumbers CURSOR
	FOR
	SELECT order_num FROM orders;
END;
```

#### 2.25.2 打开与关闭游标

```mysql
OPEN ordernumbers;  -- 打开游标

CREATE PROCEDURE processorders()
BEGIN
	DECLARE ordernumbers CURSOR
	FOR
	SELECT order_num FROM orders;
	
	OPEN ordernumbers;
	
	CLOSE ordernumbers;
END;//
```

#### 2.25.3 使用游标数据（FETCH）

```mysql
-- 1
CREATE PROCEDURE processorders()
BEGIN
	DECLARE o INT;
	
	DECLARE ordernumbers CURSOR
	FOR
	SELECT order_num FROM orders;
	
	OPEN ordernumbers;
	
	FETCH ordernumbers INTO o;
	
	CLOSE ordernumbers;
END;//

-- 2
CREATE PROCEDURE processordeers()
BEGIN
	
	-- Declare local variables          -- 先声明局部变量
	DECLARE done BOOLEAN DEFAULT 0;
	DECLARE o INT
	DECLARE t DECIMAL(8, 2);
	
	-- Declare the cursor               -- 再声明游标
	DECLARE ordernumbers CURSOR
	FOR
	SELECT order_num FROM orders;
	
	-- Declare continue handler         -- 最后声明句柄
	DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET done = 1;
	
	-- Create a table to store the results
	CREATE TABLE IF NOT EXISTS ordertotals
		(order_num INT, 
         total DECIMAL(8, 2));
	
	-- Open the cursor
	OPEN ordernumbers;
	
	-- Loop through all rows
	REPEAT
	
		--Get order number
		FETCH ordernumbers INTO o;
		
		-- Get the total for this order
		CALL ordertotal(o, 1, t);
		
		-- Insert order and total into ordertotals
		INSERT INTO ordertotals(order_num, total)
		VALUES(o, t);
		
	-- End of loop
	UNTIL done END REPEAT;
	
	-- Close the cursor
	CLOSE ordernumbers;
	
END; //
```

### 2.25 使用触发器

```mysql
-- DELETE
-- INSERT
-- UPDATE

-- 只有表才支持触发器，视图、临时表均不支持
-- 一个表最多支持6个触发器，一个触发器不能和多个事件或多个表关联
	-- 	INSERT 之前之后  2个
	--  UPDATE 之前之后  2个
	--  DELETE 之前之后  2个
```

#### 2.25.1 创建触发器

```mysql
CREATE TRIGGER newproduct AFTER INSERT ON products
FOR EACH ROW SELECT 'Product added';
```

#### 2.25.2 删除触发器

```mysql
DROP TRIGGER newproduct;  -- 触发器不可被更新或覆盖
```

#### 2.25.3 使用触发器

```mysql
-- INSERT 触发器
在INSERT触发器代码内，可引用一个名为NEW的虚拟表，访问被插入的行；
在BEFOREINSERT触发器中，NEW中的值也可以被更新（允许更改被插入的值）；
对于AUTO_INCREMENT列，NEW在INSERT执行之前包含0，在INSERT执行之后包含新的自动生成值。

-- 返回auto_increament新生成的值
CREATE TRIGGER neworder AFTER INSERT ON orders
FOR EACH ROW SELECT NEW.order_num;

-- error: Not allowed to return a result set from a trigger
改为
CREATE TRIGGER neworder AFTER INSERT ON orders
FOR EACH ROW SELECT NEW.order_num INTO @newNUM;

INSERT INTO orders(order_date, cust_id)
VALUES(Now(), 10001);

SELECT @newNUM;

-- *------------------------------------------------* --

-- DELETE触发器
在DELETE触发器代码内，你可以引用一个名为0LD的虚拟表，访问被删除的行；
OLD 中的值全都是只读的，不能更新

CREATE TRIGGER deleteorder BEFORE DELETE ON orders
FOR EACH ROW
BEGIN
	INSERT INTO archive_orders(order_num, order_date, cust_id)
	VALUES(OLD.order_num, OLD.order_date, OLD.cust_id);
END;

-- UPDATE触发器
# 在 UPDATE 触发器代码中，你可以引用一个名为 OLD 的虚拟表访问以前（ UPDATE 语句前）的值，引用一个名为 NEW 的虚拟表访问新更新的值；
# 在 BEFORE UPDATE 触发器中， NEW 中的值可能也被更新（允许更改将要用于 UPDATE 语句中的值）；
# OLD 中的值全都是只读的，不能更新。

CREATE TRIGGER updatevendor BEFORE UPDATE ON vendors
FOR EACH ROW SET NEW.vend_state = Upper(NEW.vend_state);
```

### 2.26 管理事物处理

```mysql
transaction  事物
rollback     回退
commit       提交
savepoint    保留点（可回退到该位置）
```

#### 2.26.1 ROLLBACK

```mysql
-- 事物开始
START TRANSACTION

-- ROLLBACK
# SELECT语句不能回退，CREATE、DROP也不能回退
SELECT * FROM ordertotals;
START TRANSACTION
DELETE FROM ordertotals;
SELECT * FROM ordertotals;
ROLLBACK;
SELECT * FROM ordertotals;
```

#### 2.26.2 COMMIT

```mysql
START TRANSACTION;
DELETE FROM orderitems WHERE order_num = 20010;
DELETE FROM orders WHERE order_num = 20010;
COMMIT;
```

#### 2.26.3 SAVEPOINT

```mysql
SAVEPOINT delete1;
ROLLBACK TO delete1;

savepoint 会在事务处理完成后自动释放（ROLLBACK或COMMIT）
RELEASE SAVEPOINT 明确释放保留点
```

#### 2.26.4 更改默认提交行为

```mysql
SET autocommit = 0;
```

### 2.27 全球化和本地化

```mysql
字符集
编码
校对  规定字符如何比较
```

#### 2.27.1 查看字符集

```mysql
SHOW CHARACTER SET;
```

#### 2.27.2 查看校对的完整列表

```mysql
SHOW COLLATION;
```

#### 2.27.3 指定字符集和校对

```mysql
SHOW VARIABLES LIKE 'character%';
SHOW VARIABLES LIKE 'collation%';

# 对整个表设置字符集和校对
CREATE TABLE mytable
(
    column1     INT,
    column2     VARCHAR(10)
) DEFAULT CHARACTER SET hebrew
  COLLATE hebrew_general_ci;
  
# 对每个列设置字符集和校对
CREATE TABLE mytable
(
	column1    INT,
    column2    VARCHAR(10),
    column3    VARCHAR(10) CHARACTER SET latin1 COLLATE latin1_general_ci
)DEFAULT CHARACTER SET hebrew
  COLLATE hebrew_general_ci;
  
# SELECT 子句设置校对  (group by  having  聚集函数  别名  均可指定校对)
SELECT * FROM customers
ORDER BY lastname, firstname COLLATE latin1_general_cs;
```

### 2.28 安全管理

```mysql

```

#### 2.28.1 显示用户

```mysql
USE mysql;
SELECT user FROM user;
```

#### 2.28.2 创建用户账号

```mysql
CREATE USER ben IDENTIFIED by 'p@$$w0rd';

RENAME USER ben TO bforta;
```

#### 2.28.3 删除用户账号

```mysql
DROP USER bforta;
```

#### 2.28.4 设置访问权限

```mysql
SHOW GRANTS FOR bforta;

# 授予权限
GRANT SELECT ON crashcourse.* TO bforta;   -- select只读权限
# 多次授权
GRANT SELECT， INSERT ON crashcourse.* TO bforta; 

# 撤销权限
REVOKE SELECT ON crashcourse.* FROM bforta;
```

#### 2.28.5 更改口令（密码）

```mysql
# 不指定用户名时，则为当前登录用户
SET PASSWORD FOR bforta = Password('n3w p@$$w0rd');  
```

### 2.29 数据库维护

```mysql

```

#### 2.29.1备份数据

```mysql
# 先刷新
FLUSH TABLES

-- mysqldump
-- mysqlhotcopy
-- BACKUP TABLE
-- SELECT INTO OUTFILE
-- RESTORE TABLE  复原数据
```

#### 2.29.2 数据库维护

```mysql
ANALYZE TABLE  :  检查表键是否正确

# 1
ANALYZE TABLE orders;


CHECK TABLE    :   对许多问题进行检查
CHANGED        :   检查最后一次见以来改动过的表
EXTENDED       :   彻底检查
FAST           :    检查未正常关闭的表
MEDIUM         ;    检查所有被删除的链接并键检验
QUICK          :    快速扫描
REPAIR TABLE   :    修复表
OPTIMIZE TABLE :    删除表中大量的数据后，用来收回所用的空间，优化表的性能
```

#### 2.29.3 诊断启动问题

```mysql

```

#### 2.29.4 查看日志文件

```mysql
-- 错误日志
hostname.err   data目录中
--log-error更改日志名
-- 查询日志
hostname.log   data目录中
--log 更改日志名
-- 二进制日志
hostname-bin    data目录中
--log-bin  更改日志名
-- 缓慢查询日志
hostname-slow.log   data目录中
--log-slow-queries更改


FLUSH LOGS  刷新和重新开始所有日志文件
```

#### 2.2

```mysql

```

#### 2.2

```mysql

```



## 3. 遇到的问题

### 3.1 连接问题

#### 3.1.1 MySQL配置

问题：idea建立了一个普通的Java项目，通过JDBC与MySQL数据库连接，出现了以下错误信息

> Thu Feb 04 09:14:48 CST 2021 WARN: Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default if explicit option isn't set. For compliance with existing applications not using SSL the verifyServerCertificate property is set to 'false'. You need either to explicitly disable SSL by setting useSSL=false, or set useSSL=true and provide truststore for server certificate verification.

配置信息如下

```java
private static final String DBDRIVER = "com.mysql.jdbc.Driver";
private static final String DBURL ="jdbc:mysql://localhost:3306/crashcourse";
private static final String USER = "root";
private static final String PASSWORD = "lllovezy";
```

解决办法:url添加useSSL=false

```java
private static final String DBURL = "jdbc:mysql://localhost:3306/crashcourse?useSSL=false";
```

### 3.2 sql语法问题

#### 3.2.1 varchar 与 char的区别

[varchar与char](https://zhuanlan.zhihu.com/p/63005458)

在MYSQL中，char是指:使用指定长度的固定长度表示字符串的一种字段类型；比如char（8），则数据库会使用固定的1个字节(八位）来存储数据，不足8位的字符串在其后补空字符。
varchar(M)是一种比char更加灵活的数据类型，同样用于表示[字符](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E5%AD%97%E7%AC%A6)数据，但是varchar可以保存可变长度的字符串。其中M代表该数据类型所允许保存的字符串的最大长度，只要长度小于该最大值的字符串都可以被保存在该数据类型中。因此，对于那些难以估计确切长度的[数据对象](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%AF%B9%E8%B1%A1/3227125)来说，使用varchar数据类型更加明智。MySQL4.1以前,varchar数据类型所支持的最大长度255,5.0以上版本支持65535字节长度,utf8编码下最多支持21843个字符(不为空)



### 3.3 数据表编码问题

#### 3.3.1 Incorrect string value

- 问题描述

  - 向emp表插入中文数据时报错, 插入失败,

    > ERROR 1366 (HY000): Incorrect string value: '\xE6\x9D\x8E\xE5\x85\xB4...' for column 'ename' at row 1

- 解决办法

  - [原链接](https://www.cnblogs.com/kaerxifa/p/12957578.html)

  - 数据表编码问题

  - 方法1: 修改表格字符集

    ```mysql
    ALTER TABLE emp CONVERT TO CHARACTER SET utf8mb4;
    ```

    

## 4.开发建议

### 起啥名

- SELECT语句不写 SELECT *语句