# chapter 5
## 5.1 文件系统安全、权限
通过ls命令添加参数-l可以查看到目录下的文件细节：
    
    ls -l 
每一行输出文件的内容：

![file1](https://user-images.githubusercontent.com/53077787/143806461-fb66bd2b-d472-4710-beb4-75a71811d370.gif)

-rwxrw-r-- 1 ee51ab beng95 2450 Sept29 11:52 file1

* 第一部分有10个符号位，其中第一个符号用来标识文件(-)还是文件夹(d)。
* 剩下9个符号按3 * 3分为3个部分的权限：1. owner 2. belong group 3. all。而字符含义：1. r(可读) 2. w(可写) 3. x(可执行)
## 5.2 改变权限
chom命令用来改变文件的权限，具体参数：

| symbol | Meaning |
|----|----|
| u | user |
| g | group |
| a | all |
| r | read |
| w | write |
| x | excute, access |
| + | add |
| - | deny|

e.g. 取消 biglist 这个文件的group及owner的所有权限：

    chmod go-rwx biglist
## 5.3 进程和任务 Processes & Jobs
查看当前进程：

    ps

### 5.3.1 后台执行进程
一般情况下，shell在进程结束之前都不会返回新的命令提示符，在这个进程进行时，想要执行其他命令，可以将当前的进程放到后台执行：

在结尾加上 & ：
 
    sleep 10 & # 等待10秒钟再继续
同时，在命令开始执行时会在shell中打印出后台进程的唯一标志符PID

    [（序号）] xxxx（进程数字）
如果进程已经开始，可以转到后台（backgrounding）：

    bg
## 5.4 列出暂停和后台的进程
列出进程：

    jobs
    
    [1] Suspended sleep 1000
    [2] Running netscape
    [3] Running matlab
重新开始一个暂停的任务（foreground）：

    fg %jobnumber
杀死任务：

    kill %jobnumber
在ps命令下杀死进程：

    kill jobPID
如果进程拒绝被杀死，还可以：

    kill -9 jobPID
强制杀死进程。
