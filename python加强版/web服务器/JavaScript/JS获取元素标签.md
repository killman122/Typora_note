## 使用JS获取元素标签

### 获取标签元素

可以使用__内置对象document__上的__getElementById__的方法来获取页面上设置了id属性的标签元素,获取到的是一个html对象,然后将它赋值给一个变量,比如:

```html
<script type="text/javascript">
    var oDiv = docunment.getElementById('div1');
    alert(oDiv);
</script>
<div id="div1">这是一个div元素</div>
```

#### __说明:__

上面的代码，如果把javascript写在元素的上面，就会出错，因为页面上从上往下加载执行的，javascript去页面上获取元素div1的时候，元素div1还没有加载·

#### 解决方法有两种:

第一种方法:将javascript放到页面最下边

第二种方式:调用 事件

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 如果必须要将代码写在head标签中,则需要等待所有的标签元素加载完毕后才能调用js代码 -->
    <!-- 第二种写法: 设置页面加载完成执行的函数,在执行函数里面获取标签元素 -->
    <script>

        // 第二种写法的使用匿名函数并将获取对象的js方法写在onload方法的内部
        // 页面的标签和数据都加载完成后,会触发onload事件
        // window.onload = function(){
        //     // document是js的一个内置对象dom的全称,就是html中的文档对象
        //     var oP = document.getElementById('p1');
        //     // 如果获取的对象是null(空),表示标签没有成功获取
        //     alert(oP);
        // }  
        
        // 如果不使用匿名函数(使用匿名函数的方式执行js代码只能执行一次,但是使用自己构造的函数执行代码可以执行次数无限)的方式执行相关的js代码,可以自己构造函数
        function fnLoad(){
            var oP = document.getElementById("p1");
            alert(op);
        }
        // 触发onload事件
        window.onload = fnLoad;//在python中的工厂模式中,通过return 函数名 的方式调用函数,和这里有相似之处

    </script>

</head>

<body>
    <p id="p1">我是一个段落标签</p>
</body>
<!-- 注意在使用js和css时,不要将两个对应的标签用错,js使用的是script标签,但是css使用的是style标签 -->
<!-- 在内嵌式的script标签中,如果将script标签写在最前面也就是head标签中,当需要使用jsdom获取标签元素时,会由于未完全加载页面的所有标签,导致使用getElement获取的元素为空 -->
<!-- 第一种写法   需要将执行的js代码写在body标签外,html标签内部以外,避免由于body中的标签未加载完成导致的无法使用js代码获取某个标签 -->
<!-- 这种写法不推荐,等标签初始化完成后再获取 -->
<!-- <script>
    // document是js的一个内置对象dom的全称,就是html中的文档对象
    var oP = document.getElementById('p1')
    // 如果获取的对象是null(空),表示标签没有成功获取
    alert(oP);
</script> -->
</html>

```

