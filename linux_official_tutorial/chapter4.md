# Chapter 4
## 4.1 wildcards *
* " * " 这个符号是一种wildcard，用来匹配有相同字符串片段的文件、文件夹名，具体用法：

      ls list* # 列出当前目录所有“list...”的文件/文件夹名
      ls *list # 列出当前目录所有“...list”的文件/文件夹名
* " ？ " 这个符号这种wildcard用来匹配有相同字符串片段的文件、文件夹名，并且只多一个字符，具体用法：
      
      ls list? # list1, list2这样的match，但是list10这样的旧不行了
## 4.2 帮助
通过命令查找命令的帮助：
    
    man 'command'
若不清楚命令的具体名字：

    apropos 'word'
查找在帮助页头文件中有word这个关键词的命令。
