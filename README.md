# 创建谷歌云instance
> 将VPC网络中外部IP地址改为静态；防火墙规则default-allow-http和default-allow-http增加端口tcp:5000即jupyter端口
并增加规则jupyer: 关键字段如下： 应用于所有实例 、IP 地址范围 0.0.0.0/0 、协议和端口 tcp:5000
# 连接谷歌云instance
`ssh-keygen -t rsa -f ~/.ssh/(用户名)-ssh-key -C (用户名）`
> 将.ssh/(用户名)-ssh-key.pub 中的内容复制粘贴到谷歌云实例的ssh信息,然后本地终端登录
`ssh -i .ssh/(用户名)-ssh-key (用户名)@(实例IP)` 
> ssh-copy-id -i ~/.ssh/your-key-name.pub root@35.189.188.31
ssh-add ~/.ssh/your-key-name
当用旧的ssh key 登录主机 需要更改主机rsa 执行 ssh-keygen -f "/home/senmonster/.ssh/known_hosts" -R 104.199.246.91(new host ip)
