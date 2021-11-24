# chaper 2 file operation

## 2.1 复制文件
将某个文件复制到当前目录，保持文件名。记住，.代表当前目录。

    cp 'file_directory/file' .

## 2.2 移动文件
移动一个文件到另一个文件，当文件位置不变但名字变时，相当于给文件重命名。

    mv 'filename1' 'filename2'

## 2.3 移除文件和文件夹
移除文件:
    
    rm 'filename'
移除文件夹：

    rmdir 'directory_name'

## 2.4 展示文件内容
清屏：

    clear
简单展示文件内容：

    cat 'fileaname'
进入文件浏览模式，可翻页：

    less 'filename'
    more 'filename'
more 与 less 功能类似:
* 空格下一页
* b上一页
* 支持翻页、搜索

但是也存在一些区别：
* less 不必阅读整个文件，所以加载更快
* less 退出后不会留下显示内容
* less 更随意一些，可跳转

另外，还有一个功能更为强大的命令most，在此不详述。

显示文件的前面几行，可以用:

    head -'number' 'file_name'
显示前‘nember’行，默认是10行。

同样类似的还有后几行：

    tail -'number' 'file_name'

## 查找内容：
简单的查找方式是使用less,当在less浏览模式下时，输入：

    /'search_content'
就可以找到要找的内容高亮光显示，同时按下n可以转向下一个查找到的内容。

还有一种查找命令是：
    
    grep 'search_content' 'filename'
这个命令是大小写敏感的，配合以下选项，可以获得不同的效果：

    grep -i 'search_content' 'filename'    # 大小写不敏感
    grep -v 'search_content' 'filename'    # 反转，显示不匹配的对象
    grep -c 'search_content' 'filename'    # 只显示匹配的行数
多个选项可以结合：

    grep -ivc 'search_content' 'filename'    # 选项同时
显示文件的词数或行数：

    wc 'filename' # 显示词数和行数
    wc -w 'filename' # 显示词数
    wc -l 'filename' # 显示行数
