## 表结构操作的SQL语句

### 创建一个新的数据库需要设置数据库的字符集

```sql
CREATE DATABASE bookmanage_9_19 CHARACTER SET utf8; // 这里是在编写django项目时使用的数据库创建代码
// 还有创建数据库的设计字符集的格式使用=设置字符集
create database xxx数据库名 charset = utf8;
```

### 显示所有的数据库

```sql
show databases;
```

### 使用指定的数据库

```sql
use xxx数据库名;
```

###查看当前数据库中所有表

```sql
show tables;
```

### 查看数据库中某个表的结构(设计表的数据类型等)

```sql
desc 表名(或者使用Meta更改后的表别名);  //查看数据库中某个表的详细键,DESC table_name 可以查看数据库中的 table_name 表的列名称、数据类型、是否可以为 NULL
```

### 创建表

```sql
create table students(
    id int unsigned primary key auto_increment not null, // 设置数据的id为整型并且无符号并且作为主键自增
    name varchar(2) not null,
    age tinyint unsigned default 0, //小整数类型tinyint,并且是无符号unsigned
    height decimal(5,2),	// 表示数据的总共长度为5位,但是小数点占位2位,在没有指定not null的情况下,允许数据库中的列为空
    gender enum("男","女","人妖","保密") //使用枚举类型的数据保存性别,但是使用枚举类型后,能够填写的数据的值,只能从枚举的数据类型中填写
);		// 在写完数据库sql的所有代码后一定要使用;分号用作结束的符号,否则无法判断是否结束
```

#### 说明:

```sql
create table 表名(
字段名称 数据类型 可选的约束条件，
column1 datatype contrai,
...
);
```

###修改表-添加字段(注意这里不是说向已经创建好的空表中插入数据,而是补充设置新的表结构)

```sql
alter table 表名 add 列名 类型 约束;
例:
alter table students add birthday datetime;
```

### 修改表-修改字段类型和约束

```sql
alter table 表名 modify 列名 类型 约束;
例:
alter table students modify birthday data not null;
```

__说明__:

- modify : 只能修改字段类型或者约束,但是不能修改字段名

### 修改表-修改字段名和字段类型和约束

```sql
alter table 表名 change 原名 新名 类型及约束;
例:
alter table students change birthday birth datetime not null;
```

__说明:__

- change: 既能对字段重命名又能修改字段类型还能修改约束

### 修改表-删除字段

```sql
 alter table 表名 drop 列名;
 例:alter table students drop birthday;
```

### 查看创建SQL语句

```sql
show create table 表名;
例:
show create table students;

//显示出来额效果如下: 
students | CREATE TABLE `students` (
  `id` int unsigned NOT NULL AUTO_INCREMENT,
  `name` varchar(2) NOT NULL,
  `age` tinyint DEFAULT '0',
  `gender` enum('男','女','双性人','保密') DEFAULT NULL,
  `scroes` int NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3
```

### 查看创数据库的SQL语句

```sql
show create database 数据库名;
例:
show create database 黑马高级数据库;
```

### 删除数据库

```sql
drop database xxx数据库名;
drop database 黑马高级数据库;
```

### 删除数据库中的表

```sql
drop table 表名;
drop table students;
```



## 表数据操作的SQL语句

###查询数据

```sql
查询所有列
select * from 表名;
例:
select * from students;-- 2，查询指定列select 列1,列2,...from 表名;
例:
select id,name from students;
```

### 添加数据

```sql
-- 1、全列插入:值的顺序与表结构字段的顺序完全一一对应
// 在没有指定列名的情况下,表中的列字段的所有数据都要插入
insert into 表名 values (...)

例: 如果在设计数据库时使用了default 设置默认的字段,那么在向数据库的表中插入数据时能够对于默认字段使用default代替要插入的真实数据如下所示:
但是如果是主键列则可以使用0/default/null来表示插入的默认数据
insert into students values(0,'xx",default, default,"男'); 
-- 2.部分列插入:值的顺序与给出的列顺序对应insert into 表名(列1,...) values(值1,...)例:
insert into students(name，age) values('王二小'，15);
-- 3.全列多行插入
insert into 表名 values(...),(...)...;
例:
insert into students values(0,"张飞'，55，1.75,"男'),(0,'关羽'，58，1.85,"男');
-- 4.部分列多行插入
insert into 表名(列1,...) values(值1,...),(值1,...)...;
例:
insert into students(name， height) values("刘备'，1.75),("曹操'，1.6);
                                          
// 在部分列插入和部分列多行插入的区别中,最大的区别就是多行插入使用values插入多个()插入多个列的列名中
```

__说明:__

- 主键列是自动增长，但是在全列插入时需要占位，通常使用空值(0或者null或者default)
- 在全列插入时，如果字段列有默认值可以使用 default 来占位，插入后的数据就是之前设置的默认
  值

### 修改数据

```sql
update 表名 set 列1=值1,列2=值2...，where 条件
例:
update students set age = 18, gender ='女' where id = 6;
```

### 删除数据

```sql
delete from 表名 where 条件
例:
delete from students where id=5;
```

__问题:__
上面的操作称之为物理删除，一旦删除就不容易恢复，我们可以使用逻辑删除的方式来解决这个问题。

```sql
--添加删除表示字段，0表示未删除 1表示删除
alter table students add isdelete bit/tinyint default 0;
--逻辑删除数据
update students set isdelete = 1 where id = 8;
```

__说明:__
逻辑删除，本质就是修改操作

### 小结

- 登录数据库: mysql-urootp
- 退出数据库:quit 或者exit 或者 ctr + d
- 创建数据库: create database 数据库名 charset=utf8;
- 使用数据库:use 数据库名;
- 删除数据库: drop database 数据库名;
- 创建表: create table 表名(字段名 字段类型 约束,...);
- 修改表-添加字段: alter table 表名 add 字段名 字段类型 约束
- 修改表-修改字段类型:alter table 表名 modify 字段名 字段类型 约束 
- 修改表-修改字段名和字段类型: alter table 表名 change 原字段名 新字段名 字段类型 约束
- 修改表-删除字段: alter table 表名 drop 字段名;
- 删除表: drop table 表名;
- 查询数据: select*from 表名; 或者 select 列1,列2... from 表名;
- 插入数据: insert into 表名 values (..) 或者 insert into 表名(列1,..) values(值1,...)
- 修改数据: update 表名 set 列1=值1,列2=值2...where 条件
- 删除数据: delete from 表名 where 条件