# 创建谷歌云instance
> 将VPC网络中外部IP地址改为静态；防火墙规则default-allow-http和default-allow-http增加端口tcp:5000即jupyter端口
并增加规则jupyer: 关键字段如下： 应用于所有实例 、IP 地址范围 0.0.0.0/0 、协议和端口 tcp:5000
# 连接谷歌云instance
`ssh-keygen -t rsa -f ~/.ssh/(用户名)-ssh-key -C (用户名）`
> 将.ssh/(用户名)-ssh-key.pub 中的内容复制粘贴到谷歌云实例的ssh信息,然后本地终端登录

`ssh -i .ssh/(用户名)-ssh-key (用户名)@(实例IP)`
### 附加说明
`ssh-copy-id -i ~/.ssh/your-key-name.pub 用户名@35.189.188.31` 

`ssh-add ~/.ssh/your-key-name` 

当用旧的ssh key 登录主机 需要更改主机rsa 执行 

`ssh-keygen -f "/home/senmonster/.ssh/known_hosts" -R 104.199.246.91(new host ip)`

# 机器学习环境配置
```
wget http://repo.continuum.io/archive/Anaconda3-5.0.0-Linux-x86_64.sh  && bash ./Anaconda3-5.0.0-Linux-x86_64.sh
```
安装包完成后 
`source ~/.bashrc`
# 配置jupyter 后端登录
`jupyter notebook --generate-config && vim ~/.jupyter/jupyter_notebook_config.py`
insert:
c = get_config()
c.NotebookApp.ip = '0.0.0.0'
c.NotebookApp.notebook_dir = u'/home/topppyang/'
c.NotebookApp.open_browser = False
c.NotebookApp.password = u'sha1:9c648d04c827:a0578e432ba863eba2932f9a20b7f944fd8f2453'
c.NotebookApp.password_required = True
c.NotebookApp.port = 5000

# 安装jupyter extension and jupyter themes and import_ipynb 
```
pip install jupyter_contrib_nbextensions && jupyter contrib nbextension install --user && pip install --ignore-installed jupyterthemes && jt -T -N -cellw 85% -t gruvboxd && pip install import_ipynb && jupyter nbextension enable collapsible_headings/main && jupyter nbextension enable codefolding/main && jupyter nbextension enable codefolding/firstline-fold && jupyter nbextension enable varInspector/main && jupyter nbextension enable hide_input/main && jupyter nbextension enable splitcell/splitcell
```
> 生效指定扩展功能，说明：jupyter kernel 下 import sys; sys.executable 得到比如 '/home/senmonster/anaconda3/bin/python'
那就 cd /home/senmonster/anaconda3/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions
该目录下的文件夹为扩展名，进入扩展名下的js文件名为以下命令/的后半部分

若修改主题后导致print打印不全，则：
cd ~/.jupyter/custom &&vim custom.css
命令模式下输入/ 查找 div.output_area
再i进入编辑模式 增加
div.output_area {
display: -webkit-box;
padding: 13px;
}

# cell 多输出 以及 auto reaload
`vim ~/.ipython/profile_default/ipython_config.py`
insert:
c = get_config()
c.InteractiveShell.ast_node_interactivity = "all"
c.InteractiveShellApp.exec_lines = ['%autoreload 2']
c.InteractiveShellApp.extensions = ['autoreload']
c.TerminalInteractiveShell.autoindent = False
source ~/.ipython/profile_default/ipython_config.py



'/opt/conda/bin/python' -m conda install pkname 安装包到指定环境（路径由sys.executable得到）
top 10 largest directories
du -a / | sort -n -r | head -n 10
