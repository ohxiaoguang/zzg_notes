

## 安装
安装docker
```
# 更新数据源
apt-get update
# 安装所需依赖
apt-get -y install apt-transport-https ca-certificates curl software-properties-common
# 安装 GPG 证书
curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# 新增数据源
add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# 更新并安装 Docker CE
apt-get update && apt-get install -y docker-ce
```
配置docker加速
```
tee /etc/docker/daemon.json <<-'EOF'
{
"registry-mirrors": ["https://vvxct781.mirror.aliyuncs.com"]
}
EOF
# 重启 Docker
systemctl daemon-reload
systemctl restart docker
```

安装docker-compose
```
curl -L https://github.com/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```




## 常用脚本
MySQL 5.7
```
#!/bin/bash
docker stop zzg-mysql-5.7
docker rm -f zzg-mysql-5.7
docker run --name zzg-mysql-5.7 -v `pwd`/conf:/etc/mysql/conf.d -v `pwd`/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123 -d mysql:5.7.27
```
conf/my.cnf
```
[mysqld]
character-set-server=utf8mb4

[client]
default-character-set=utf8mb4

[mysql]
default-character-set=utf8mb4

```
mongoDB
```
docker rm -f myMongodb
docker run -p 27017:27017 --name myMongodb -v `pwd`/data/db:/data/db -d mongo --auth
```
第一次启动后需要进行以下操作，对数据库设置密码
```
进入容器
docker exec -it myMongodb bash

进入Mongo
mongo

切库，新增用户
use admin;
db.createUser({ user: "root", pwd: "123", roles: [{ role: "root", db: "admin" }] })
```
Redis
```
docker stop redis
docker rm redis
docker run -p 6379:6379 -v `pwd`/data:/data -d --name redis hub.c.163.com/public/redis:2.8.4 redis-server --appendonly yes --requirepass 123456
```
nacos
```
* Clone 项目
git clone https://github.com/nacos-group/nacos-docker.git
cd nacos-docker
* 单机模式
docker-compose -f example/standalone-mysql.yaml up -d
* 查看日志
docker-compose -f example/standalone-mysql.yaml logs -f
* Nacos 控制台
http://192.168.141.132:8848/nacos
```
RabbitMQ
```
docker rm -f rabbitmq3.7.7
docker run -d --name rabbitmq3.7.7 -p 5672:5672 -p 15672:15672 -v `pwd`/data:/var/lib/rabbitmq --hostname myRabbit -e RABBITMQ_DEFAULT_VHOST=my_vhost  -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin rabbitmq:3.7.7-management
```
zookeeper
```
docker rm -f zzg-zookeeper
docker run --name zzg-zookeeper -p 2181:2181 --restart always -d zookeeper:3.5
```

kafka
```
docker rm -f kafka
docker run -d --name kafka --publish 9092:9092  --link zzg-zookeeper --env KAFKA_ZOOKEEPER_CONNECT=192.168.124.58:2181  --env KAFKA_ADVERTISED_HOST_NAME=localhost  --env KAFKA_ADVERTISED_PORT=9092  --volume D:\\Data\\docker\\volumes\\zzg-kafka:/etc/localtime wurstmeister/kafka:2.11-0.11.0.3
```