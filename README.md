# Clash Tracing Dashboard

An example of a clash tracing exporter API.

### Screenshot

![screenshot](./screenshot/screenshot.jpg)

### How to use

1. modify `docker-compose.yaml` and start (`docker-compose up -d`)
2. setup Grafana
3. import `grafana.json` to Grafana


debian 10安装详细说明

	1. 安装docker
		a. 由于 apt 源使用 HTTPS 以确保软件下载过程中不被篡改。首先需要添加使用 HTTPS 传输的软件包以及 CA 证书
		b. sudo apt-get update
		sudo apt-get install \
		apt-transport-https \
		ca-certificates \
		curl \
		gnupg-agent \
		lsb-release \
		software-properties-common
		c. 为了确认所下载软件包的合法性，需要添加软件源的 GPG 密钥
		 curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
		d. 向 sources.list 中添加 Docker 软件源
		# 官方源
		$ sudo add-apt-repository \
		     "deb [arch=amd64] https://download.docker.com/linux/debian \
		     $(lsb_release -cs) \
		     stable"
		e. 安装docker
		$ sudo apt-get update
		$ sudo apt-get install docker-ce docker-ce-cli containerd.io
		
	2. 系统关联python 3.7     #https://www.quyu.net/info/1549.html
		a. 先列出可用python版本
		update-alternatives --list python
		出现错误：update-alternatives: error: no alternatives for python
		如果出现以上所示的错误信息，则表示 Python 的替代版本尚未被 update-alternatives 命令识别。想解决这个问题，我们需要更新一下替代列表，将 python2.7 和 python3.7 放入其  中，执行以下命令：
		update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
		update-alternatives: using /usr/bin/python2.7 to provide /usr/bin/python (python) in auto mode
		update-alternatives --install /usr/bin/python python /usr/bin/python3.5 2
		update-alternatives: using /usr/bin/python3.5 to provide /usr/bin/python (python) in auto mode
		注意：命令最后面的数字是序号
		b. python --version 检查当前python版本
		
	3. 安装pip
		a. curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py   # 下载安装脚本
		b. sudo python get-pip.py    # 运行安装脚本
		注意：用哪个版本的 Python 运行安装脚本，pip 就被关联到哪个版本，如果是 Python3 则执行以下命令
		sudo python3 get-pip.py    # 运行安装脚本
		# 可能报错
		#  ModuleNotFoundError: No module named 'distutils.util'
		sudo apt-get install python3-distutils  #安装依赖
		c. pip install --upgrade pip    #升级pip
		d. 显示版本和路径
		pip --version
		
	4. pip 安装 docker-compose
		a. pip3 install docker-compose
		
	5. 修改docker-compose.yaml
		a. CLASH_HOST: '10.10.10.3:9090'       # clash IP以及端口
		b. CLASH_TOKEN: '123456'          #web-UI密码
		
	6. 启动：docker-compose up-d
	
	7. grafana后台地址：
		a. Clash IP：3000
		b. 添加数据库 influxdb
		所有信息按docker-compoes.yaml填写
		
	8. 导入json文件
