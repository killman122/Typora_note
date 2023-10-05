## 获取和设置元素的内容

### html方法的使用

jquery中的htmI方法可以获取和设置标签的html内容

#### 示例代码:

<script>
$(function(){
var $div =$("#div1");
获取标签的htm1内容I
var result = $div.html();
alert(result);
// 设置标签的htm1内容·之前的内容会清除
$div.html("<span style="color:red">你好</span>”);
// 追加html内容
$div.append("<span style="color:red'>你好</span>");
});
</script>

#### 说明:

给指定标签追加html内容使用append方法

### 小结

- 获取和设置元素的内容使用: htrml方法
- 给指定元素追加htnl内容使用:append方法