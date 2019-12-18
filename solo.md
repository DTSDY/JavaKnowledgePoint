```bash
# 安装docker
yum -y install docker

#启动 Docker 后台服务
service docker start

# 安装mysql:5.6,直接docker run 他会自动去官方镜想下载
# MYSQL_ROOT_PASSWORD=你的数据库密码
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6

# docker安装的mysql默认允许远程连接，可以使用Navicat等软件连接数据库
# 进入容器mysql
docker exec -it mysql bash

# 进入数据库 p后面跟你的密码
mysql -uroot -pXXX

# 创建数据库(数据库名:solo;字符集utf8mb4;排序规则utf8mb4_general_ci)
create database solo DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
# 出现Query OK, 1 row affected (0.00 sec)表示成功
#退出数据库
exit
#退出容器
exit

# 获取最新镜像
docker pull b3log/solo

# 使用 MySQL
docker run --detach --name solo --network=host \
    --env RUNTIME_DB="MYSQL" \
    --env JDBC_USERNAME="root" \
    --env JDBC_PASSWORD="123456" \
    --env JDBC_DRIVER="com.mysql.cj.jdbc.Driver" \
    --env JDBC_URL="jdbc:mysql://127.0.0.1:3306/solo?useUnicode=yes&characterEncoding=UTF-8&useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true" \
    b3log/solo --listen_port=8080 --server_scheme=http --server_host=116.62.136.166 --server_port=8080
    
# --listen_port：进程监听端口
# --server_scheme：最终访问协议，如果反代服务启用了 HTTPS 这里也需要改为 https
# --server_host：最终访问域名或公网 IP，不要带端口
# --server_port：最终访问端口，使用浏览器默认的 80 或者 443 的话值留空即可



# 编写定时任务
crontab -e

00 02 * * * ls  每日2点执行

# 升级
docker pull b3log/solo
docker stop solo
docker rm solo
docker run --detach --name solo --network=host \
    --env RUNTIME_DB="MYSQL" \
    --env JDBC_USERNAME="root" \
    --env JDBC_PASSWORD="123456" \
    --env JDBC_DRIVER="com.mysql.cj.jdbc.Driver" \
    --env JDBC_URL="jdbc:mysql://127.0.0.1:3306/solo?useUnicode=yes&characterEncoding=UTF-8&useSSL=false&serverTimezone=UTC" \
    b3log/solo --listen_port=8080 --server_scheme=http --server_host=116.62.136.166
    
    
    
    
    
    
    docker run --detach -v /usr/local/solo/markdowns/:/opt/solo/markdowns/:ro --name solo --network=host \
--env RUNTIME_DB="MYSQL" \
--env JDBC_USERNAME="root" \
--env JDBC_PASSWORD="123456" \
--env JDBC_DRIVER="com.mysql.cj.jdbc.Driver" \
--rm \
--env JDBC_URL="jdbc:mysql://127.0.0.1:3306/solo?useUnicode=yes&characterEncoding=UTF-8&useSSL=false&serverTimezone=UTC" \
b3log/solo --listen_port=8080 --server_scheme=http --server_host=116.62.136.166 --server_port=8080

```

