---
title: 【数据库】  约束
date: 2025-03-25 23:07:30
tags: [数据库,学习]
categories: [学习]
excerpt: "约束（Constraint） 是数据库中用于确保数据完整性和一致性的规则或限制。它们定义了数据表中的数据如何存储、修改和操作，确保数据库中的数据符合预设的规则。"
---

## 约束
> **约束（Constraint）** 是数据库中用于确保数据完整性和一致性的规则或限制。它们定义了数据表中的数据如何存储、修改和操作，确保数据库中的数据符合预设的规则。
### 主键约束 PRIMARY KEY

- PRIMARY KEY又称为主键约束，定义表中构成主键的一列或多列。
- 主键用于唯一标识表中的每条记录，作为主键的字段值不能为NULL且必须唯一，可以是单一字段，也可以是多个字段的组合。
- 每个数据表中最多只能有一个主键约束。

`属性名 数据类型 PRIMARY KEY`

<br>

#### 使用 PRIMARY KEY 关键字设置主键约束

图形化操作界面创建表的方法每个IDE都不同

我们这里主要以SQL语句进行讲解:

当主键只需要一个字段构成时，创建时在后方加上关键字即可

```mysql
CREATE TABLE goods(
	gid int PRIMARY KEY,	# 标识该字段为主键
    gname varchar(30) NOT NULL
    gprice decimal(20,2)
);
```

> 创建表 goods

<br>

当主键由多个字段组合构成时，主键只能在字段定义完成后设置:

```mysql
CREATE TABLE cart(
    gid int ,
    uid int ,
    cnum int,
    PRIMARY KEY (gid,uid)   # 自定义复合主键
);
```

> 创建购物车表car

<br>

#### 复合主键

你可能觉得，主键不是每个表最多一个吗，为啥还能用复合主键？

实际上，主键确实在表里唯一，但是复合主键的意思并不是表里有多个主键，而是表的唯一主键里有多个字段组合而成的**复合主键（Composite Primary Key）**

复合主键实际上是将多个字段联合起来作为一个唯一标识符

以`cart`表为例，设置了两个字段(gid+uid)为主键

这意味着，每一行数据通过 `uid` 和 `gid` 的组合来唯一标识。虽然 `uid` 和 `gid` 可以单独重复，但它们的组合必须是唯一的。

举个例子：

| `uid` | `gid` | `cnum` |
| ----- | ----- | ------ |
| 1001  | 2001  | 5      |
| 1001  | 2002  | 3      |
| 1002  | 2001  | 8      |

在这个表中：

- `uid = 1001` 和 `gid = 2001` 的组合是唯一的。
- 同样，`uid = 1001` 和 `gid = 2002` 也有唯一的组合。
- 不会出现相同的 `uid` 和 `gid` 组合，确保了数据的一致性和完整性。

<br>

###  非空约束 NOT NULL

- NOT NULL约束也称非空约束
- 强制字段的值不能为NULL，它不等同于0或空字符串，也不能跟任何值进行比较。
- NOT NULL只能用作约束使用。

`属性名 数据类型 NOT NULL`

<br>

```mysql
ALTER TABLE goods
    ADD gcode varchar(50) NOT NULL AFTER gid ; 
```

> 在goods表内新加字段 gcode，并设置为非空，放在gid后面

<br>

<br>

### 默认约束 DEFUALT

- DEFAULT约束即默认值约束，用于指定字段的默认值。
- 当向表中添加记录时，若未为字段赋值，数据库系统会自动为将字段的默
- 认值插入。
- 属性名数据类型DEFAULT默认值

`属性名 数据类型 DEFAULT 默认值`

<br>

```mysql
ALTER TABLE cart
    MODIFY  cnum int DEFAULT 1;	# 修改默认值为1
```

> 修改购物车表cart的cnum字段，将默认值设定为1

<br>

### 唯一约束 UNIQUE

- NIQUE约束又称唯一性约束，是指数据表中一列或一组列中只包含唯一值。

`属性名 数据类型 UNIQUE`

<br>

```MYSQL	
ALTER TABLE users
	MODIFY ulogin varchar(50) UNIQUE ;
```

> 修改users表的ulogin添加唯一约束



### 检查约束 CHECK

- CHECK约束是列输入数据值的验证规则，列中输入数据必须满足CHECK约束的条件，否则无法写入数据库。
- MySQL8.0开始支持CHECK约束。

`CONSTRAINT 约束名 CHECK (表达式)`

<br>

```mysql
ALTER TABLE goods
	ADD CONSTRAINT ck_gprice CHECK(gprice >= 0);
```

> 修改goods表gprice字段的检查约束ck_gprice，设置价格>=0

<br>

### 外键约束 FOREIGN KEY

- FOREIGN约束是用于确保表与表之间的数据一致性和完整性
- 它的作用是在一张表中引用另一张表的主键或者唯一键，目的是确保被引用的记录存在，避免不一致或无效的数据输入。

> 也就是说，外键通过链接另一个表的唯一键或者主键，让其实时连接唯一键或者主键的数据，当被链接方(父表)发生改变时，链接方也会跟着改变

<br>

`FOREIGN KEY (外键列名) REFERENCES 父表名(父表主键列名)`

<br>

假设我们有两个表，一个是 `users` 表，另一个是 `orders` 表，`orders` 表中的 `user_id` 字段是 `users` 表的外键，指向 `users` 表的主键 `id`：

```mysql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    order_date DATE,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```
![Static Badge](https://img.shields.io/badge/状态-待更新-brightgreen?style=flat-square)