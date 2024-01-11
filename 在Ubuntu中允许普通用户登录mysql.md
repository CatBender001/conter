# 在Ubuntu中允许普通用户登录mysql

## 在Ubuntu中，普通用户默认情况下无法登录MySQL。这是因为MySQL的root用户默认只能从本地主机进行连接，而普通用户没有足够的权限进行远程连接。

如果您想要允许普通用户登录MySQL，可以尝试以下步骤：

1. 创建一个新的MySQL用户并授权。您可以使用以下命令在MySQL中创建一个新用户：

```
sudo mysql -u root -p
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
quit;
```

请将上述命令中的"newuser"和"password"替换为您想要设置的新用户名和密码。

2. 修改MySQL的配置文件/etc/mysql/mysql.conf.d/mysqld.cnf，允许远程连接。您可以使用以下命令打开mysqld.cnf文件进行编辑：

```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

在mysqld.cnf文件中，找到以下行并确保它们没有被注释掉：

```
#bind-address = 127.0.0.1
```

如果这一行被注释掉了，请将其取消注释并保存文件。然后，使用以下命令重启MySQL服务：

```
sudo systemctl restart mysql
```

3. 现在，您可以使用新创建的MySQL用户从远程主机登录MySQL。请注意，为了安全起见，建议您仅允许特定IP地址的主机进行远程连接。您可以使用以下命令授权特定IP地址的主机：

```
sudo mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'your_remote_host_ip' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
quit;
```

请将上述命令中的"your_remote_host_ip"替换为您想要授权的远程主机的IP地址。