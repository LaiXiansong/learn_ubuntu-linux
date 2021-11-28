# 外网连接实验室内网主机
在清华校园网下连接实验室的主机很容易实现，但是从外网想要控制实验室的主机还需要其他手段。

最简单的方式是通过一些商业的远程控制软件，甚至可以通过两个qq号远程控制，但是傻瓜式的方法并不能学习到什么东西（笑）。

主机不能被远程控制，根本的原因在于其没有一个公网的ip，从ipconfig直接查到的ip都是一个私网ip，是不能从网络上搜索到的，这就需要借助工具实现内网到公网的映射，即：**内网穿透**。

介绍通过一种特殊的手段实现内网穿透：云服务器 + frp + vnc viewer远程控制主机。
## 1 原理
以云服务器作为中介，将内网主机的端口映射到云服务器的外网端口，从而实现从外网端口访问，远程控制内网主机。

## 2 frp
frp是一款开源的快速的反向代理，能够使本地的服务穿过NAT及防火墙，暴露在网络上。
![frp原理](https://github.com/fatedier/frp/blob/dev/doc/pic/architecture.png "frp原理")

release及详细使用教程地址：https://github.com/fatedier/frp

下载时注意版本统一。

下载解压后的文件夹内包含以下几个部分：
1. systemd的文件夹（暂时用不到）
2. frpc(.exe)，客户端的启动程序
3. frps(.exe)，服务端的启动程序
4. frpc.ini，客户端的配置文件
5. frps.ini，服务端的配置程序
6. frpc.ini，客户端的配置文件，内容较全
7. frps.ini，服务端的配置文件，内容较全
8. LICENSE

服务端只需要保留frps及fros.ini文件，客户端只用保留了frpc及frpc.ini文件。

## 3 云服务器
云服务器相当于远程主机，常见的云服务器厂商，国内有：阿里云、腾讯云、华为云等。国外也有服务器，但是服务器的速度与地域有关。
以阿里云为例：
1. 首先在阿里云官网购买了服务器，公网ip为：39.108.186.48
2. 系统安装为ubuntu20.04 64位 server版
3. cpu单核
4. 2G内存

### 3.1 云服务器搭建frp server
保留服务器中frp文件夹的服务端相关文件，打开配置文件进行修改，简单的配置如下（其他）：

    [common]
    bind_port = 7000 # 服务端的默认端口，与客户端建立联系相关
    token = 300018 # 服务端授权码，需要与客户端保持一致
    
    # 监视控制台相关，服务器启动后，在浏览器中输入：服务器的公网ip:端口，能够进入到监视控制台，查看代理的详细信息
    dashboard_port = 55500 # 监视控制台的网址端口
    dashboard_user = laixiansong # 监视控制台的用户名
    dashboard_pwd = 300018 # 监视控制台的用户密码
    
配置完成之后，运行以下命令可以启动服务端服务。

    ./frps -c ./frps.ini
windows计算机可以在cmd运行以下命令：

    frps -c frps.ini
## 4 内网主机
在内网中，需要被控制的主机为客户端。
同样，客户端的frp只保留客户端相关的文件。配置参考：

    [common]
    server_addr = x.x.x.x # 服务器的公网ip地址，与服务端对应
    server_port = 7000 bind_port = 7000 # 服务端的默认端口，与客户端建立联系相关
    token = 300018 # 与服务端的配置token一致
    
    # 配置ssh服务
    [ssh] # 中括号中的内容没有关系，只起到一个代理名字的作用
    type = tcp # 连接协议类型：tcp
    local_ip = 127.0.0.1 # 本地ip
    local_port = 22 # 需要暴露到公网的端口，ssh的默认端口为22
    remote_port = 2222 # 服务端监听的端口，客户端需要暴露的端口映射到服务器的端口
    
    [ssh2] # 可以添加其他服务
    ...
    
配置好服务器之后，通过类似的命令启动服务：

    ./frpc -c ./frpc.ini
windows计算机可以在cmd运行以下命令：

    frpc -c frpc.ini

## 5 防火墙开放端口
默认情况下防火墙都是没有开的，ubuntu系统可以通过ufw相关命令控制防火墙开启、关闭以及端口：

    ufw enable # 启动防火墙
    ufw status # 查看防火墙状态
    ufw disable # 禁用防火墙
    ufw allow 80 # 允许端口
    ufw deny 80 # 拒绝端口
    ufw delete allow http # 删除允许端口
    ufw delete deny 21 # 删除拒绝端口
    ufw reset # 端口重启
    ...

## 6 阿里云控制台开放端口
**在自己配置服务器远程控制的时候遇到的一个最坑的问题，大多数博客都没有强调这一点**

打开阿里云的控制台，找到安全组，点开配置规则：

默认情况下端口3389和22是开启的，需要增加服务器开启的端口通过界面交互添加即可。


## 7 ssh访问内网机器的方法
假设用户名为root，访问内网机器的linux命令为：

    ssh -oPort=2222 test@x.x.x.x # 对应的-Oprot为在客户端配置的remote_port， @后为服务器的公网ip

## 8 vnc viewer远程控制内网机器
### 8.1 客户端安装vnc服务
在局域网内已经安装好了vnc的服务端：tightvncserver以及x11vnc，如果没有经过这步需要提前安装：

    sudo apt install tightvncserver   
    sudo apt install x11vnc
然后运行以下命令启动vnc服务：
    
    vncserver
### 8.2 控制端下载vnc viewer软件并连接
下载安装vnc viewer并连接，输入以下地址：

服务器公网ip地址:remote_port

连接完成！


## 9 配置后台运行及开机启动
将文件复制到系统文件夹下，可以通过systemctl通过命令实现后台运行、开机自启等。

* 复制文件

      sudo mkdir -p /etc/frp
      sudo cp frps.ini /etc/frp
      sudo cp frps /usr/bin
      sudo cp systemd/frps.service /usr/lib/systemd/system/
* 开机自启

      sudo systemctl enable frps
* 取消开机自启

      sudo systemctl disable frps
* 后台运行

      sudo systemctl start frps
* 结束后台运行

      sudo systemctl start frps
