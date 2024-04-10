# Catcher(捕手)

最近在学习golang，看到EHole感觉真的很好用，所以写了这个工具

## 0x00: 简介

Catcher重点系统指纹漏洞验证工具，适用于外网打点，资产梳理漏洞检查。

在面对大量的子域名时，Catcher可将其进行指纹识别，将已经识别成功的指纹进行对应的漏洞验证，并对域名进行cdn判断，将未使用cdn域名进行端口扫描
![image-1](https://github.com/wudijun/Catcher/blob/master/image/1.png)


## 0x01: 使用

工具目录如下

![image-2](https://github.com/wudijun/Catcher/blob/master/image/2.png)

domain.txt: 需要进行测试的域名（可直接写入ip和端口的形式如1.1.1.1:80，也可写url: https://www.xxx.com的形式，也可直接写域名www.xxx.com）

finger.json: 指纹文件

poc : poc文件



使用时直接通过命令行运行Catcher.exe即可，不需要使用任何参数

## 0x02: 流程

1.Catcher首先会对域名通过finger.json文件进行指纹识别

![image-3](https://github.com/wudijun/Catcher/blob/master/image/3.png)

2.识别成功后会进入poc文件下去找具体对应的poc进行测试

比如识别到的指纹为Atlassian Confluence，那么就会进入到 poc文件下的Atlassian Confluence文件下，去运行该文件中所有的poc文件

![image-4](https://github.com/wudijun/Catcher/blob/master/image/4.png)

 Catcher中内置了许多用于漏洞验证的poc

![image-5](https://github.com/wudijun/Catcher/blob/master/image/5.png)

![image-6](https://github.com/wudijun/Catcher/blob/master/image/6.png)

后续会继续更新指纹以及poc

3.进行完漏洞测试后会将所有域名进行cdn判断（不可能做到绝对准确）

4.判断完cdn后会去获取域名对应的ip，并进行端口扫描

5.运行结束后会将结果保存到results文件下

![image-7](https://github.com/wudijun/Catcher/blob/master/image/7.png)

该文件下有7个文件 

Cdn.txt: 使用了cdn的域名

NoCdn.txt: 没有使用cdn的域名

ErrorCdn.txt: 未判断出是否使用cdn的域名

Finger.json: 指纹识别到的域名

NoFinger.json: 未指纹识别到的域名

PocResults.txt: 漏洞测试的结果

Ports.txt: 端口扫描结果

 

在查看结果时推荐使用sublime等编译器打开查看，文本文档直接打开不太友好

![image-8](https://github.com/wudijun/Catcher/blob/master/image/8.png)

除了对多个域名进行指纹识别漏洞验证

因为domain.txt中也可写入ip端口的形式，并且Catcher中有很多poc。

对多个资产、单个资产进行批量的泛微OA、用友OA等漏洞验证也是不错的选择

![image-10](https://github.com/wudijun/Catcher/blob/master/image/10.png)

![image-9](https://github.com/wudijun/Catcher/blob/master/image/9.png) 



## 参考优秀项目

EHole：https://github.com/EdgeSecurityTeam/EHole

## 免责声明
本工具仅面向合法授权的企业安全建设行为，如您需要测试本工具的可用性，请自行搭建靶机环境。

为避免被恶意使用，本项目所有收录的poc均为漏洞的理论判断，不存在漏洞利用过程，不会对目标发起真实攻击和漏洞利用。

在使用本工具进行检测时，您应确保该行为符合当地的法律法规，并且已经取得了足够的授权。请勿对非授权目标进行扫描。

如您在使用本工具的过程中存在任何非法行为，您需自行承担相应后果，我们将不承担任何法律及连带责任。

在安装并使用本工具前，请您务必审慎阅读、充分理解各条款内容，限制、免责条款或者其他涉及您重大权益的条款可能会以加粗、加下划线等形式提示您重点注意。 除非您已充分阅读、完全理解并接受本协议所有条款，否则，请您不要安装并使用本工具。您的使用行为或者您以其他任何明示或者默示方式表示接受本协议的，即视为您已阅读并同意本协议的约束。
