# debain 11 安装postgresql 12

###  安装命令

- 安装 sudo apt-get install postgresql-12
  - 提示 Unable to locate package postgresql-12  这时候需要添加Postgresql 官方存储库
  - 参考文档postgresql 官方文档: https://www.postgresql.org/download/linux/debian/ 
    - 创建文件存储库配置：sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
    - 导入存储库签名和密钥：wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    - 更新资源包 ： sudo apt-get update
    - 安装对应版 ：sudo apt-get -y install postgresql-12

- 验证安装 sudo -u postgresql psql -c "SELECT  version"

  - 输出内容：PostgreSQL 11.14 (Debian 11.14-0+deb10u1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 8.3.0-6) 8 即为安装成功

- 修改密码：

  - 1、先切换用户：su postgres 
  - 2、psql 进入postgres
  - 3、ALTER Role postgres WITH PASSWORD '123456';

- 启用PostgreSQL 服务器可远程访问

  - 打开配置文件 postgresql.conf：sudo vi /etc/postgresql/11/main/postgresql.conf

    - 将listen_addresses 的值修改为：listen_addresses = '*'   *# what IP address(es) to listen on;*

  - 打开配置文件`pg_hba.conf`:  sudo vi /etc/postgresql/11/main/pg_hba.conf

    - ```
      # "local" is for Unix domain socket connections only
      #local   all             all                                     peer
      local   all             all                                    md5 
      # IPv4 local connections:
      # host    all             all             127.0.0.1/32            md5
      host    all             all             0.0.0.0/0            md5
      
      ```

- 使用pgAdmin4 远程连接数据库，测试是否可以外部访问

### PostgreSQL 基本命令使用

- 创建数据库：createdb '数据名称'  example：createdb mydb 不报错就是创建成功
  - createdb ： command not found  没有找到createdb 指令 没有正确的安装 PostgreSQL 
    - 要么你的 shell 的搜索路径没有设置为包含它。尝试使用绝对路径调用命令：/usr/local/pgsql/bin/createdb mydb：
  - 
- 