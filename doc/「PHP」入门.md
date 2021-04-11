# 「PHP」入门

### 初始化php 配置php-fpm为默认配置文件
```bash
sudo cp /private/etc/php-fpm.conf.default /private/etc/php-fpm.conf
php-fpm --fpm-config /private/etc/php-fpm.conf
sudo vim /usr/local/etc/php-fpm.conf
# 修改error log file,pid file
error_log = /usr/local/var/log/php-fpm.log
pid = /usr/local/var/run/php-fpm.pid
```

### 配置mysql
```
brew install mysql
mysql.server start
mysql_secure_installation
Remove anonymous users? [Y/n]
(是否移出数据库的默认帐户，如果移出，那么在终端中直接输入mysql是会提示连接错误的)
Disallow root login remotely?
(是否禁止root的远程登录)
Remove test database and access to it?
删除测试数据库并访问它
Reload privilege tables now?
现在重新加载权限表？

# 启动sql
brew services start mysql
# 重启
brew services restart mysql
# 停止
brew services stop mysql
```

### apache配置
1. 修改apache配置文件
```bash
sudo vi /etc/apache2/httpd.conf
# ServerName localhost:80 注释去掉
# 开启 LoadModule
# 去掉 LoadModule php7_module libexec/apache2/libphp7.so 注释
# 开启 虚拟域名文件配置
# 去掉 Virtual hosts 下 Include /private/etc/apache2/extra/httpd-vhosts.conf 注释
```

code
2. 配置虚拟域名文件
```bash
# 打开虚拟域名配置文件
sudo vi /etc/apache2/extra/httpd-vhosts.conf
# 或 sudo vi /private/etc/apache2/extra/httpd-vhosts.conf
```

3. 重启服务器
```bash
sudo apachectl restart
brew services start mysql
```

### 项目部署
```bash
# 文件夹根目录 /Library/WebServer/Documents
# 软连接到 服务器文件夹 例: 项目路径/Users/lee/woke/svn/ErShouChe/code/php/ErShouChe
sudo ln -s /Users/lee/woke/svn/ErShouChe/code/php/ErShouChe /Library/WebServer/Documents/ErShouChe
sudo ln -s /Library/WebServer/Documents/ErShouChe
sudo chmod -R 777 /Users/lee/woke/svn/ErShouChe/code/php/ErShouChe
# 配置入口
sudo vi /etc/apache2/extra/httpd-vhosts.conf
# 修改host文件
/private/etc/hosts 
```
code
### Q&A
1. 报错：Permission denied
> 报错原因是文件夹权限不够,解决方法：
  `chmod -R 777 目录名`

2. mysql无法启动 “Warning:The /usr/local/mysql/data directory is not owned by the 'mysql' or '_mysql' ”
> sudo chown -R mysql /usr/local/mysql/data


3. 可视化软件登录报错：2059 - Authentication plugin 8.0后版本sql
>/～ mysql -uroot -p12345678  
/～ use mysql;  
/～ select user,plugin from user where user='root';  
/# 可以看到当前用户的加密方式为caching_sha2_password  
/～ alter user 'root'@'localhost' identified with mysql_native_password by '12345678';  
/# 将用户的加密方式改为mysql_native_password  
/～ flush privileges;  
/# 使权限配置项立即生效。  