GitHub 应该是广大开发者最常去的站点，GitHub 提供了大量优秀的项目，是广大开发者寻找资源，交友学习的好地方，虽然 GitHub 没有被 Q，但是由于 CDN 服务器都在国外，所以国内访问 GitHub 的速度实在是慢的一匹，页面经常刷新不出来，对于一些需要 clone 项目的码农来说更是雪上加霜，在我们获取知识的道路上增加了重重的阻碍!
![请添加图片描述](https://img-blog.csdnimg.cn/0f4eee2e831946aa8fe7807ee279c62c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
我们尝试 ping 一下 GitHub 的官网，我们发现访问的时候延迟很慢，导致网页打开很慢，甚至有时访问不到，出现像我这样的情况
![请添加图片描述](https://img-blog.csdnimg.cn/08a0cc31bb804da984ed952026074feb.png)
所以经过不断尝试和查阅资料，终于找到了在不用 T 子的情况下，加速 GitHub 访问速度的方法，最后分享给大家
经过我查阅资料，分析后，提供给大家三种方式解决 GitHub 访问缓慢的问题（这里不提供镜像网站的方法）

首先我们回顾一下 DNS 域名访问的过程
域名解析全过程

域名就是浏览器访问网站地址栏输入的网址，如www.baidu.com.
想要访问网站，就要找到网站服务器的 IP 地址，域名和 IP 地址是对应关系，所以域名解析的过程就是通过域名找到对应的 IP 地址
![请添加图片描述](https://img-blog.csdnimg.cn/f6455641075d48bc8d13c8307c849bbc.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
这个域名解析的过程可以分为十步。如果在当前步骤查询到域名对应的 IP 地址就不会继续后面的步骤

1、浏览器搜索自己的 DNS（Domain Name System,域名系统）缓存
2、搜索操作系统中的 DNS，如内存中的 DNS 缓存或者本地的 hosts 文件（windows 环境下，维护一张域名与 IP 地址的对应表，位置一般在 C:\Windows\System32\drivers\etc\hosts）
![请添加图片描述](https://img-blog.csdnimg.cn/fc9bdebaac18480eb25259efb5ada9d1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
3、使用递归查询的方式查询本地域名解析服务器，该服务器地址可以通过手动设置，未设置则使用路由器中的本地 DNS 地址
4、本地域名服务器采用迭代查询的方式
(1)、向根域名服务器（其虽然没有每个域名的具体信息，但存储了负责的每个域，如 com,net,org 等的解析的顶级域名服务器的地址）查找，根域名服务器返回 com 域的顶级域名服务器的地址
(2)、本地域名服务器向 com 域的顶级域名服务器发起请求，返回 baidu.com 权限域名服务器（权限域名服务器，用来保存该区中所有主机域名到 ip 地址的映射）地址
(3)、本地域名服务器向 baidu.com 权限域名服务器发起请求，得到www.baidu.com的IP地址

5、本地域名服务器将得到的 IP 地址返回给操作系统，同时自己也将 IP 地址缓存起来

6、操作系统将 IP 地址返回给浏览器，同时自己也将 IP 地址缓存起来

7、至此，浏览器已经得到域名对应的 IP 地址

这里需要说明一下 递归查询和迭代查询的区别

——递归查询是一种 DNS 服务器的查询模式，在该模式下 DNS 服务器接收到客户机请求，必须使用一个准确的查询结果回复客户机。如果 DNS 服务器本地没有存储查询 DNS 查询信息，那么该服务器会询问其他服务器，并将返回的查询结果提交给客户机

——迭代查询 DNS 服务器，在该模式下 DNS 服务器会向客户机提供其他能够解析查询请求的 DNS 服务器地址，当客户机发送查询请求时，DNS 服务器并不直接回复查询结果，而是告诉客户机另一台 DNS 服务器地址，客户机再向这台 DNS 服务器提交请求，依次循环直到返回查询结果

言归正传，GitHub 在国内访问速度慢的原因其实有很多，但最主要的原因就是 GitHub 的分发加速网络域名遭到 DNS 的污染，为了解决这个问题，查询大量相关资料以及查阅各位大佬的解决方案，最佳方案就是通过修改 Hosts 文件，绕过国内 DNS 解析，直接访问 GitHub 的 CDN 节点，从而达到加速的目的，大多数关于此法的介绍，只提供了 3 个 GitHub 的相关域名，而且需要一个个去查，根据查到的 IP，再去自己 ping,肉眼选取最快的 IP，自行编译成 ip+域名格式贴到 hosts 文件里，

下面以 GitHub.com 该域名为例，进行演示
首先进入 ipaddress.com 输入想要查询的域名

![在这里插入图片描述](https://img-blog.csdnimg.cn/4e723aed728f4a3ca83d99247b3a3571.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
跳转后我们找到我们需要的有关信息
![请添加图片描述](https://img-blog.csdnimg.cn/f6ba56a314c94de49b57d3f4fcee6537.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)![在这里插入图片描述](https://img-blog.csdnimg.cn/910c9d57a1304fa8978793443e593e9e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/81b9001d820040df81e36a110f8e0dd3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
查询后我们可以得到 GitHub.com 的 IP：140.82.112.4，所以我们以这个为例， 将他译成 ip+域名格式即

140.82.112.4 github.com
然后我们修改 hosts 文件，一般他的路径为

C:\Windows\System32\drivers\etc\hosts
![在这里插入图片描述](https://img-blog.csdnimg.cn/5a27ba782d9245ce9553bb7d10b2d804.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
记事本方式打开 hosts,

140.82.112.4 github.com

直接复制粘贴添加刚刚查询到的 IP 地址+域名格式到 hosts 文件里最后一行保存即可（由于将 IP 地址添加到 hosts 毫无操作性可言，这里就不作讲解了，不懂的自行百度一下即可）
![在这里插入图片描述](https://img-blog.csdnimg.cn/c3be682729544c4796658c8f8617904a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
然后再 ping 一下发现可以访问了（由于这里只是示范，所以选取的域名并不是速度最快的）
![在这里插入图片描述](https://img-blog.csdnimg.cn/82a33fd2608b408180b1008882c0a63b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
这里就不得不说一下，其实 GitHub 用到的相关域名有很多，我整理了一下，一共有十几个，如下：

```bash
github.global.ssl.fastly.net
github.com
assets-cdn.github.com
documentcloud.github.com
gist.github.com
help.github.com
nodeload.github.com
codeload.github.com
raw.github.com
status.github.com
training.github.com
avatars0.githubusercontent.com
avatars1.githubusercontent.com
avatars2.githubusercontent.com
avatars3.githubusercontent.com
```

但是我查询解决方案发现大多数解决是直接以 GitHub.com 作为默认域名，对 github.com 不同的 DNS 所在地的 TTL 值进行了测试，选取 TTL（IP 协议包中的一个时间值）值最小的 DNS 所在地的 ip 地址为最优速度，

下面我们讲解直接以 github.com 为默认域名，对不同 DNS 所在地的 TTL 值进行测试，进而确定最有速度的 IP 地址，这也是我将要讲解的第二种方法

1、首先我们随便选择一个 DNS 查询网站，这里我用的是
http://tool.chinaz.com/dns
，接着输入 github.com，如图所示

![在这里插入图片描述](https://img-blog.csdnimg.cn/6d0de1b8a33242d99e9de63c54716c40.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
TTL 值小的速度越快，选择 TTL 值最小的 DNS 所在地对应的 IP 地址加上域名添加到 hosts 里即可 13.114.40.48 github.com，我们再次 ping github.com,发现成功了
![在这里插入图片描述](https://img-blog.csdnimg.cn/f2efa3e0dd304a8e8cbb97c6afa40391.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)
这说明该方法有效。

但是认真观察我们会发现，不同域名之间的 TTL 值相差很大，所以将 GitHub.com 作为默认域名选择 TTL 值最小的 DNS 所在地对应的 IP 地址，得到的并不是在不加 T 子的情况下的最快速度，所以如果对速度要求不是特别的高的话，以上两种都可以尝试选择，只要能满足需求即可，如果需要更快的速度的话，建议大家先对不同域名的 IP 进行 ping ,测试找到速度更快的域名，接着对筛选出来的域名测试并得到其 TTL 值最小的 DNS 所在地对应的 IP 地址，同理，添加到 hosts 里即可。

在这里补充一下，建议使用谷歌浏览器访问 GitHub
1、因为这种形式经常会被黑客利用，所以电脑安装的杀毒软件很有可能会报病毒，这时候只需要把这部分添加到信任区即可

2、若某天访问 GitHub 的时候发现再次变慢了，再次进行上述操作，更新网址对应的 IP 地址
3、若某天打开 GitHub 还是感觉很慢，更新了上述 IP 地址也没有用，可以尝试刷新一下 dns 缓存
方法：
在 cmd 中输入 ipconfig/flushdns
![在这里插入图片描述](https://img-blog.csdnimg.cn/7caeb425acce407db9ceba75c92088a7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6Iyr5rih44CC,size_20,color_FFFFFF,t_70,g_se,x_16)

个人 csdn:

[https://blog.csdn.net/density\_]()
