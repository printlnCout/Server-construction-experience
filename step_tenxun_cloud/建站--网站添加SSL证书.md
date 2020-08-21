网站的搭建我采用wordpress教程：https://cloud.tencent.com/edu/learning/course-1812-20652
SSL证书安装教程： https://cloud.tencent.com/document/product/400/4143

由于可能不太安全需要后续修改，我将域名映射到默认站点停止页(需要修改)，好歹那也是个界面，在下面加上公安备案代码，平时在另一地址开发，将wordpress调好以后再映射回来。

没有SSL证书时，浏览器会提示"不安全连接"
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E6%B2%A1%E6%9C%89%E6%B7%BB%E5%8A%A0SSL%E8%AF%81%E4%B9%A6%E6%98%BE%E7%A4%BA%E4%B8%8D%E5%AE%89%E5%85%A8.png)
安装wordpress时选的是nginx，就选择Nginx服务器证书安装
(步骤： https://cloud.tencent.com/document/product/400/35244)

图方便使用宝塔面板装的nginx，当时选的源码安装，nginx.conf文件保存在别处，使用ps aux|grep nginx查看实际使用的nginx路径，再用nginx -t可查看使用的配置文件位置及是否有效

nginx启动、停止与重启教程：https://www.cnblogs.com/wangcp-2014/p/9922845.html

执行nginx配置文件检查命令，结果显示修改后的配置文件通过

[root@printlnCout ~]#nginx -t
nginx: the configuration file /www/server/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /www/server/nginx/conf/nginx.conf test is successful
但https显示域名无法访问
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-https%E6%98%BE%E7%A4%BA%E6%97%A0%E6%B3%95%E8%AE%BF%E9%97%AE.png)
解决不了提交工单，专业人员测试发现443端口被拦截，建议排查服务器防火墙及其他安全设置
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E4%B8%93%E4%B8%9A%E6%B5%8B%E8%AF%95%E4%BA%BA%E5%91%98%E5%B8%AE%E5%8A%A9%E6%8E%92%E6%9F%A5https%E6%97%A0%E6%B3%95%E8%AE%BF%E9%97%AE.png)
所使用的nmap在centos上安装命令：

yum install nmap
在linux服务器上开一个443端口
参考链接：Linux CentOS7 开启80，443端口外网访问权限(https://www.cnblogs.com/yanglang/p/10711826.html)

firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --reload
firewall-cmd --zone=public --query-port=443/tcp
nmap -Pn learncodeshare.cn -p 80,443
显示443端口已被打开

Starting Nmap 6.40 ( http://nmap.org ) at 2020-04-07 15:44 CST
Nmap scan report for learncodeshare.cn (106.53.2.50)
Host is up (0.00035s latency).
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https

蛋疼的nginx缓存，找时间去看下如何设置nginx清除缓存，开始时root目录定位到建站成功的index.html文件所在目录，但该文件没加备案号，直接改写nginx配置文件再重启nginx还是加载被它缓存的文件，云服务器重启后就可以了。当然，浏览器还得清除一下缓存。

按照教程下面的操作，将HTTP自动跳转为HTTPS，这样当用户输入"http://learncodeshare.cn"就可自动跳转到"https://learncodeshare.cn/"，其实就是nginx配置HTTP跳转HTTPS，网上还有许多其他方法可行，当然还要注意nginx缓存的问题。
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-SSL%E8%AF%81%E4%B9%A6%E6%B7%BB%E5%8A%A0%E6%88%90%E5%8A%9F.PNG)
修改好后重启nginx，提示server name重复绑定，一查发现这警告不影响服务器运行
(参考链接：https://www.cnblogs.com/wangkongming/p/4450038.html)

[root@printlnCout ~]#nginx -c /www/server/nginx/conf/nginx.conf
nginx: [warn] conflicting server name "learncodeshare.cn" on 0.0.0.0:80, ignored
