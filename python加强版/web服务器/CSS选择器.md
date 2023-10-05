## CSS选择器

### css选择器的定义

css选择器是用来选择标签的,选出来以后给标签加样式.

### css选择器的种类

1. 标签选择器
2. 类选择器
3. 层级(后代选择器)
4. id选择器
5. 组选择器
6. 伪类选择器



### 标签选择器

根据标签来选择标签,以标签开头,此种选择器影响范围大,一般用来做一些通用设置

__示例代码:__

```html
<style type="text/css">
	p{
		color:red;
	}
</style>

<div>hello</div>
<p>hello</p>
```



#### 类选择器

更具类名选择标签,以`.`开头,一个类选择器可应用于多个标签上,一个标签上也可以使用多个类选择器,多个类选择器需要使用空格分割,应用灵活,可复用,是css中应用最多的一种选择器

__示例代码:__

```html
<style type="text/css">
	.blue{color:blue}
	.big{font-size:20px}
	.box{width:100px; height:100px;background:gold}
</style>

<div class="blue">这是一个div</div>
<h3 class="blue big box">这是一个标题标签</h3>
<p class="blue box">这是一个段落标签</p>
```



#### 层级选择器

根据层级关系选择后代标签，以选择器1 选择器2开头，主要应用在标签嵌套的结构中，减少命名·

__示例代码:__

```html
<style type="text/css">
    div p{
        color:red;
    }
    .con{width:330px;height:80px;background:green}
    .con span{color:red}
    .con .pink{color:pink}
    .con .gold{color:gold}
</style>
<div>
    <p>hello</p>
</div>
```



### id选择器

根据id选择标签，以#开头元素的id名称不能重复，所以id选择器只能对应于页面上一个元素，不能复用，id名一般给程序使用，所以不推荐使用id作为选择器。

__示例代码:__

```html
<style type="text/css">
    #box{color:red}
</style>
<p id="box">这是一个段落标签</p>	<!-- 对应以上一条样式,其他元素不允许应用此样式-->
<p>这是第二个段落标签</p> <!--无法应用以上的样式,每个标签只能有一个id名-->
```

__注意点: 虽然给其他标签设置id="box"也可以设置样式,但是不推荐这样做,因为id是唯一的,以后js通过id只能获取一个唯一的标签对象__



#### 组选择器

根据组合的选择器选择不同的标签,以`,`分割开,如果有公共的样式设置,可以使用组选择器

#### 示例代码:

```html
<style type="text/css">
    .box1,.box2,.box3{width:100px;}
    .box1{background:red}
    .box2{background:pink}
    .box3{background:gold}
</style>
<div class="box1">这是第一个div</div>
<div class="box2">这是第二个div</div>
<div class="box3">这是第三个div</div>
```



#### 伪类选择器

用于向选择器中添加特殊的效果,以`:`分隔开,当用户和网站交互时改变效果可以使用伪类选择器

__示例代码:__

```html
<style type="text/css">
    .box1{width:400px;height:100px;background:gold}
    .box1:hover{width:300px}
    /*当实现鼠标移动到指定标签时,将调用伪类选择器中的css设置*/
</style>
<div class="box1">这是第一个div</div>
```





__注意在a<a>标签的herf属性中设置(#+锚点名称)可以当作锚点使用,单独的一个a标签,在herf属性中直接填写#相当于空的跳转标签,可以直接回到页面的顶部__

_href=”URL”的作用_

1、URL为绝对URL

```
 此时指向另一个站点，比如href="http://write.blog.csdn.NET",那么点击时就会直接跳转到这个链接的页面。
```

2、URL为相对URL

```
 此时指向站点内的某个文件，比如href="/test.doc"，那么点击时就会直接下载文件。
```

3、锚 URL

```
   此时指向页面中的锚，比如href="#top"，那么点击时就会到当前页面中id="top"的这个锚点，实现当前页面的所谓跳转。用的最多就是在可滚动页面中，添加菜单，可以直接回到页面中的某个部分的内容。
```
