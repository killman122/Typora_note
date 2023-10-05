## json

### json的介绍

json是JavaScript Object Notation 的首字母缩写，翻译过来就是javascript对象表示法，这里说的json就是类似于javascript对象的字符串，它同时是一种数据格式，目前这种数据格式比较流行，逐渐替换掉了传统的xml数据格式。

### json的格式

json有两种格式:

1. 对象格式
2. 数组格式



#### 对象格式:

对象格式的ison数据，使用一对大括号{}，大括号里面放入key:vaue形式的键值对，多个键值对使用逗号分隔·

#### 对象格式的json数据:

```json
{
	"name":"王道",
	"age":22
}
```

__注意:__在javascript中创建对象默认情况下不对属性的key增加双引号,虽然在python等语言中可能是需要在对象的key中添加引号

#### 格式说明:

json中的(key)属性名称和字符串值需要用双引号引起来，用单引号或者不用引号会导致读取数据错误。

#### 数组格式:

数组格式的json数据，使用一对中括号[]，中括号里面的数据使用逗号分隔。

数组格式的json数据:

```
["tom",18,"programmer"]
```



### json数据转换为JavaScript对象(一般用作服务器数据返回处理)

json本质上是字符串，如果在js中操作json数据，可以将json字符串转化为JavaScript对象·

#### 示例代码:

```
var sJson ='{"name":"tom","age":21}';
var oPerson = JSON.parse(sJson);
//将json数据转换为js对象
//操作属性
alert(oPerson.name)
alert(oPerson.age)
```



### 将js对象转换为json数据(一般情况下是向服务器发送数据的请求体中)

```js
let parms = {
    url: `https://xianpoqiang.com/user/checkin`,
    headers: {
        "accept": "application/json, text/javascript, */*; q=0.01",
        "accept-encoding": "gzip, deflate, br",
        "accept-language": "zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6",
        "cache-control": "no-cache",
        "content-length": "0",
        "cookie": cookie,
        "origin": "https://xianpoqiang.com",
        "pragma": "no-cache",
        "referer": "https://xianpoqiang.com/user",
        "sec-ch-ua-mobile": "?0",
        "sec-ch-ua-platform": "Windows",
        "sec-fetch-dest": "empty",
        "sec-fetch-mode": "cors",
        "sec-fetch-site": "same-origin",
        "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36 Edg/105.0.1343.53",
        "x-requested-with": "XMLHttpRequest",
    },
    body:``
};
parmas =JSON.stringify(parms)
```

