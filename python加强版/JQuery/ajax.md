## ajax

### ajax的介绍

ajax是Asynchronous JavaScriptandXML的简写，ajax一个前后台配合的技术，它可以让javascript发送异步的http请求，与后台通信进行数据的获取，ajax最大的优点是实现局部刷新，ajax可以发送http请求，当获取到后台数据的时候更新页面显示数据实现局部刷新，在这里大家只需哪记住，当前端页面想和
后台服务器进行数据交互就可以使用ajax了。这里提示一下大家在htmi页面使用ajax需要在web服务器环境下运行，一般向自己的web服务器发送ajax请求·



### ajax的使用

jquery将它封装成了一个方法Sajax0，我们可以直接用这个方法来执行ajax请求。

#### 示例代码:

```html
<script>
    $.ajax({
    //1.ur1 请求地址
    url:'http://t.weather.sojson.com/api/weather/city/101010100',
	//2.type 请求方式，默认是'GET，常用的还有 POST
	type:'GET',
    //3.dataType 设置返回的数据格式，常用的是 json'格式
	dataType:'JSON'，
    // 4.data 设置发送给服务器的数据，没有参数不需要设置
    //5.success 设置请求成功后的回调函数
    success:function (response) {
    	console.log(response);
	},	
    // 6.error 设置请求失败后的回调函数
    error:function () {
    	alert(“请求失败,请稍后再试!");
    },
    // 7.async 设置是否异步，默认值是'true’，表示异步，一般不用写
	async:true
});
</script>
```

#### ajax方法的参数说明:

1. url 请求地址
2. type请求方式，默认是GET，常用的还有POST
3. dataType 设置返回的数据格式，常用的是json格式
4. data 设置发送给服务器的数据，没有参数不需要设置(注意在回调函数中,传入和传出的是response的服务器返回的数据,并且通过dataType的参数解析)
5. success 设置请求成功后的回调函数
6. error 设置请求失败后的回调函数
7. async 设置是否异步，默认值是'true'，表示异步，一般不用写
8. 同步和异步说明
   1. 同步是一个ajax请求完成另外一个才可以请求，需要等待上一个ajax请求完成，好比线程同步
   2. 异步是多个ajax同时请求，不需要等待其它ajax请求完成，好比线程异步



#### ajax的简写说明

$.ajax按照请求方式可以简写成为\$.post()方式或者\$.get()方式 
