# chapter 8
## 8.1 UNIX变量
变量是将信息从shell传递到程序的方法。

程序从环境中找到特定的变量，找到了就会用这些储存的值。有些值是系统设置的，有些是用户自己设置的。

标准的UNIX变量分为两类：
1. 环境变量：登录会话后设置的变量在会话区间有效，大写。
2. shell变量：仅适用于当前的shell实例，设置短期工作条件，小写。
## 8.2 环境变量
环境变量举例：
* OSTYPE：使用的操作系统
* USER：登陆名
* HOME：home文件夹的路径名
* HOST：使用的计算机的名
* ARCH：计算机处理器的名字
* DISPLAY：显示X窗口的计算机屏幕的名字
* PRINTER：默认打印机的名字
* PATH：shell找命令的目录
### 8.2.1 找到这些变量的当前值
通过`srtenv`命令能够设置变量，显示变量额的值：
    printenv | less
## 8.3 shell变量

history就是shell变量的一个例子，记录之前用过的命令。

### 8.3.1 shell变量的当前值
通过`set`命令可以查找当前shell变量的值。

### 8.2.1 PATH和path
仅大小写不同的环境变量和shell变量通常是相互独立的。

更改shell变量home，user和term的值的时候，HOME，USER和TERM的值会一起变化，但是改变环境变量时，shell变量没有影响。

path和PATH总是一起改变。

## 8.4 使用和设置变量
每次登录一个UNIX账户，系统从home目录找到初始化文件，用来设置工作环境，C和TCshell用两个文件：**.login**和**.cshrc**。
* **.login**设置应用于整个会话的条件，并执行仅在登录时的相关操作。
* **.cshrc**设置条件并执行特定于shell及其每次调用的操作。

## 8.5 在.cshrc文件中设置shell变量
改变history列表中保存的shell命令数量，需要设置shell变量history。默认情况下为100。
```
set history = 200
echo $history # 检查
```
然而，这样设置的变量的生命周期只在当前的shell。要设置永久的值，需要把设置命令加在.cshrc文件中。

打开编辑.cshrc文件：
```
nedit ~/.cshrc
```
加入**set history=200**这个命令。

保存并强制shell重新读取他的.cshrc文件：
```
source .cshrc
echo $history # 检查
```
## 8.6 设置path
"command:Command not found"，代表这个命令不存在整个系统，或者不再你的path中。

比如，要运行`~/units174/bin/units`，需要这个目录在你的path中。

在path结尾加入新的环境变量：
```
set path = ($path ~/units174/bin)
```
需要变量永久设置，同样也要添加到./cshrc中
