# 使用moonlight进行PC串流教程

使用Moonlight与Nvidia Gforce Experience进行PC（游戏）串流，分为本地串流和远程串流2种方式。

## 系统要求和前期准备
### 1）串流PC:使用N卡，GTX 600以上型号，并且安装Nvidia Geforce Experience
### 2）可以对家庭路由器进行配置
### 3）拥有接受串流的移动设备

## 本地串流
本地串流比较容易，就是串流PC和接受串流的移动设备在同一个局域网中，只要安装好软件既可以使用

### 1）串流PC配置
在串流PC中打开Gforce Experience，在设置里面的"SHIELD"中打开“GAMESTREAM”选项
![](https://github.com/sheldonl3/Moonlight_Config/blob/master/gfe.png)
GFE默认会添加支持串流的游戏，并且可以添加任何程序

### 2）移动端配置
安装moonlight客户端，默认搜索局域网内开启GAMESTREAM功能的PC，之后进行连接配对即可使用


## 远程串流
远程串流是使用外部网络连接家庭内网的游戏主机进行串流，需要解决内网的访问问题
![](https://github.com/sheldonl3/Moonlight_Config/blob/master/%E7%BD%91%E7%BB%9C%E6%8B%93%E6%89%91.png)
可以使用IPV4或者IPV6进行串流，但是IPV6的访问需要路由器的支持，配置IPV6防火墙，由于条件限制本文使用IPV4
因为用户从外网访问，因此需要进行内网穿透，需要通过对路由器和猫进行配置

### 1）猫
猫配置最简单的方式是直接关闭防火墙，但是不安全
因此需要对指定的端口进行nat转发，在moonlight的[Setup Guide](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide)中可以找到相关端口
为了保证lan地址不变，根据使用的lan端口的mac地址配置静态ip地址
![](https://github.com/sheldonl3/Moonlight_Config/blob/master/%E9%9D%99%E6%80%81.png)
在nat中对静态lan地址配置端口转发
![](https://github.com/sheldonl3/Moonlight_Config/blob/master/nat2.png)

### 2)路由器
路由器可以使用桥接模式，或者关闭防火墙，但是这样对原本的网络功能有较大的影响，不推荐。

所以首先主机绑定静态IP。这一步有的路由器不用配置，因为进行nat的时候可以直接绑定主机
![](https://github.com/sheldonl3/Moonlight_Config/blob/master/%E9%9D%99%E6%80%81ip.png)
对主机同样的端口配置nat，这样串流流量通路顺利打通
![](https://github.com/sheldonl3/Moonlight_Config/blob/master/nat.png)
使用![端口检测](https://www.canyouseeme.org/)工具可以检测是否配置成功（只需检测47984 47989，其他端口使用时才开放）


### 3）PC配置和移动端
和本地串流方式相同，无序做多余配置，GFE默认开启所有服务
最后使用连接外网的移动端，在moonlight内添加家庭的公网IP，会搜素到串流PC，添加后即可游戏

测试使用北京联通4G下行58Mbps，主机使用联通宽带，上行24Mbps，
可能是因为带宽限制，画面效果可以，但是经常会有声音卡顿的情况
