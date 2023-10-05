  1.生成一个带有id的div标签。
div#dome

<div id="dome"></div>
1
2.生成一个带有class的div标签。
div.dome

<div class="dome"></div>
1
3.生成一个带有特定属性的标签。
a[href=“www.baidu.com”]

<a href="www.baidu.com"></a>
1
4.生成一个标签有内容的div。
div{内容}

<div>内容</div>
1
5.在div标签里嵌套一个p标签。
div>p

<div>
    <p></p>
</div>
1
2
3
6.给div创建一个兄弟标签h1。
div+h1

<div></div>
<h1></h1>
1
2
7.给span标签生成父级元素div的同级元素p。
p^div.span

<p></p>
<div><span></span></div>
1
2
8.分组操作符。
(div.box>(img[src=img/loading.gif].img))*1

<div class="box"><img src="img/loading.gif" alt="" class="img"></div>
1
9.乘法操作符。
div>ui>li*10

<div>
    <ui>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ui>
</div>
1

10.自动计数。
div>ui>li{$}*10+p{如果生成两位数则使用两个连续的 $$ ，更多位数以此类推。}

<div>
    <ui>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
        <li>7</li>
        <li>8</li>
        <li>9</li>
        <li>10</li>
        <p>如果生成两位数则使用两个连续的 $$ ，更多位数以此类推。</p>
    </ui>
</div>

11.自动添加单词。
div>ul>li>lorem4*5



在vscode中直接按下ctrl+shift+c可以快速打开管理员权限下的命令提示行,在当前的文件路径下,注意该功能只在vscode中存在,在idea中不存在

使用div:xxx 设置的是type的类型,可以直接调用



在vscode中使用`shift+alt+f`可以快速格式化代码,由于直接使用idea中快速格式化代码的快捷键失效在vscode中,ctrl+alt+L
