## jQuery选择器

### 1.jQuery选择器的介绍

jquery选择器就是快速选择标签元素，获取标签的，选择规则和css样式一样·(和css选择器一样只是设置样式)

### 2.jQuery选择器的种类

1. 标签选择器
2. 类选择器
3. id选择器
4. 层级选择器
5. 属性选择器

__示例代码:__

```js
$('li')// 选择所有的li标签
$("#myId")// 选择id为myId的标签
$(".myClass")// 选择class名为myClass的标签
$("#ul1 li span") // 选择id为ul
$('input[name=first]') // 选择name属性为first的input标签,似乎和xpath还是和bs4的代码几乎一致
```

__说明:__
可以使用length属性来判断标签是否选择成功,如果length大于0表示选择成功，否则选择失败·

