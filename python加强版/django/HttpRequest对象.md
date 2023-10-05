# Httprequest对象

HTTP协议向服务器传递参数有哪几种路径?

__注意: __在?前的是url中的路由,在❓后的是url中的查询字符串

- 提取URL中的特定部分,如/weather/2023,可以在服务器端的路由中使用正则表达式,例如京东的商品id不一致,在url中请求得到的响应数据也不一致
- 查询字符串(query string),形如key1=value1&key2=value2; 在路由中也是在url中的?后面编写key1 = value1 例如:search.jd.com/Search?keyword=无人飞机,keyword=无人飞机 的键值对就是一个查询字符串 
- 请求体(body)中发送的数据,比如表单数据,json,xml;
- 在http报文的请求头(header)中,例如:cookie中的应用

### 1.URL中的路径参数

- 如果想从URL中获取值 https://127.0.0.1:8000/10/188

- 应用中`urls.py` 设置路由匹配,匹配url后的路由,将实现不同路由之间的不同响应

- ```python
  from django.urls import path 
  from book.views import index,shop
  urlpatterns = [
      # path('路由',视图函数名)
      path('/10/188',shop), # 注意此处中视图函数的名称需要和视图模块views.py中的视图函数对应
      path('home/', index), # 视图函数中的函数名,不是完整函数,添加规则进行路由匹配
      path('<city_id>/<shop_id>',shop) 更新后
  ]
  ```

  在路由中设置完路由匹配后,需要设置视图以及视图函数中的内容

  进入到子应用的views.py中,设置关于shop的视图函数,视图函数中参数的位置不能错

  ```python
  from django.http import HttpResponse
  from django.shortcuts import render
  from book.models import BookInfo
  
  创建视图函数
  
  def shop(request):
  	return HttpResponse("七哥的小饭店")
  def shop(request,city_id,shop_id): 更新后
  	print(city_id,shop_id)
  	return HttpResponse("七哥的小饭店")
  ```




### 2.Django中的QueryDict对象(查询字符串)

查询字符串:
http://ip:port/path?key=value&key1=value1

url 以 ? 为分割分为2部分, ? 前为请求路径  ? 后面为查询字符串

查询字符串类似于字典的	key-value	多个数据采用&拼接	查询字符串貌似只是适用于get请求

HttpRequest对象的属性GET,POST都是QueryDict类型的对象,与python中的字典不同,QueryDict类型的对象用来处理同一个键带有多个值的情况

- 方法get():根据键获取值
  如果一个键同时拥有多个值将获取最后一个值,如果键不存在则返回None值,可以设置默认值进行后续处理

  ```python
  get('键',默认值)
  ```

- 方法getlist(): 根据键获取值，值以列表返回，可以获取指定键的所有值
  如果键不存在则返回空列表[]，可以设置默认值进行后续处理

  ```
  getlist('值',默认值)
  ```

  

```python
from django.http import HttpResponse
from django.shortcuts import render
from book.models import BookInfo

创建视图函数

def shop(request):
	return HttpResponse("七哥的小饭店")
def shop(request,city_id,shop_id): 更新后
	print(city_id,shop_id)
	return HttpResponse("七哥的小饭店")
def shop(request,city_id,shop_id): 再次更新后
	print(city_id,shop_id)
    query_params = request.GET() # 获取查询字符串的值,返回的对象是查询字典
    print(query_params) # <QueryDict:{'order':{'readcount'}}>
    # 对于传统的字典类型数据来说,一个键只能对应一个值,但是对于QueryDict查询字典来说,一个键可以对应多个值
    # 当一个值查询的数据有多个时,则需要再次进行匹配筛选
    # QueueDict具有字典的特性还具有一键多值
    order = query_params.get('order')# 获取字典中的数据
	print(order)
    # 注意get()方法是能获得最后一个数据(貌似就是最后一个key-value的键值对),但是如果有多个数据则无法使用get,但是可以使用getlist方法获取
    order = query_params.getlist('order')
	print(order)
    return HttpResponse("七哥的小饭店")
```



### 3.查询字符串Query String

获取请求路径中的查询字符串参数(如:?k1=v1&k2=v2),可以通过request GET属性获取,返回QueryDict对象,get方法只能一键一值

```python
# /get/?a=1&b=2&a=3
def get(request):
    a = request.GET.get('a')
    b = request.GET.get('b')
    alist = request.GET.getlist('a')
    print(a) # 3
    print(b) # 2
    print(alist) # ['1','3']
    return HttpResponse('ok')
```



