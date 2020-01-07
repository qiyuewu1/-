# MySQL

## 基础语句

- `show TABLES; -- 查看数据库中所有表`
- `desc table_name --查看表结构`
- `show databases; --查看所有数据库`
- `use database_name; --使用该数据库`

## 曾经犯下的错

### 1.时区设置

- 高版本mysql连接时需要有时区参数
- **正确配置：**spring.datasource.url=jdbc:mysql://localhost:3306/demo**?characterEncoding**=utf8**&useSSL**=true**&serverTimezone**=Asia/Shanghai 
  - 否则报错：The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more than **one time zone**. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you wan

## 一、DDL

### 1.创建数据库

```sql
create database demo [character set utf8];
```

### 2.修改数据库

```sql
alter database demo character set utf8;
```

### 3.删除数据库

```sql
drop database demo;
```

### 4.表创建-create table

#### 1）第一种建表

```sql
create table table_name(
	id int(12) primary key auto_increment,-- auto_increment 表示自增
    name varchar(20) not null,
    column_name1 varchar(24) unique,
    column_name2 varchar(20)
);
```

#### 2）第二种建表，联合主键

``` sql
create table table_name(
	id int(12) ,
    name varchar(20),
    primary key(id,name)
);
```

**-- 后期增加**
`alter table table_name add primary key(column_name);`
**-- 后期删除（只能全部删除）**
`alter table table_name drop primary key;`

- **注！！！**：第二种建表方式才能后期增删主键约束
- 第一种报错：Multiple primary key defined

### 5.表修改-alter table

#### 1)  唯一约束 unique

```sql
-- 后期增加唯一约束
alter table table_name add unique(column1[,column2....])
```

- **注！！！**当列为多个时，唯一的约束效果 与联合主键相似，是**联合后唯一约束**

``` sql
-- 后期删除唯一约束
drop index index_name on table_name;
```

- **注！！！**当为联合唯一约束时，index_name相当于添加时写在第一位的列名**column1**

#### 2) 非空约束、以及字段类型(长度)  modify

```  SQL 
-- 修改字段类型Type与长度都用这个
-- 后期增加非空约束
alter table table_name modify Column1 Type not null;
-- 后期删除非空约束
alter table table_name modify Column1 Type;
```

- **注：**
  - 当修改字段长度时比某个已存在值短，修改失败！
  - 当表中数据该列存在**Null**值的时候，修改失败！

## 二、SQL

### 1.exists用法

```sql
SELECT c.CustomerId,CompanyName FROM Customers c
WHERE EXISTS(
SELECT 'x' FROM Orders o WHERE o.CustomerID=c.CustomerID) 
```

- 判断上层表的某字段的值 是否在当前层的表中存在
- 存在返回true 否则返回false
- 与in 条件类似，适用外表小，内表大的情况

### 2.时间、字符串转换

- 时间	转为	字符串

  ```sql
  date_format(reg_time,'%Y-%m-%d') reg_time  -- 输出为 2020-01-06
  ```

- 字符串 转为   日期

  ```sql
  str_to_date(#{regTime},'%Y-%m-%d')
  ```

