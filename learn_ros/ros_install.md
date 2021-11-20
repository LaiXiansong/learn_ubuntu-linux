# ubuutu20.04如何安装ros
这是关于如何安装ros的记录。   
值得注意的是，在安装ros时要考虑安装ros的ubuntu版本，目前ros最新的版本是noetic，对应的ubuntu版本是20.04。如果版本不对，可能会出现install时找不到release的情况。   
参考官方安装文档: http://wiki.ros.org/noetic/Installation/Ubuntu   
### 1.1 配置仓库
软件&更新设置 允许：‘restricted’,‘universe’,‘multiverse’
### 1.2 设置源列表
设置电脑接受来自package.ros.org的软件   
（如果没有科学上网可以考虑镜像）   
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'   
### 1.3 设置密钥
网上找一个密钥
$ sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
### 1.4 安装
$ sudo apt install ros-noetic-desktop-full: 安装完全版（推荐）   
其他安装模式见官方教程   
需要安装其他包时，可以随时通过以下命令安装PACKAGE:   
sudo apt install ros-noetic-PACKAGE
### 1.5 环境设置
$ echo "source /opt/ros/noetic/setup.zsh" >> ~/.zshrc   
$ source ~/.zshrc
### 1.6 依赖项安装
$ sudo apt install python3-rosdep   
然后进行初始化及更新
$ sudo rosdep init   
$ rosdep update   
注意 update 的时候最好能有一个科学上网的手段
### 1.7 安装成功及测试
new terminal   
$ rosrun turtlesim turtlesim_node   
出现小乌龟   
new terminal
$ rosrun turtlesim turtle_teleop_key   
键盘控制小乌龟移动
