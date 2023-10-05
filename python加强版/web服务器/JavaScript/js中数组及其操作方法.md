## js中数组及其操作方法

### 数组的介绍

__数组就是一组数据的集合,js中,数组中的数据可以是不同数据类型的集合,好比python中的列表__

### 数组的定义

```javascript
//实例化对象方式创建
var aList = new Array(1,2,3);

//字面量
字面量是在计算机中描述事物
字面量:
11000此时的11000就是数字字面量
'黑马程序员'字符串字面量
[]数组字面量    {}对象字面量
字面量方式创建相当于直接创建出的是一个数组
var aList2 = [1,2,3,4,'1234'];
```



### 多维数组

多维数组指的是数组的成员还是数组,把这样的数组称为多维数组.

```javascript
var aList = [[1,2,3],['a','b','c']];
```



### 数组的操作

#### 获取数组的长度

```javascript
var aList = [1,2,3,4];
alert(aList.length); // 弹出4的数组长度
```

#### 根据数组下标取值

```javascript
var aList = [1,2,3,4];
alert(aList[0]);//弹出1
```

#### 从数组最后添加和删除数据

```javascript
var aList = [1,2,3,4];
aList.push(5)
alert(aList);//弹出1,2,3,4,5,因为上面使用push的方式入数组
aList.pop();
alert(aList);//弹出1,2,3,4 因为数组末尾元素pop出数组
```

#### 根据下标添加和删除元素

```javascript
arr.splice(start,num,element1,...elementN);
```

python中具有相似的代码insert() 	列表list.insert(index,值)

参数解析:

1. start: 必须,开始删除的索引
2. num: 可选,删除数组元素的个数
3. elementN: 可选,在start索引位置要插入的新元素

此方法会删除从start索引开始的num个元素,并将elementN参数插入到start索引的位置

==在项目d:vscode中具有相关的所有js代码==

如果指定删除的数组元素个数为num = 0,则表示没有删除数据,可以在之后的参数中添加数据也就是需要添加的数据elementN,将elementN参数插入到start索引的位置

```javascript
var colors = ["red","green","blue"];
colors.splice(0,1);//删除第一项元素
alert(colors);//green,blue

colors.splice(1,0,"yellow","red");//从第一个索引位置插入两项数据
alert(colors);//green,yellow,red,blue	在第一个索引的位置开始,由于第二个参数为空,表示不删除元素,并且在索引位置后添加,第三个参数及其以后的参数

colors.splice(1,1,"pink","purple");//从第一个索引的位置开始删除一个元素,并插入,第三个参数及其以后的参数到,删除元素的索引后
alert(colors);//green,pink,purple,red,blue 
```



#### 追加数据到数组中

```javascript
var colors = ["red","green","blue"];
```

