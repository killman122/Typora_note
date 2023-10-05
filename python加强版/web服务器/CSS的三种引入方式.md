## css 的三种引入方式

#### css的三种引入方式

1. 行内式
2. 内嵌式(内部样式)
3. 外链式



### 1.行内式

> 直接在标签的style属性中添加css的样式

#### 示例代码:

```html
<div style="width:100px; height:200px; backgroundcolor:red"> hello</div>
```

__优点: 方便 直观.	缺点:可重用性差.__



### 2.内嵌式

> 在<head>标签中加入<style>标签,在<style>标签中编写css代码

#### 示例代码:

```css
<head>
	<style type="text/css">
	h3{
		color:red;	
	}
	</style>
</head>
```

__优点: 在同一个页面内部便于复用和维护.  	缺点: 在多个页面之间的可重用性不够高__



### 3.外链式

> 将css代码写在一个单独的.css文件中,在<head>标签中使用<link>标签直接引入该文件到页面中

#### 示例代码:

```html
<link rel="stylesheet" type="text/css" herf="css/main.css">
```

__优点:使得css样式与html页面分离,便于整个页面系统的规划和维护,可重用性高. 	缺点:css代码由于分离到单独的css文件中,容易出现css代码过于集中,若维护不当则极容易造成混乱__

 