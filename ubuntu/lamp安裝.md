####  1. 安裝 Apache2       
		
```
$ sudo apt install apache2
```        
    
#### 2. 調整防火牆以允許Web通信

檢查UFW是否有 Apache的應用程式配置文件	
```
$ sudo ufw app list
```
	
```
Output	
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH
```
	
如果查看 Apache Full配置文件, 顯示啟用到端口80和443流量：	
```
sudo ufw app info "Apache Full"
```
	
```
Output
Profile: Apache Full
Title: Web Server (HTTP,HTTPS)
Description: Apache v2 is the next generation of the omnipresent Apache web
server.

Ports:
  80,443/tcp
```
	
允許此配置文件傳入http和https流量：	
```
sudo ufw allow in "Apache Full"
```

#### 3. 安裝mysql	
	
```
sudo apt install mysql-server
```
	
完成後運行互動式安裝腳本	
```
sudo mysql_secure_installation
```
	
#### 4. 安裝php	
	
```
sudo apt install php libapache2-mod-php php-mysql
```

重啟Apache	
```
sudo systemctl restart apache2
```
	
#### 5. 安裝phpmyadmin	
	
```
sudo apt-get install phpmyadmin
```
	
將phpmyadmin軟連結到Apache的根目ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

錄底下	
	
```
sudo  ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

```
	
完成安裝


#### 6. 解決phpmyadmin權限問題 (#1698)
	
連結到數據庫	

```
sudo mysql -u root -p
```
	
創建一個帳號來賦予系統權限	
```mysql
CREATE USER 'root_sql'@'localhost' IDENTIFIED BY 'yourpasswd';
GRANT ALL PRIVILEGES ON *.* TO 'root_sql'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

更新phpmyadmin配置	
```
sudo /etc/dbconfig-common/phpmyadmin.conf

```

修改配置文件內容	
```
# dbc_dbuser: database user
#       the name of the user who we will use to connect to the database.
dbc_dbuser='root_sql'

# dbc_dbpass: database user password
#       the password to use with the above username when connecting
#       to a database, if one is required
dbc_dbpass='yourpasswd'
```


- - - 
參考資料 ： https://www.howtoing.com/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04           	
參考資料 ： https://blog.csdn.net/teddy_dewei_lu/article/details/79659013
