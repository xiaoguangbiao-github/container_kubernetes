## 1、部署mysql

## 3、部署redis

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

#### （3）【kubesphere工作负载】镜像自选、端口默认、设置环境变量
![01](https://user-images.githubusercontent.com/78718204/230371259-9847a708-48dd-4d4c-9372-1744ca759021.png)

#### （4）【kubesphere工作负载】设置存储卷
![0](https://user-images.githubusercontent.com/78718204/230371532-82f815cb-1438-4a58-8658-748234d289ff.png)

#### （5）【kubesphere工作负载】设置配置文件
![1](https://user-images.githubusercontent.com/78718204/230371999-7f43d6c8-c301-4d1f-a514-5e342be396fa.png)
![2](https://user-images.githubusercontent.com/78718204/230372117-cd7b4751-5643-4258-80dc-6cbf909e47d1.png)

最终如下：  
![screenshot-20230406-195000](https://user-images.githubusercontent.com/78718204/230372152-6471a8fc-cf38-4a6e-a11d-fb806c9e4d1e.png)

#### （6）【kubesphere服务】调整服务

