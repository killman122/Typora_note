## 函数定义和调用

### 函数定义

函数就是可以重复使用的代码块,使用关键字function定义函数.

```html
<script type="text/javascript">
    //函数定义
    function fnAlert(){
        alert("hello");
    }
</script>
```



### 函数调用

函数调用就是函数名加小括号,比如:函数名(参数[参数可选])

```html
<script type="text/script">
	//函数定义
	function fnAlert(){
		alert('hello');
	}
	//函数调用
	fnAlert()
</script>
```



### 定义有参数有返回值的函数

定义函数时,函数如果有参数,参数放到小括号里面,函数如果有返回值,返回值通过`return`关键字来返回

```html
<script type="text/javascript">
function fnAdd(iNum1,iNum2){
    var iRs = iNum1;
    return iRs;
    alert("here!");
}

var iCount = fnAdd(3,4);
alert(iCount);//弹出
</script> 
```

