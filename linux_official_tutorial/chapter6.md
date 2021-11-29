# chapter 6

## 其他常用Unix命令
### 6.1 quota
* 查看文件服务器的空间剩余：

	  df .
* 每个子目录中的千字节数，用来看哪个子目录占用了最多的空间：

	  du -s * # '-s' 代表short，'*'代表all
* 文件压缩

      gzip filename # 压缩文件为gz格式
      gunzip filename # 解gz压缩文件
* 读取gz压缩文件

      zcat filename
      cat filename | less # pipe显示
     
* 文件分类

      file *
* 比较不同

      diff fi le1 file2
* 找文件

      find . -name "*.txt" -print
