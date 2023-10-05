## jQuery的用法

### jQuery的引入

```html
<script src="js/jquery-12.2xxx.min.js"></script>
```

### jQuery的入口函数

我们知道使用is获取标签元素，需要页面加载完成以后再获取，我们通过给onload事件属性设置了一个函数来获取标签元素，而jquery提供了__ready函数__来解决这个问题，保证获取标签元素没有问题，__它的速度比原生的 window.onload 更快。__

__入口函数示例代码:__

```html
<script src="js/jquery-1.12.4.min.js"></script>
<script>
    # 等待所有标签初始化完成,所有的资源都可以在网页中显示后,调用windos.onload()方法
    window.onload = function(){
        var oDiv = document.getElementById("div01")<!-- 通过标签元素的id值获取标签元素对象并将标签元素对象返回给js-->
        alert("原生就是获取的div"+oDiv);<!-- 可以使用`${变量的方式直接在js代码中使用变量或者对象}` -->
    };
    # 使用jQuery当该标签初始化完成后,可以调用ready方法执行需要执行的js,所以使用ready的方式一定比windo.onload()的方式执行的效率更高更快
    $(document).ready(function(){
        var $div = $('#div01');
        alert('jQuery获取的div:'+$div);
    });
</script>
<div id="div01">这是一个div标签</div>
```

