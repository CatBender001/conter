在Ubuntu中安装好hive后，需要安装并配置MySQL，使MySQL数据库作为hive的元数据。以下是具体的操作步骤：

1. 安装MySQL

   在终端中输入以下命令来安装MySQL：

   ```
   sudo apt-get update
   sudo apt-get install mysql-server
   ```

   安装过程中会提示您设置MySQL的root用户密码，请根据提示进行设置。

2. 创建hive元数据数据库

   在终端中输入以下命令来登录MySQL：

   ```
   mysql -u root -p
   ```

   然后输入您设置的root用户密码以登录MySQL。

   接着，在MySQL命令行中输入以下命令来创建hive元数据数据库：

   ```
   CREATE DATABASE hive_metastore;
   ```

3. 创建hive元数据用户

   在MySQL命令行中输入以下命令来创建hive元数据用户：

   ```
   CREATE USER 'hiveuser'@'localhost' IDENTIFIED BY 'password';
   ```

   其中，'hiveuser'是您要创建的用户名，'password'是该用户的密码。

4. 授权hive元数据用户

   在MySQL命令行中输入以下命令来授权hive元数据用户对hive元数据数据库的访问权限：

   ```
   GRANT ALL PRIVILEGES ON hive_metastore.* TO 'hiveuser'@'localhost';
   ```

5. 配置hive-site.xml文件

   打开hive-site.xml文件，并添加以下配置：

   ```
   <property>
     <name>javax.jdo.option.ConnectionURL</name>
     <value>jdbc:mysql://localhost/hive_metastore?createDatabaseIfNotExist=true</value>
   </property>
   <property>
     <name>javax.jdo.option.ConnectionDriverName</name>
     <value>com.mysql.jdbc.Driver</value>
   </property>
   <property>
     <name>javax.jdo.option.ConnectionUserName</name>
     <value>hiveuser</value>
   </property>
   <property>
     <name>javax.jdo.option.ConnectionPassword</name>
     <value>password</value>
   </property>
   ```

   其中，'hiveuser'和'password'分别是您在步骤3中创建的hive元数据用户的用户名和密码。

6. 重启hive服务

   在终端中输入以下命令来重启hive服务：

   ```
   sudo systemctl restart hive-server2
   ```

   然后，您就可以使用MySQL作为hive的元数据数据库了。

希望这些步骤能够帮助您安装并配置MySQL作为hive的元数据。