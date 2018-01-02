# 文件同步命令：
    scp
    rsync
    
## scp
### 语法：
` scp [OPTION] [[user@]host1:]file1 … [[user@]host2:]file2 `  

` scp [参数] [原路径] [目标路径] `

### 参数详解：  
-1  强制scp命令使用协议ssh1  

-2  强制scp命令使用协议ssh2  

-4  强制scp命令只使用IPv4寻址  

-6  强制scp命令只使用IPv6寻址  

-B  使用批处理模式（传输过程中不询问传输口令或短语）  

-C  允许压缩。（将-C标志传递给ssh，从而打开压缩功能）  

-p 保留原文件的修改时间，访问时间和访问权限。  

-q  不显示传输进度条。  

-r  递归复制整个目录。  

-v 详细方式显示输出。scp和ssh(1)会显示出整个过程的调试信息。这些信息用于调试连接，验证和配置问题。   

-c cipher  以cipher将数据传输进行加密，这个选项将直接传递给ssh。   

-F ssh_config  指定一个替代的ssh配置文件，此参数直接传递给ssh。  

-i identity_file  从指定文件中读取传输时使用的密钥文件，此参数直接传递给ssh。    

-l limit  限定用户所能使用的带宽，以Kbit/s为单位。     

-o ssh_option  如果习惯于使用ssh_config(5)中的参数传递方式，   

-P port  注意是大写的P, port是指定数据传输用到的端口号   

-S program  指定加密传输时所使用的程序。此程序必须能够理解ssh(1)的选项。  

* 用的最多的，可能就是-r 了，复制目录的时候，要用到   

### 语法格式：  
* 因为之前一篇文章已经介绍了，如何打通两个服务器，这里就默认不需要输入密码，直接执行了  

(1) 复制文件：   
` scp local_file remote_username@remote_ip:remote_file `
有多种写法，这里只介绍常用或者说我喜欢的 ^_^ 的格式！  
  
(2) 复制目录：
` scp -r local_folder remote_username@remote_ip:remote_folder  `
可以看到跟复制文件的区别就是多了个参数-r，递归复制，其实复制文件也是可以用-r的，为了简单，这里只记加参数-r即可！

### 语法格式：  
#### 从远程服务器复制到本地服务器
` scp -r root@192.168.1.110:/home/shell/arr.sh /home/shell/ `  

把192.168.1.110的服务器上的 arr.sh  复制到本地，并且保存到 /home/shell/arr.sh


#### 从本地服务器复制到远程服务器
` scp -r /home/shell/ root@192.168.1.110:/home/ `
把本地的服务器上shell 目录复制到192.168.1.110服务器，并且保存到 /home 下，那么就有了在 .1.110 上的/home下就有个目录叫 shell
  
  

## rsync  
参考：
` http://roclinux.cn/?p=2643 `  
具体可参考上面的链接，我这里只简单介绍常用的命令：  
### 语法格式：  
` rsync -avH /home/shell/arr.sh root@192.168.1.110:/home/shell `

把本地的 arr.sh 复制到 远程的 /home/shell/  下面  
可以发现，rsync 和 scp 在语法格式上非常相近，但是其执行复制的机制还是有区别的，对于 rsync 只需要记住 -av H 即可，好记，好用！











