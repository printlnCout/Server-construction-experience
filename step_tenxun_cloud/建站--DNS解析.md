解析的作用相当于将域名解析为IP地址，这样就可不用输入IP地址，而是通过输入网址访问网站。

登录DNS解析控制台( https://console.cloud.tencent.com/cns)
点击"添加解析"，弹出的框中输入域名，确定后可添加具体解析记录。
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-DNS%E6%B7%BB%E5%8A%A0%E5%9F%9F%E5%90%8D%E8%A7%A3%E6%9E%90.PNG)
      记录类型为"A"时，将域名指向云服务器(IP地址)，主机类型是域名前缀，例如我的域名：learncodeshare.cn，想要输入"www.learncodeshare.cn"解析到我的服务器IP地址，主机类型填"www"，想要输入"learncodeshare.cn"解析到我的服务器IP地址，主机类型填"@".
      记录类型为"T"的那个，是前面说的SSL证书申请验证时填写的。
      解析需要时间，时间在1天左右。
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E5%9F%9F%E5%90%8D%E8%A7%A3%E6%9E%90%E6%88%90%E5%8A%9F.png)

官方教程：https://cloud.tencent.com/document/product/302/3446