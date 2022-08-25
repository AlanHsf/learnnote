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