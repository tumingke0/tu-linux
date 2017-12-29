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
	








