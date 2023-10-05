import redis
r = redis.StrictRedis('8.130.32.139',6379,0,password='wjr123')
*# r.setbit()* *设置**bit**格式的数据
**#* *使用普通的方法设置**redis**中的数据
*r.set('foo','bar')
print(r.get('foo'),type(r.get('foo'))) *#* *二进制**byte**数据
**
*'''
redis常见通用命令
KEYS:查看符合模板的所有key
查看命令的具体用法:help[commmand]
help keys
查看所有的key使用KEYS *
查看以某个字符开头,比如说这里以a开头的key
KEYS a*

DEL:删除一个指定的key
DEL key [key...]
DEL name
DEL name age k1 k2 k3

EXISTS:判断key是否存在
EXISTS age

EXPIRE:给一个key设置有效期,有效期到期时该key会自动删除
TTL:查看一个key的剩余有效期
EXPIRE age 20   设置age key的有效期为20秒
当一个key的ttl查看的有效期为-2时证明这个key已经被移除

在未设置EXPIRE存活时间时,例如直接使用set name Jack的方式设置key value
查看ttl key的剩余有效期为-1  表示这个key为永久有效
'''

"""
String 类型的常见命令和基本用法
String类型,也就是字符串类型,redis中对简单的存储类型
SET:添加或者修改已经存在的一个String类型的键值对
GET:根据key获取String类型的value
MSET:批量添加多个String类型的键值对
MGET:根据多个key获取多个String类型的value
INCR:让一个整型的key自增1
INCRBY:让一个整型的key自增并指定步长,例如:incrby num 2 让num的值自增2 value值自增步长的长度 
INCRBYFLOAT:让一个浮点类型的数字自增并指定步长
SETNX:添加一个String类型的键值对,前提是这个key不存在,否则不执行
SETEX:添加一个String类型的键值对,并且指定有效期

SETNX等同于set name wangwu nx
SETEX等同于set name jack ex 10 设置key-value的有效期为10s

"""

*# redis**中的层级结构
*'''
Redis中的key允许有多个单词形成的层级结构,多个单词之间使用':'隔开,格式如下:
项目名:业务名:类型:id

例如项目名叫做heima,有user和product两种不同类型的数据,可以这样定义key
user相关的key:heima:user:1
product相关的key:heima:product:1

如果value是一个Java对象,例如一个User对象,则可以将对象序列化为json字符串后存储
key             value
heima:user:1    {"id":1,"name":"jack","age":21}
heima:product:1 {"id":1,"name":"消灭"}
使用:的key可以在redis中形成层级结构
'''

*# redis**中的**Hash**类型
*'''
key-field-value 键-字段-值  
一个键可以对应多个字段和值,但是在一个hash表中,字段名不能重复

Hash类型,也叫做散列,其中value是一个无序字典,类似于python中的字典,类似于Java中的HashMap结构
String结构将对象序列化转换为JSON字符串后存储,当需要修改某个字段时很不方便
Hash结构可以将对象中的每个字段独立存储,可以针对单个字段做CRUD:
也就是说将原本的json格式的value再次转换为field-value的对应形式
其中field相当于json中的key,value相当于是json中的value

Hash中的常见命令有:
HSET key field value:添加或者修改hash类型的key的field的值
HGET key field:获取一个hash类型的key的field的值
HMSET:批量添加多个hash类型key的field的值
HGET:批量获取多个hash类型的key的field的值
HGETALL:获取一个hash类型的key中的所有的field和value
HKEYS:获取一个hash类型的key中的所有的field
HVALS:获取一个hash类型的key中的所有的value
HINCRBY:让一个hash类型的key的字段值自增并指定步长
HSETNX:添加一个hash类型key的field值,前提是这个field不存在,否则不执行(类似于SETNX在string类型的变量中)


在使用hset命令时需要大写命令词
例如:HSET heima:user:3 name luck
其中name指的时field,name后的参数表示value值,key值为heima:user:3

使用hget命令获取其中的key对应的value值
HGET heima:user:3 name
其中HGET 是主要命令  heima:user:3 是key值
name是field值,因为在存储时,不是原来的json格式存储数据,而是按照field-value的方式

使用hmset命令
HMSET heima:user:4 name lilei age 20 sex man

使用hmget命令
HMGET heima:user:4 name age sex
'''

'''
在python中的常用redis命令
1.设置
    a.设置键值
    set key value
    b.设置键值及其过期时间,以秒为单位
    setex key second value
    c.设置多个键值
    mset key value [key value .....]
2.获取
    a.根据键获取值,如果键不存在则返回None(null,0,nil)
    get key
    b.根据多个键获取多个值
    mget key [key ....]
3.运算
    要求:值是字符串类型的数字
    a.将key对应的值加1
    incr key
    b.将key对应的值减1
    decr key 
    c.将key对应的值加整数
    incrby key intnum
    d.将key对应的值减整数
    decrby key intnum
4.其他
    a.追加值
    append key value
    b.获取值长度
    strlen key 
    
1.查找键,参数支持正则
    keys pattern
2.判断键是否存在,如果存在返回1,不存在返回0
    exists key
3.查看键对应的value的类型
    type key
4.删除键及其对应的类型
    del key [key...]
5.设置过期时间,以秒为单位
    expire key seconds
6.查看有效时间,以秒为单位
    ttl key

三.hash
概述:hash用于存储对象
{
    name:'tom',
    age:age
}  
1.设置
    a.设置单个值
    hset key field value
    b.设置多个值
    hmset key field value [field value] 
2.获取
    a.获取一个属性的值
    hget key field
    b.获取多个属性的值
    hmget key field [field]
    c.获取所有的属性和值
    hgetall key
    d.获取所有属性
    hkeys key
    e.获取所有值
    hvals key
    f.返回包含数据的个数
    hlen key
3.其他
    a.判断属性是否存在,存在返回1,不存在返回0
    hexists key field
    b.删除属性和值
    hdel key field [field...]
    c.返回值的字符串长度
    hstrlen key field    
   
四.list
概述:列表的元素类型为string,按照插入的顺序排序,在列表头部或者是尾部添加元素
1.设置
    a.在头部插入
    lpush key value [value...] 
    b.在尾部插入
    rpush key value [value...]
    c.在一个元素的前|后插入新元素
    linsert key before|after pivot value
    
'''

"""
Redis快速入门
redis-cli
redis默认有16个数据库,编号为0-15,默认情况下访问第0号数据库
select 数据库编号    选择指定数据库
select 15 访问15号数据库

dbsize     查看当前数据库的键值对数量
flushdb     清除当前数据库中的所有数据
flushall    清除所有的数据库
save    将数据保存到磁盘
bgsave  将数据异步保存到磁盘
lastsave    获取最后一次保存的unix时间

keys 格式     查看指定格式的key,*为通配符    key *   key k
exsits key1 [key2...] 查看是否存在一个至多个指定的key     exsits name sex
type key    按照key查看value的数据类型
del key1 [key2...]  按照key删除一个至多个键值对
rename key1 key2 重命名key1,如果key2已经存在,key2的值将被覆盖
renamenx key1 key2  key2不存在时重命名key1
move key 数据库编号   按照key将一个键值移动到指定数据库
copy key1 key2  将key1的值拷贝给key2
set key value   添加/修改一个键值对
get key     按照key获取value
mset key1 value1 [key2 value2]  添加修改一至多个键值对
mget key1 [key2...]     按照key获取一个或者多个value值
append key value    按照原有value后追加内容value
strlen  key     查看字符串的长度
getrange key startundex endindex    获取范围[startindex,endindex]的子串 0,-1的索引和python相同

set key value nx    仅当key不存在时,添加一个键值对
setnx key value

set key value xx 仅当key已经存在时,修改一个键值对

set key value get   修改一个键值对并返回原值,原址不存在则
getset key value    

msetnx key1 value1 [key2 value2]    批量版sernx

incr key 按照key创建值为1的value,或者使value增长1
incrby key 数值   按照key使得value增长给定数值
decr key    按照key使得value减小1
decrby key 数值   按照key使得value值减小给定的数值

expire key 秒数   设置一个生存时间
ttl key     查看生存时间的剩余秒数
pexpire key 毫秒数     设置生存时间毫秒版
pttl key
persist key     持久化存储取消生存时间

hset key field1 value1 [field2 value2...]   添加修改一个键至多个字段和值
hget key field      按照key和field获取一对value
hmget key field [field2]    按照key和field获取一至多对value
hgetall key 按照key获取field获取全部的field-value值
hdel key field1 [field2...]     删除一至多对field-value
hsetnx key field value 仅在field不存在时添加一对field-value
hkeys key   查看一个散列表中的所有的field
hvals key   查看一个散列表中的所有的value
hlen key    统计一个散列表中多少对field-value
hexists key field   查看一个field是否存在

hstrlen key field   按照key和field查看value的长度

hincrby key field 整数值   按照key和field使得value增长给定整数值
hincrbyfloat key field 小数值      按照key和field使得value增长给定小数值

列表list
key-value0-value1...,键-有序的值队列
key1 value0 value1 ...
key2 value0 value1 ...

rpush l1 1 2 3 4 5 从右侧依次插入列表中的数据,其中5是第一个插入的数据
lrange l1 0 -1   从左
lpush l1 6 7 8 9 0 从左侧依次插入列表中的数据,其中6先入在最下边

rpop key [数量] 从列表右侧弹出指定数量的值   rpop l1 3 弹出三个
lpop key [数量] 从列表左侧弹出指定数量的值

rpushx key value0 [value1 ...] 仅当列表存在时,从列表的右侧推入一个至多个值
lpushx key [...value1] value0   仅当列表存在时,从列表左侧推入一个或者多个值

lset key *index value   修改指定位置的值
linsert key before/after 定位vlaue vlaue  在定位value前/后插入一个值
lindex key *index       按照索引查看值
lrange key *startindex *endindex    查看给定范围的值
llen key 查看队列的长度
lrem key 数量 value   删除指定值   数量为正代表从左侧开始删除,数量为负代表从右侧开始删除     删除列表中的值     数量count=0删除所有
ltrim key *startindex *endindex 将列表修剪到给定范围内

集合set
key-stringx,stringy...,键-无序的不重复的成员
key1 stringx stringy...

sadd key stringx [stringy....]   添加一个或多个成员   sadd s1 1 2 3 4
srem key stringx [stringy....]   删除一个或多个成员
scard key       返回成员数量
sismember key string        查看是否存在指定成员
smismember key stringx [stringy...]     批量查看是否存在指定成员
smembers key    查看你集合中的所有成员



有序集合(可以通过时间戳对商品的浏览记录等进行记录)
元素类型为String类型,元素具有唯一性不重复,每个元素会关联一个double类型的score,表示权重,仅通过权重将元素从小到大排列

增加 zadd key score1 member1 score2 member2 score2
zrange key start stop	按照顺序排列集合中的元素
删除 zrem key stringx	