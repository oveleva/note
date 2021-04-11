# 「梯子」vps
```bash
ssh -i "evanlee.pem" ec2-user@ec2-13-112-199-31.ap-northeast-1.compute.amazonaws.com
ssh -i "evanlee.pem" ec2-user@ec2-54-92-6-188.ap-northeast-1.compute.amazonaws.com
# 退出
logout
```

### Q&A

1. 公钥过于开放问题解决：
```
# error
Permissions 0644 for '/Users/lee/evan.pem' are too open.
# 解决方案
sudo chmod 0644 /Users/lee/evan.pem
```

```bash
# 安装配置shadowsocks
# Debian / Ubuntu:
apt-get install python-pip
pip install shadowsocks
# CentOS:
yum install python-setuptools && easy_install pip
pip install shadowsocks
# 获取软连接实际路径
ls -al python3
# 创建 shadowsocks 目录
mkdir /etc/shadowsocks
# 创建并编辑我们的配置文件
vim /etc/shadowsocks/config.json
{
  # 配置服务器 ip，这里填写 0.0.0.0
  "server":"0.0.0.0",
  # 配置端口号及各自的密码
  # 这里我用的多用户配置，大家也可以采用单用户配置
  # 端口号如果不懂可以选择跟我相同的，密码修改为自己想设置的密码就好
  "port_password":{
       "20610":"MII**********QEA"
       },
  # 超时时间 这个不用修改
  "timeout":300,
  # 加密算法
  "method":"aes-256-cfb",
  # true 或者 false 开启后能降低延迟
  "fast_open":false
}
# 启动
sudo /usr/local/bin/ssserver -c /etc/shadowsocks/config.json -d start
sudo /usr/local/bin/ssserver -c  -d start
# 停止
sudo /usr/local/bin/ssserver -d stop
# 重新启动
sudo /usr/local/bin/ssserver -c /etc/shadowsocks/config.json -d restart
# 查看日志
sudo less /var/log/shadowsocks.log
```

# ShadowSocks
```
#有网友做了个服务器端一键安装ShadowSocks的脚本，使用root用户登录，运行以下命令： 
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev.sh
chmod +x shadowsocks-libev.sh
./shadowsocks-libev.sh 2>&1 | tee shadowsocks-libev.log
安装完成后，得到的服务器端口：8989，客户端端口：1080，密码为自己设定的密码。
卸载方法：使用 root 用户登录，运行以下命令：
./shadowsocks-libev.sh uninstall
安装完成后即已后台启动 shadowsocks ，运行：
ps -ef | grep ss-server | grep -v ps | grep -v grep
可以查看进程是否存在。此脚本安装完成后，会将 shadowsocks-libev 加入开机自启动。
使用命令：
启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
查看状态：/etc/init.d/shadowsocks status
卸载：./shadowsocks.sh uninstall
修改端口和加密方式：编辑修改配置文件 /etc/shadowsocks-libev/config.json

上述创建的ss服务，只有一个（账号）密码，只能供一个人用，或者说，如果多个人使用，则使用的是同一个（账号）密码，显得很不方便和不安全。
如果想要多个用户每人有不同的账号（密码），则可以：用shadowsocks-libev实现多账号/多用户
新建另外一个配置文件，比如：
/etc/shadowsocks-libev/config1.json
内容和之前一致，只是端口号server_port和密码password改了一下即可：
{
    "server": "0.0.0.0",
    "server_port": 21501,
    "password": "passowrd2",
    "method": "aes-256-cfb",
    "timeout": 300,
    "mode": "tcp_and_udp"
}
注意: 端口号不要和系统中其他服务的端口号冲突了。
另外再去用：
setsid ss-server -c /etc/shadowsocks-libev/config1.json -u
启用新端口对应的ss服务。
```