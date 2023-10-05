### 如果是使用豆瓣的镜像源安装依赖包(调用外部的requirements文件)

`pip install -i http://pypi.douban.com/simple --trusted-host pypi.douban.com -r requirements.txt `

> 其中requirements.txt文件存储的是所有需要安装的python依赖文件,其中包含了xx模块等

需要注意的是在-r参数后面的参数是需要安装的一个模块,或者是很多的模块所组成的文本,文本中存储着所有所需要的model

## requirements 文件

> 在python项目中必须要包含一个requirements.txt文件,用于记录所有的依赖包和精确的版本号,方便在新环境中进行部署



### 如何生成requirements文件

>`pip freeze >requirements.txt`

 在控制台输入pip freeze>requirements.txt 就可以生成所需要并已经安装过的所有的model依赖