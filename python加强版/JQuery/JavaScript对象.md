## Javascript对象

### JavaScript对象的介绍

JavaScript 中的所有事物都是对象: 字符串、数值、数组、函数等都可以认为是对象，此外，JavaScript允许自定义对象，对象可以拥有属性和方法。

### JavaScript创建对象操作

创建自定义javascript对象有两种方式:

- 通过顶级Object类型来实例化一个对象
- 通过对象字面量创建一个对象

#### Object类创建对象的示例代码:

```js
<script>
var person = new Object();
// 添加属性
person.name ="tom';
person.age '25";
// 添加方法:
person.sayName = function(){alert(this.name)};
// 调用属性和方法
alert(person.age);
person.sayName();
</script>
```

