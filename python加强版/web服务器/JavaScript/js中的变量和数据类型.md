## 变量和数据类型

### 定义变量

JavaScript 是一种弱类型语言，也就是说不需要指定变量的类型，JavaScript的变量类型由它的值来决定，定义变量需要用关键字“var”，一条JavaScript语句应该以“;”结尾

#### 定义变量的语法格式:

var 变量名=值;

```javascript
var inum =33;
var sTr = "asd";

//同时定义多个变量可以使用","隔开,公用(共用)一个"var"关键字
var inum=45,sTr="we",Scount='99';
```



### JavaScript注释

JavaScript的注释分为单行注释(//注释内容)和多行注释(/*多行注释*/)

```javascript
<script type="text/javascript">
//单行注释
//var num =11;
/*
	多行注释
	1....
	2...
	...
*/
```

==拓展==在python中定义多个变量:

```
不是直接使用类似于元组的方式传入变量的数据值
a,b = 1,2
实质上还是以元组的方式传入变量,类似于=>(a,b) = (1,2)
但是也有不使用元组的方式在一行中连续定义多个变量,使用a=1;b=2
在python和js中;似乎表示的只是语句的结束
```



### 数据类型

js中有六种数据类型，包括五种基本数据类型和一种复杂数据类型(object)。
5种基本数据类型:

1. number 数字类型
2. string 字符串类型
3. boolean 布尔类型 true 或 false
4. undefined undefined类型，变量声明未初始化，它的值就是undefined
5. null null类型，表示空对象，如果定义的变量将来准备保存对象，可以将变量初始化为null在页面上获取不到对象，返回的值就是null
   在python中的空值就是none

由于js历史原因,设计之前没有null类型,null值归属于object类型,后续语言迭代后也没有进行修改
对于大家来说null值属于null类型

1种复合类型:

1. object 后面学习的JavaScript对象属于复合类型
2. 定义一个空对象:var oData = null; //空对象在这里使用null,undefined是未定义和对象无关

```javascript
//定义javascript对象类型
var oPerson={
    name:"王五",
    age:20
}
```



### 变量的命名规范

1. 区分大小写
2. 第一个字符必须是字母,下划线,美元符
3. 其他字符可以是字母,下划线,美元符或数字



### 匈牙利命名风格

对象o Object 比如:oDiv
数组a Array 比如:altems
字符串s String 比如:sUserName
整数i Integer 比如:iltemCount
布尔值b Boolean 比如:blsComplete
浮点数f Float 比如:fPrice
函数fn Function 比如 :fnHandler

使用typeof()查看数据或者是对象的数据类型