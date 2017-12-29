# 甲服务器：
## 使用ssh-keygen在 （"甲" ）服务器上生成 公钥私钥（即 RSA加密）
	执行：ssh-keygen 
（1）<br/>
可自行输入保存路径如：<br/>
	  /home/.ssh/rsa-key <br/>
	（ 注意: "/home/.ssh/"是路径，"rsa-key"是公钥私钥的名称，即会在 "/home/.ssh" 下生成 "rsa-key" 和 "rsa-key.pub" )<br/>
默认路径：<br/>
	centos默认保存到 "/root/.ssh/id_rsa" 和 "/root/.ssh/id_rsa.pub"
<br/>
（2）输入密码，类似开机密码，可不输入，然后一路enter下去
<br/>
（3）完了之后，着重注意保存路径及其名称即可！

# 乙服务器：
## 然后就是使用了，把新生成的id_rsa.pub的内容公钥放到你想ssh连接的（"乙"）服务器的认证列表里
（1）认证列表的路径：
		```
		grep AuthorizedKeysFile /etc/ssh/sshd_config 
		```
	得到：
		```
		.ssh/authorized_keys  
		```
	即该服务器的认证列表的路径是  ~/.ssh/authorized_keys

（2）然后把上面在第一个#步骤（甲服务器）生成的 id_rsa.pub 打开，复制里面的信息，
	执行 <br/>
		``` 
		vim ~/.ssh/authorized_keys
		```<br/>
	把复制的pub信息，粘贴至这个文件即可！

# 到甲服务器执行
	ssh root@127.0.0.1
  或者指定端口号：<br/>
	ssh root@127.0.0.1 -p 22 -i ~/.ssh/id_rsa

	
# 可禁用密码登录
	vim /etc/ssh/sshd_config
	把 PasswordAuthentication  改为 no 即可
	

# 打通后， 可使用 scp 复制文件
	scp [参数] [原路径] [目标路径]
	
	```
	-1 强制scp命令使用协议ssh1
	-2 强制scp命令使用协议ssh2
	-4 强制scp命令只使用IPv4寻址
	-6 强制scp命令只使用IPv6寻址
	-B 使用批处理模式（传输过程中不询问传输口令或短语）
	-C 允许压缩。（将-C标志传递给ssh，从而打开压缩功能）
	-p 留原文件的修改时间，访问时间和访问权限。
	-q 不显示传输进度条。
	-r 递归复制整个目录。
	-v 详细方式显示输出。scp和ssh(1)会显示出整个过程的调试信息。这些信息用于调试连接，验证和配置问题。
	-c cipher 以cipher将数据传输进行加密，这个选项将直接传递给ssh。
	-F ssh_config 指定一个替代的ssh配置文件，此参数直接传递给ssh。
	-i identity_file 从指定文件中读取传输时使用的密钥文件，此参数直接传递给ssh。
	-l limit 限定用户所能使用的带宽，以Kbit/s为单位。
	-o ssh_option 如果习惯于使用ssh_config(5)中的参数传递方式，
	-P port 注意是大写的P, port是指定数据传输用到的端口号
	-S program 指定加密传输时所使用的程序。此程序必须能够理解ssh(1)的选项。
	```
	
	1. 从本地服务器复制到远程服务器
	scp -r /opt/soft/demo.tar root@10.6.159.147:/opt/soft/scptest
	scp -r /opt/soft/test root@10.6.159.147:/opt/soft/scptest

	2. 从远程复制到本地
	scp -r root@10.6.159.147:/opt/soft/demo.tar /opt/soft/


