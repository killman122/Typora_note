### 布局常用样式属性

- width 设置元素(标签)的宽度，如:width:100px;
- height 设置元素(标签的高度，如:height:200px;
- background 设置元素背景色或者背景图片，如: background;gold; 设置元素的背景色,background:url(images/logo.png);设置元素的背景图片。
- border设置元素四周的边框，如:border;1px solid black; 设置元素四周边框是1像素宽的黑色实
- 以上也可以拆分成四个边的写法，分别设置四个边的 :
- border-top 设置顶边边框，如:border-top:10px solid red;
- border-left 设置左边边框，如:border-left:10px solid blue;
- border-right 设置右边边框，如:border-right:10px solid green;
- border-bottom 设置底边边框，如:border-bottom:10px solid pink;
- padding 设置元素包含的内容和元素边框的距离，也叫内边距，如padding:20px;padding是同时设置4个边的，也可以像border一样拆分成分别设置四个边:padding-toppadding-leftpadding-rightpadding-bottome
- margin 设置元素和外界的距离，也叫外边距，如margin:20px;margin是同时设置4个边的，也可以像border一样拆分成分别设置四个边margin-topmargin-leftmargin-rightmargin-bottom
- float 设置元素浮动，浮动可以让块元素排列在一行，浮动分为左浮动:float:left; 右浮动:float;right:



### 文本常用样式属性

- color 设置文字的颜色·如: color:red:
- font-size 设置文字的大小，如:font-size:12px;
- font-family 设置文字的字体，如:font-family: 微软雅黑为了避免中文字不兼容，一般写成:font-family:'Microsoft Yahei;
- font-weight 设置文字是否加粗，如:fontweight;bold; 设置加粗 font-weight:normal 设置不加粗
- line-height 设置文字的行高，如: ine-height:24px;表示文字高度加上文字上下的间距是24px，也就是每一行占有的高度是24px
- text-decoration 设置文字的下划线，如:text-decoration;none; 将文字下划线去掉
- text-align 设置文字水平对齐方式，如text-align:center 设置文字水平居中
- text-indent设置文字首行缩进，如:text-indent:24px;设置文字首行缩进24px

想要设置多个标签在同一行显示,或者多个容器标签显示在同一次侧,左侧或者右侧或者一个左侧一个右侧,可以使用css中的float属性设置,该属性设置标签是向左向右还是向上等方向浮动标签