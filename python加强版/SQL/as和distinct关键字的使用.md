## as和distinct关键字

### as关键字

在使用SQL语句显示结果的时候，往往在屏幕显示的字段名并不具备良好的可读性，此时可以使用 as 给字段起一个别名。

1. 使用as给字段起别名

   ```sql
   select id as 序号，name as 名字，gender as 性别 from students;
   ```

   ​	

2. 可以通过as给表起别名

   ```sql
   -- 如果是单表查询可以省略表名,这里指的是查询的列中的表名.字段名(属性名)
   select id,name,gender from students;
   -- 表名.字段名(多表查询)
   select students.id,students.name,students.gender from students;
   -- 可以通过as给表起别名(与python中相同)
   select s.id,s.name,s.gender from students as s;
   ```

   __说明:__

   - 在这里给表起别名看起来并没有什么意义,然而并不是这样的，我们在后期学习 自连接 的时候必须要对表起别名

### distinct关键字

distinct可以去除重复数据行

```sql
select distinct 列1,... from 表名;
例:查询班级中学生的性别
select name，gender from students;
看到了很多重复数据 想要对其中重复数据行进行去重操作可以使用distinct
select distinct name, gender from students;
```



### 小结

- as 关键字可以给表中字段 或者 表名 起别名
- distinct 关键字可以去除重复数据行