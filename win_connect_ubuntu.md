# 这是关于如何通过WinSCP建立windows主机和ubuntu主机之间的文件传输通信的记录
## 1 下载WinSCP
## 2 打开，新建会话
## 3 通过查找ubuntu主机的ip
### 3.1 具体操作：
首先需要sudo apt-get install ssh 安装ssh的服务端   
然后sudo apt install net-tools 安装网络工具（查询ip要用到）   
再通过ifconfig命令查找本机的ip地址
## 4 WinSCP 输入主机名、用户名、密码，连接！
