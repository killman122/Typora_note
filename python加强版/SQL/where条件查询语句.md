## where条件查询

### where条件查询的介绍

使用where条件查询可以对表中的数据进行筛选，条件成立的记录会出现在结果集中。

#### where语句支持的运算符:

1. 比较运算符
2. 逻辑运算符
3. 模糊查询
4. 范围查询
5. 空判断

#### where条件查询语法格式如下:

```sql
select * from 表名 where 条件;
例:
select * from students where id=1;
```



### 比较运算符查询

1. 等于:=
2. 大于:>
3. 大于等于:>=
4. 小于:<
5. 小于等于:<=
6. 不等于:!= 或 <>

#### 例1:查询编号大于3的学生:

```sql
select * from students where id > 3;
```

#### 例2:查询编号不大于4的学生:

```sql
select * from students where id <= 4;
```

#### 例3:查询姓名不是“黄蓉”的学生:

```sql
select * from students where name !="黄蓉";
select * from students where name <>"黄蓉";
```

#### 例4:查询没被删除的学生:

```sql
select * from students where is_delte=0;
```



### 逻辑运算符查询

1. and
2. or
3. not

#### 例1:查询编号大于3的女同学:

```sql
select * from students where id > 3 and gender-0;
```

#### 例2:查询编号小于4或没被删除的学生:

```sql
select * from students where id < 4 or is_delete=0;
```

#### 例3:查询年龄不在10岁到15岁之间的学生:

```sql
select * from students where not (age >= 1 and age <= 15);
```

__说明:__

- 多个条件判断想要作为一个整体，可以结合"()"

  ```sql
  // 例:查询年龄在10岁到15岁之间的学生
  select * from students where age>=10 and age<=15;
  ```



### 模糊查询

1. like是模糊查询关键字
2. %表示任意多个任意字符
3. _表示一个任意字符

#### 例1:查询姓黄的学生:(由于不知道完整字段,所以需要模糊查询,黄为首字符并且未知除姓外的任意字符)

```sql
select * from students where name like '黄%';
```

#### 例2:查询姓黄并且“名”是一个字的学生:

```sql
select * from students where name like '黄_';
```

#### 例3:查询姓黄或叫靖的学生:

```sql
select * from students where name like '黄%' or name like %靖;
```



### 范围查询

1. between ..and..表示在一个连续的范围内查询(比如说1-9的范围)
2. in 表示在一个非连续的范围内查询,并将可选项写在一个()包裹的整体内部

#### 例1:查询编号为3至8的学生:

```sql
select * from students where id between 3 and 8;
```

#### 例2:查询编号不是3至8的男生:

```sql
select * from students where not (id between 3 and 8) and gender='男';
```

#### 例3:查询编号是3,5,7的学生:

```sql
select * from students where id in(3,5,7); 
```

#### 例4:查询编号不是3,5,7的学生:

```sql
select * from students where id not in(3,5,7));
```



### 空判断查询

1. 判断为空使用:is null (无法通过where直接查询相关的条件,select * from students where height=null;select * from students where height=NULL;)
2. 判断非空使用:is not null

传统添加表中列的字段的方法:`alter table 表名 add 列名 类型 约束;`

###### 添加一列身高,身高的总共长度占三位,小数点占据两位,并且允许升高的取值为空,不需要编写not null(在数据库的表中):`alert table students add height decimal(3,2)`

###### 更新表中身高的全部信息,让所有的表中学生的身高都设置为1.85m:`update students set height = 1.85;`

#### 例1:查询没有填写身高的学生:

```sql
select * from students where height is null;
```

#### 例2:查询填写了身高的学生信息:

```sql
select * from students where height is not null;
```

__注意:__

1. 不能使用 where height = null 判断为空
2. 不能使用 where height!= null 判断非空
3. null 不等于 '' 空字符串



### 小结

- 常见的比较运算符有 >,<,>=,<=,!=
- 逻辑运算符and表示多个条件同时成立则为真,or表示多个条件有一个成立则为真,not表示对条件取反
- like和%结合使用表示任意多个任意字符，like和_结合使用表示一个任意字符
- between-and限制连续性范围 in限制非连续性范围
- 判断为空使用:is null
- 判断非空使用:is not null