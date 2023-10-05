## 定时器的使用

### 定时器的介绍

定时器就是在一段特定的时间后执行某段程序的代码

### 定时器的使用

js定时器有两种方式创建

1. setTimeout(func[,delay,param1,param2...]):以指定的时间间隔(以毫秒计算)调用一次函数的定时器
2. setInterval(func[,delay,param1,parma2,...]):以指定的时间间隔(以毫秒记)重复调用一个函数的定时器

#### setTimeout函数的参数说明:

- 第一个参数 func，表示定时器要执行的函数名
- 第二个参数 delay,表示时间间隔，默认是0，单位是毫秒
- 第三个参数 param1,表示定时器执行函数的第一个参数，一次类推传入多个执行函数对应的参数。

## 定时器

### 1. setTimeout()

1.1 作用：延迟定时器，只会循环一次。
 1.2
 普通函数用法：

```javascript
var timer1=setTimeout(function(){  
   console.log('我是延迟定时器')  
},1000)
```

箭头函数用法：

```javascript
var timer1=setTimeout(()=>{  
  console.log('我是延迟定时器')  
},1000)
```

1.3 清除定时器(定时器是直接执行的，为了优化性能在使用完每一帧定时器都要清除掉，因此要命名并方便后续清除)：
 `clearTimeout(timer)`

### 2.setInterval()

1.1 作用：循环定时器，循环多次
 1.2
 普通函数用法：

```javascript
var timer2=setInterval(function(){
 console.log('我是循环定时器')
},1000)
```

箭头函数用法：

```javascript
var timer2=setInterval(()=>{
 console.log('我是循环定时器')
},1000)
```

2.3 清除定时器：
 `clearInterval(time2)`

### 3.关于定时器的参数

定时器可以接收多个参数：
 第一个参数：执行的函数，不可省略。
 第二个参数：定时器所执行的毫秒数，可省略。
 第三个参数及之后的参数：都将是第一个参数函数执行的实参

## 定时器的箭头函数指向

1.1 箭头函数是ES6提出函数语法糖，可以简化普通函数的写法，并且与普通函数的区别为：**箭头函数**中的this指向是**固定不变的**，一直指向的是定义函数的环境。
 1.2 没有特殊情况时，setInterval和setTimeout的回调函数中this的指向都是window，因此箭头函数通常可伴随着定时器一起使用。