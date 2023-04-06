## 1、部署MySQL
### 1.1、docker方式启动
```powershell
docker run -p 3306:3306 --name mysql-01 \
-v /mydata/mysql/log:/var/log/mysql \
-v /mydata/mysql/data:/var/lib/mysql \
-v /mydata/mysql/conf:/etc/mysql/conf.d \
-e MYSQL_ROOT_PASSWORD=root \
--restart=always \
-d mysql:5.7 
```
### 1.2、MySQL部署分析
![image](https://user-images.githubusercontent.com/78718204/230373295-926dc608-50e6-4f1c-a082-8af72c990134.png)

### 1.3、MySQL部署步骤
#### （1）docker方式启动MySQL，copy出my.cnf
```powershell
[client]
default-character-set=utf8mb4
 
[mysql]
default-character-set=utf8mb4
 
[mysqld]
init_connect='SET collation_connection = utf8mb4_unicode_ci'
init_connect='SET NAMES utf8mb4'
character-set-server=utf8mb4
collation-server=utf8mb4_unicode_ci
skip-character-set-client-handshake
skip-name-resolve
```

#### （2）【kubesphere配置中心】配置my.cnf
![11](https://user-images.githubusercontent.com/78718204/230373725-97e303a6-4602-4862-8614-d71c173d7757.png)

#### （3）【kubesphere工作负载】镜像自选、端口默认、设置环境变量、同步时区
![12](https://user-images.githubusercontent.com/78718204/230374507-ed4a41dd-9a67-46ac-ad9b-6f7d1419384c.png)

#### （4）【kubesphere工作负载】设置存储卷
![13](https://user-images.githubusercontent.com/78718204/230374529-3070cec1-dfa1-4c7c-b553-cdca33f461b4.png)

#### （5）【kubesphere工作负载】设置配置文件
![14](https://user-images.githubusercontent.com/78718204/230374551-e51f0941-dd18-426c-871c-ac9258fc0cd0.png)

#### （6）【kubesphere服务】调整服务


## 2、部署Redis
### 2.1、docker方式启动
```powershell
#创建配置文件
## 1、准备redis配置文件内容
mkdir -p /mydata/redis/conf && vim /mydata/redis/conf/redis.conf

#docker启动redis
docker run -d -p 6379:6379 --restart=always \
-v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
-v  /mydata/redis-01/data:/data \
 --name redis-01 redis:6.2.5 \
 redis-server /etc/redis/redis.conf
```
### 2.2、Redis部署分析
![image](https://user-images.githubusercontent.com/78718204/230374831-97edf68e-6585-4553-9d53-7c021a626173.png)


### 2.3、Redis部署步骤
#### （1）docker方式启动Redis，copy出redis.conf
```powershell
appendonly yes
port 6379
bind 0.0.0.0
```

#### （2）【kubesphere配置中心】配置redis.conf
![21](https://user-images.githubusercontent.com/78718204/230375152-a72e9899-65f7-4004-b3a2-efc928ca0359.png)

#### （3）【kubesphere工作负载】镜像自选、端口默认、设置启动命令、同步时区
![22](https://user-images.githubusercontent.com/78718204/230375964-b123607d-64a4-462c-9d2d-6720265a3bb4.png)

#### （4）【kubesphere工作负载】设置存储卷
![23](https://user-images.githubusercontent.com/78718204/230376074-9b94a4f4-303d-4837-9031-95c7b33b48ca.png)

#### （5）【kubesphere工作负载】设置配置文件
![24](https://user-images.githubusercontent.com/78718204/230376110-e3e87a96-ef35-4241-a52f-fa96b8ad6eb4.png)

#### （6）【kubesphere服务】调整服务

## 3、部署ElasticSearch
### 3.1、docker方式启动
```powershell
# 创建数据目录
mkdir -p /mydata/es-01 && chmod 777 -R /mydata/es-01

# 容器启动
docker run --restart=always -d -p 9200:9200 -p 9300:9300 \
-e "discovery.type=single-node" \
-e ES_JAVA_OPTS="-Xms512m -Xmx512m" \
-v es-config:/usr/share/elasticsearch/config \
-v /mydata/es-01/data:/usr/share/elasticsearch/data \
--name es-01 \
elasticsearch:7.13.4
```
### 3.2、es部署分析
![image](https://user-images.githubusercontent.com/78718204/230366322-01bccb9b-23e1-4e19-8a8e-b67dadf12ec7.png)
注意： 子路径挂载，配置修改后，k8s不会对其Pod内的相关配置文件进行热更新，需要自己重启Pod

### 3.3、es部署步骤
#### （1）docker方式启动es，copy出elasticsearch.yml、jvm.options
参见3.1、docker方式启动

#### （2）【kubesphere配置中心】配置elasticsearch.yml、jvm.options
![screenshot-20230406-194651](https://user-images.githubusercontent.com/78718204/230367517-934caad3-e0c5-4d16-87d8-480c22b2f8ba.png)

#### （3）【kubesphere工作负载】镜像自选、端口默认、设置环境变量、同步时区
![01](https://user-images.githubusercontent.com/78718204/230371259-9847a708-48dd-4d4c-9372-1744ca759021.png)

#### （4）【kubesphere工作负载】设置存储卷
![0](https://user-images.githubusercontent.com/78718204/230371532-82f815cb-1438-4a58-8658-748234d289ff.png)

#### （5）【kubesphere工作负载】设置配置文件
![1](https://user-images.githubusercontent.com/78718204/230371999-7f43d6c8-c301-4d1f-a514-5e342be396fa.png)
![2](https://user-images.githubusercontent.com/78718204/230372117-cd7b4751-5643-4258-80dc-6cbf909e47d1.png)

最终如下：  
![screenshot-20230406-195000](https://user-images.githubusercontent.com/78718204/230372152-6471a8fc-cf38-4a6e-a11d-fb806c9e4d1e.png)

#### （6）【kubesphere服务】调整服务

