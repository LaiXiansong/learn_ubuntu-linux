# how to reinstall the broswer
## uinstall: firefox
    
    dpkg -l | grep firefox 

* 找到火狐浏览器的关联包
    
      sudo dpkg -p firefox firefox-locale-en firefox-locale-zh-hans # 根据关联包卸载

##  install： chrome
* 官网下载安装包：

      wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
* 安装：

      sudo apt install ./google-chrome-stable_current_amd64.deb #
* 可选，删除安装包

      rm google-chrome-stable_current_amd64.deb
