# How to install vscode in ubuntu20.04
在微软官网有vscode的apt源仓库。
1. 更新软件包索引并安装依赖软件：

       sudo apt update
       sudo snap install --classic code

2. 使用wgent命令插入Microsoft GPG key:

       wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
3. 启动源仓库：

       sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
4. 安装vscode软件包：

       sudo apt install code
5. 完成
