以下是在Ubuntu中安装Hive的步骤：

1. 安装Java

   在终端中输入以下命令来安装Java：

   ```
   sudo apt-get update
   sudo apt-get install default-jdk
   ```

2. 下载Hive

   在终端中输入以下命令来下载Hive：

   ```
   wget https://mirrors.tuna.tsinghua.edu.cn/apache/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz
   ```

   这个命令会从清华镜像站下载Hive的压缩包。

3. 解压Hive

   在终端中输入以下命令来解压Hive：

   ```
   tar -zxvf apache-hive-3.1.2-bin.tar.gz
   ```

   这个命令会将Hive解压到当前目录下的apache-hive-3.1.2-bin目录中。

4. 配置Hive

   打开Hive的配置文件hive-env.sh，并添加以下配置：

   ```
   export HADOOP_HOME=/path/to/hadoop
   export HIVE_CONF_DIR=/path/to/hive/conf
   ```

   其中，'/path/to/hadoop'是您安装Hadoop的路径，'/path/to/hive/conf'是您存放Hive配置文件的路径。

   ####   如果在Hive的conf目录中没有找到hive-env.sh文件，您可以尝试查看Hive的安装目录下是否有一个名为hive-env.sh.template的文件。这个文件是Hive的环境变量模板文件，您可以将其复制并重命名为hive-env.sh，然后进行编辑。

   您可以使用以下命令来复制hive-env.sh.template文件并重命名为hive-env.sh：

   ```
   cd apache-hive-3.1.2-bin/conf
   cp hive-env.sh.template hive-env.sh
   ```

   然后，您可以使用文本编辑器（如vi或nano）打开hive-env.sh文件进行编辑。

5. 启动Hive

   在终端中输入以下命令来启动Hive：

   ```
   cd apache-hive-3.1.2-bin
   bin/hive
   ```

   这个命令会启动Hive的命令行界面。

6. 测试Hive

   在Hive的命令行界面中输入以下命令来测试Hive：

   ```
   show databases;
   ```

   如果Hive正常工作，它会列出所有的数据库。

希望这些步骤能够帮助您在Ubuntu中安装Hive。