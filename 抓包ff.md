抓包那些事

[](https://www.zhihu.com/people/andy0214)



### 代理

简单来说代理就是一个中间人：

![img](https://pic2.zhimg.com/80/v2-08e782576db78178154f82980b254305_720w.webp)

没有代理的时候，客户端只接请求服务器，有了代理，客户端就请求代理，代理再去请求服务器。服务器返回时先返回给代理，代理，返回给客户端。

有了代理我们就可以看到客户端的请求数据，和服务器的返回数据。常见的代理软件：Fiddler 、Charles、Burp Suite Professional，我最常用的就是 Burp Suite Professional，它是 CTF 最常用的抓包工具，内部集成不少实用工具，Java 开发，轻量级，Windows 和 Mac 通用。

### 什么是全局代理，什么是局部代理？

![img](https://pic1.zhimg.com/80/v2-ae515fb19c1d5628c0c4950110f0f724_720w.webp)

使用全局代理，则计算机中的所有程序都会走这个代理，即你本机的IP地址会变成这个代理的IP地址。
如上图，可以看出，所有的进程的请求都先通过代理服务器，再通过代理服务器发给目标服务器。

![img](https://pic1.zhimg.com/80/v2-e9a8d9857b07398a646396836522fed0_720w.webp)

![img](https://pic2.zhimg.com/80/v2-816ebbc052d8fed657e36ee0d9f6742d_720w.webp)

而局部代理，只是部分请求经过代理服务器，而其他请求还是直接发送到目标服务器的。
如上面的两张图，图1的进程A的请求经过了代理服务器，而图2的进程B的请求则是直接发送到目标服务器。

### 为什么要设置全局代理？

### 原因1——检测代理

APP在发起网络请求前会检测系统是否设置了代理，如果发现有代理，就不发起请求。以下是一段APP检测系统是否有代理的实例代码：

```java
public static boolean isWifiProxy(Context context) {
    final boolean IS_ICS_OR_LATER = Build.VERSION.SDK_INT >= Build.VERSION_CODES.ICE_CREAM_SANDWICH;
    String proxyAddress;
    int proxyPort;
    if (IS_ICS_OR_LATER) {
        proxyAddress = System.getProperty("http.proxyHost");    //获取代理主机
        String portStr = System.getProperty("http.proxyPort");  //获取代理端口
        proxyPort = Integer.parseInt((portStr != null ? portStr : "-1"));
    } else {
        proxyAddress = android.net.Proxy.getHost(context);
        proxyPort = android.net.Proxy.getPort(context);
    }
   Log.i("代理信息","proxyAddress :"+proxyAddress + "prot : " proxyPort")
   return (!TextUtils.isEmpty(proxyAddress)) && (proxyPort != -1);
}
```

### 特征

设置手机代理后，APP无法获取网络数据。

### 解决方案

### 方案一

适合在 PC 电脑上进行。通过修改 host 文件，让客户端认为代理服务器就是目标服务器。比如客户端请求 [http://xxxxxx.com](https://link.zhihu.com/?target=http%3A//xxxxxx.com)，我们的代理服务器是 192.168.3.9:80，那就在 host 里面添加 "192.168.3.9 [http://xxxxxx.com](https://link.zhihu.com/?target=http%3A//xxxxxx.com)" 然后代理服务器收到请求后在转发到 [http://xxxxxx.com](https://link.zhihu.com/?target=http%3A//xxxxxx.com)。

### 方案二

适合移动设备或 PC，简单来说就是使用 VPN 将终端设备的流量转发到代理服务器。VPN 软件上添加一个 HTTP 服务器，就是代理服务器的 IP 和 端口，然后设置全局代理，这样所有的请求都会走 VPN，也就是走代理服务器了。这样就可以抓包。亲测有效。

### 原因2——# No Proxy

除了上述情况外，有些 app 默认就是不走系统代理，或者某些关键的请求不走代理，实际情况还真不少，这种情况下，设置了代理也没用。 以下是一段使用`No Proxy`参数发起网络请求的代码：

```java
public void run() {
    Looper.prepare();
    OkHttpClient okHttpClient = new OkHttpClient.Builder().
        proxy(Proxy.NO_PROXY).      //使用此参数，可绕过系统代理直接发包
        build();
    Request request = new Request.Builder()
        .url("http://www.baidu.com")
        .build();
    Response response = null;
    try {
        response = okHttpClient.newCall(request).execute();
        Toast.makeText(this, Objects.requireNonNull(response.body()).string(), Toast.LENGTH_SHORT).show();
    } catch (IOException e) {
        e.printStackTrace();
    }
        Looper.loop();
}
```

### 特征

设置代理后，APP依然能正常获取网络数据，但抓包工具无法抓到该APP的数据包。

### 解决方案

### 方案一

直接在系统底层使用`iptables`强制转发流量（ProxyDroid：全局模式）

### 方案二

以VPN形式设置代理（Drony，启动后手机状态栏上会显示VPN图标）

### 方案三

直接hook上面代码所在点，使其强制走代理，具体hook代码可到星球自取。

### 全局代理怎么设置？

我们介绍一下针对移动端设备的全局代理的设置。

### Android系统

推荐从Google Play下载ProxyDroid，目前最新版本是V3.2.0，对于我们基本的全局代理抓包只需要做如下的基本配置即可。

### 对ProxyDroid进行配置（基本配置）:

- Auto Setting不勾选，我们手动进行配置。
- Host：输入代理服务器IP。
- Port：输入代理服务器端口。（HTTP默认808，SOCKS默认1080，具体视服务器情况而定）
- Proxy Type选择代理服务器提供服务类型：我这里选择Socks5。
- Auto Connect为当2G/3G/WIFI网络开启时，自动开启代理服务。不勾选，我们手动启动，以获取最大灵活性。
- Bypass Addresses：相当于黑名单列表，选择排除代理的IP范围，有需要的可以自己手动设置。

![img](https://pic1.zhimg.com/80/v2-480aec6da138c8273e9bf2f8e30b32e4_720w.webp)

### 认证信息配置：

- Enable Authentication ：如果代理服务器需要账户、密码认证，勾选。
- User ：认证账户名。
- Password ：认证密码。
- NTLM Authentication：NTLM/ NTLM2，Windows早期的一种认证方式，不用勾选。

![img](https://pic2.zhimg.com/80/v2-f7608a617df6e74cf46eefe742a0b395_720w.webp)

### 特征设置：

- Global Proxy：一定要勾选，即为全局代理，代理所有App。
- Individual Proxy：单独代理所选App ，勾选了（1）的不用管。
- Bypass Mode：勾选了代表（2）中所选App不代理，勾选了（1）的不用管。
- DNS Proxy：开启DNS代理。

![img](https://pic4.zhimg.com/80/v2-89b268a23f208441335e5192243207e7_720w.webp)

### 通知设置：

- Ringtone ：选择通知铃声。
- Vibrate ：选择连接发生变化时是否震动提醒。

![img](https://pic3.zhimg.com/80/v2-12ed75c47243a4eb392dbdfba9b82382_720w.webp)

### iOS系统

我们使用小火箭Shadowrocket，简单好用，不过现在不太容易下载到对应系统版本的包。

![img](https://pic2.zhimg.com/80/v2-a22886f6111dd2eeb956691ace6e0bd9_720w.webp)

### 添加节点

![img](https://pic2.zhimg.com/80/v2-75b6fc6153e41bf93657b24d4a57e4d1_720w.webp)

\- 我们点击右上角的+号添加节点 - 类型一般选择HTTP - 添加服务器和端口即可

### 打开VPN

![img](https://pic4.zhimg.com/80/v2-ddeac0888cf8acd98533935fa4976023_720w.webp)

\- 选择我们刚才配置的节点，最前面显示小黄点 - 全局路由选择代理 - 开启上面的开关即可

按照以上配置，我们就可以针对一些不走系统代理的客户端进行抓包了。

### BurpSuite高级用法透明代理抓包（不用设置代理，不用安装证书）

### 路由重定向

### 原理

HTTP/HTPS的默认端口分别是80和443我们在BurpSuite并设置透明代理，模拟并监听这两个端口，在透明代理中应用认为我们用BurpSuite模拟服务器开放端口就是真实服务器，实际上将手机的TCP协议的路由都重定向到我们的电脑IP地址中进而BurpSuite会进行代理服务器转发。

### 操作

- 添加80、443、8080端口，设置透明代理

![img](https://pic2.zhimg.com/80/v2-289e842e723fe9c06a8320547817f545_720w.webp)

![img](https://pic3.zhimg.com/80/v2-dd61da3df71f66b68b00e19be1d946a2_720w.webp)

![img](https://pic4.zhimg.com/80/v2-199c91552f99a04c3dd1541b6a7b5c67_720w.webp)

![img](https://pic4.zhimg.com/80/v2-73ed44d31d9266b232a99675211c6c13_720w.webp)

按照上面步骤依次添加其他几个端口：

![img](https://pic1.zhimg.com/80/v2-a1785c8fb736b0b58151c280c5d52364_720w.webp)

- 接下来进入手机shell进行配置（手机需要root）

```bash
iptables -t nat -A OUTPUT -d 0.0.0.0/0 -p tcp -j DNAT --to （电脑IP地址）   #设置重定向
iptables -t nat -D OUTPUT -d 0.0.0.0/0 -p tcp -j DNAT --to （电脑IP地址）   #取消重定向
```

![img](https://pic4.zhimg.com/80/v2-205ad6cb546df266fc8fa25b46a21f33_720w.webp)



### 其他全局代理工具——Drony（不建议）

不管是Drony，还是上面介绍的ProxyDroid，其实都是一款VPN工具，即将手机上的所有流量都重定向到drony自身 ，这样drony就可以管理所有手机上的网络流量，甚至可以对手机上不同APP的流量进行单独配置。

### 安装drony

您可以在网络上搜索drony选择自己想要的版本进行安装，或者在到星球下载最新版，安装完成后打开软件如下图

### 开启代理抓包软件（我使用的是Charles）

我用了burp好像有点问题，两款抓包工具实现原理略有差别，有时候这个不行的时候可以试试另外的，说不定就有奇迹。 其他证书相关内容不做赘述，可参考之前的文章。

### 配置drony转发（左右划动切换功能页面）

点击选择Networks Wi-Fi 进入配置

![img](https://pic1.zhimg.com/80/v2-6872e145b1702a8967ae5f4972bdba18_720w.webp)

选择我们手机连接的wifi

![img](https://pic3.zhimg.com/80/v2-41e49381c217b36d45bc2e97bfb43652_720w.webp)

配置要为当前网络使用的代理入口（这里直接填写burp代理地址就可以），选择代理模式为手动（Manual）

![img](https://pic4.zhimg.com/80/v2-ec87632b2f08564795b8cabd90a97f07_720w.webp)

注意Proxy type代理方式要选择 Plain http proxy

![img](https://pic3.zhimg.com/80/v2-b94b592b3299df38728ed648e927908e_720w.webp)

Filter default value 选择 Direct all ，然后点击下面的Rule设置应用规则

![img](https://pic4.zhimg.com/80/v2-2f184c314740a820b17bda83a473ab93_720w.webp)

![img](https://pic4.zhimg.com/80/v2-0d626b56e01c866dcd3d170fe7882397_720w.webp)

\- Network id处 选择当前wifi的SSID - Action 选择 Local proxy chain - Application 选择需要强制代理的APP - Hostname 及 Port 不填 表示所有的都会被强制代理，因为APP可能会使用其他的网络协议不一定都是http，可能不希望把所有流量都引流到http代理服务器，这个时候就会使用这个配置指定ip及端口才转发

完成后保存即可，然后返回到SETTING主页，滑动到LOG页，点击下面按钮，使其处于ON的状态（表示启用）

### adb命令行设置代理

- 设置代理

```bash
adb shell settings put global http_proxy ip:端口
```

- 关闭代理,建议第一种（三条都要执行）

```text
adb shell settings delete global http_proxy
adb shell settings delete global global_http_proxy_port
adb shell settings delete global global_http_proxy_host
```

或者

```text
adb shell settings put global http_proxy:0
```

### 实验（失败）

我们可以用iptables命令查看经过上面的ProxyDroid配置之后的网络配置参数具体是什么情况，看看能不能通过iptables的命令完成ProxyDroid的配置，事实证明是可以完成对应的配置，但是结果不太一样，无法抓包的还是无法抓包，不知道问题出在哪里，有大神知道可以指导一下。

- ProxyDroid配置后的参数：

![img](https://pic1.zhimg.com/80/v2-ca682d08f753c5ee0069a78551256d14_720w.webp)

- 通过iptables命令进行配置：

```text
iptables -t nat -A PREROUTING -p tcp -d 192.168.43.0/24 -j RETURN
iptables -t nat -A PREROUTING -p tcp -j REDIRECT --to-ports 8124
iptables -t nat -A OUTPUT -p tcp -d 172.31.253.158 -j RETURN
iptables -t nat -A OUTPUT -p tcp --dport 80 -j REDIRECT --to 8123
iptables -t nat -A OUTPUT -p tcp --dport 443 -j REDIRECT --to 8124
iptables -t nat -A OUTPUT -p tcp --dport 5228 -j REDIRECT --to 8124
```

经过以上命令后，配置参数和上图一致，但是还是无法达到ProxyDroid的效果。

### 拓展分析

无奈之下打算分析一下ProxyDroid代码，看看代码中具体怎么实现 - 找到了一些使用iptables的命令痕迹

![img](https://pic1.zhimg.com/80/v2-436672fd402c4d0d6599cccacf3fe5f4_720w.webp)

![img](https://pic1.zhimg.com/80/v2-7f05fef26c6b615c4e156fa4478036c8_720w.webp)

\- 跟踪一下吧

![img](https://pic4.zhimg.com/80/v2-b49a5e909ae0835ae236af479249a427_720w.webp)

![img](https://pic1.zhimg.com/80/v2-adf204f0323eb1f180e5328be3c30640_720w.webp)

\- 包含了一些root检测

![img](https://pic1.zhimg.com/80/v2-8fef80a5715447c38e29725640d0403c_720w.webp)

\- 好多命令啊，还要提权，我废了

![img](https://pic4.zhimg.com/80/v2-5f5ecfcaf1c3118b03515f58cbd63ab7_720w.webp)

[ProxyDroid源码]（[https://github.com/madeye/proxydroid](https://link.zhihu.com/?target=https%3A//github.com/madeye/proxydroid)），感兴趣的可以看看。看了一下用到了cntlm、redsocks、netfilter/iptables、transproxy、stunnel等开源软件，还是相当复杂的。

## **所有工具可到星球下载。**

参考文章：

1、[https://blog.csdn.net/codezjx/article/details/8872071](https://link.zhihu.com/?target=https%3A//blog.csdn.net/codezjx/article/details/8872071)

2、[https://blog.csdn.net/somenzz/article/details/124113506](https://link.zhihu.com/?target=https%3A//blog.csdn.net/somenzz/article/details/124113506)

3、[https://blog.csdn.net/weixin_44575208/article/details/107345190?spm=1001.2014.3001.5501](https://link.zhihu.com/?target=https%3A//blog.csdn.net/weixin_44575208/article/details/107345190%3Fspm%3D1001.2014.3001.5501)

4、[https://xz.aliyun.com/t/9843](https://link.zhihu.com/?target=https%3A//xz.aliyun.com/t/9843)

5、[https://www.cnblogs.com/lulianqi/p/11380794.html](https://link.zhihu.com/?target=https%3A//www.cnblogs.com/lulianqi/p/11380794.html)

发布于 2023-03-09 10:43・IP 属地北京

数据抓包

抓包





对于burp中的调试功能,如果透明代理和全局代理抓包失败的情况下可以使用burp的repeater功能

![image-20230812130950421](image-20230812130950421.png)

如果要添加关于请求的注释可以在请求中添加# 或者是右键123...tab重命名tab键,添加分组和注释





所需工具1.一部手机 2.一台电脑 3.一条数据线情景模拟某个网页只能在微信中打开，但我想要抓包调试怎么办？1.HttpCannary(小黄鸟)这时候你可能会打开HttpCannary(小黄鸟) 目标应用选择微信 回到主界面，点击按钮开始抓包 打开微信，打开想要的网页 **回到小黄鸟发现抓到的都是UDP连接和网页没有半毛钱关系** 2.fiddler打开电脑，手机用数据线连接上 打开fiddler，配置好端口信息 手机用微信打开对应的网页 电脑上fiddler查看抓到的包 但是这里只能看到数据包，**不方便调试** 一招解决以上问题！正文开始1.首先用数据线把手机连接到电脑2.手机打开USB调试3.手机进入微信随便打开一个聊天窗口输入并发送：  `http://debugxweb.qq.com/?inspector=true`点击打开这个链接，弹出“执行成功”，即可 4.手机微信打开想要抓包调试的网页5.电脑上打开chrome内核的浏览器或edge浏览器chrome内核的浏览器输入`chrome://inspect/#devices` edge浏览器输入：`edge://inspect/#devices` 打开后稍等片刻 然后在打开的界面中点击这个 ![图片1](https://blog.wystudio.xyz/wp-content/uploads/2023/08/360%E6%88%AA%E5%9B%BE20230826214321764.jpg) 点击后会跳转到这个界面 ![图片2](https://blog.wystudio.xyz/wp-content/uploads/2023/08/360%E6%88%AA%E5%9B%BE20230826214138682.jpg) 到这里你就可以像在电脑浏览器的开发人员工具一样调试这个网页 打断点，审查元素等