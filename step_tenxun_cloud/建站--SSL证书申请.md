描述：当时腾讯云搞活动，学生价非常优惠，就按年份买了几年，现在也想像同学一样，自己搞个网站玩玩SSL证书申请：个人用的是腾讯云的云服务器，所以申请的是免费的TrustAsia TLS RSA CA(1年)证书，流程如下：
	1. 登录腾讯云平台账号(已注册过账号及通过实名认证)
	2. 在SSL证书管理界面(https://console.cloud.tencent.com/ssl)点击"申请免费证书"，就在腾讯云蓝色显著标明的旁边(如果有钱你可以试试"购买证书"，看自己需要)
	3. 按照参考教学链接完成内容填写，我只填了证书的通用名称(绑定域名)和申请邮箱，点击下一步
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E5%85%8D%E8%B4%B9SSL%E8%AF%81%E4%B9%A6%E7%94%B3%E8%AF%B7.PNG)

	1. 进入域名验证阶段，该域名初次申请验证时有手动DNS验证和文件验证两种方式，我这已将使用云解析服务了(以及验证过了，现在为了截图再来一次)，我当时选的是手动DNS验证，具体操作步骤可点击对应"详细说明"查看。
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E5%9F%9F%E5%90%8D%E9%AA%8C%E8%AF%81.PNG)

	1. 点击“确定申请”之后，会显示带验证的DNS的基本信息(这里我用的是腾讯云官网自带图像)。我们需要使用这里的信息(红色框标注)取DNS解析控制台添加解析记录，具体操作可点击"操作指引"查看(紫色框标注)
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E6%9F%A5%E7%9C%8B%E5%B8%A6%E9%AA%8C%E8%AF%81%E7%9A%84%E4%BF%A1%E6%81%AF%E7%9A%84DNS.png)

	1. 进入DNS解析控制台(https://console.cloud.tencent.com/cns)，在域名解析列表中的，找到域名解析记录，点击域名(例如我这的"learncodeshare.cn")或"解析"，进入对应域名下的解析
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E8%BF%9B%E5%85%A5DNS%E8%A7%A3%E6%9E%90%E6%8E%A7%E5%88%B6%E5%8F%B0.PNG)
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E6%8E%A7%E5%88%B6%E5%8F%B0%E6%B7%BB%E5%8A%A0%E8%A7%A3%E6%9E%90.PNG)

	1. 点击添加记录，按照当初证书详情界面红框内容，添加"主机记录"、"记录值"，记录类型选择"TXT"，填写完后保存。(我在之前在 DNS解析控制台 将域名解析运行着，如果不是"正常解析"状态，可能还要解析)
![image](https://github.com/printlnCout/Server-construction-experience/blob/master/pic_tenxun_cloud/%E8%85%BE%E8%AE%AF%E4%BA%91-%E5%A1%AB%E5%86%99%E5%85%B7%E4%BD%93%E8%A7%A3%E6%9E%90%E8%AE%B0%E5%BD%95%E4%BF%A1%E6%81%AF.PNG)

	1. 按照腾讯云官方说法，解析生效时间一般为10分钟 - 24小时，但各地解析的最终生效取决于各运营商刷新时间，请您耐心等待。是否成功可查看自动诊断结果查看指引(链接：https://cloud.tencent.com/document/product/400/6760)，或在当初的证书详情页面，点击"自助诊断查询"，需要等待。
	2. 我由于是网站以前按照腾讯云wprdpress教程搭建wordpress解析过域名，添加TXT解析记录后，大概几分钟就在 证书详情界面 的 查询 按钮，点击后显示 已提交审核
	3. 大概一天左右时间，可以收到短信

【腾讯云】尊敬的用户：您名下域名learncodeshare.cn的TrustAsia TLS RSA CA（1年）证书申请已审核通过。请访问腾讯云证书管理控制台查看。感谢您对腾讯云的支持！

后续需要将SSL证书添加到网站

参考教学链接：https://cloud.tencent.com/developer/article/1522482
