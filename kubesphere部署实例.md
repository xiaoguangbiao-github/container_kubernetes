## 一、微服务部署篇
### 1、kubesphere部署RuoYi-Cloud
#### 1.1、项目介绍
项目地址 https://gitee.com/y_project/RuoYi-Cloud

若依是一套全部开源的快速开发平台，毫无保留给个人及企业免费使用。
* 离的模式，微服务版本前端(基于 RuoYi-Vue)。
* 后端采用Spring Boot、Spring Cloud & Alibaba。
* 注册中心、配置中心选型Nacos，权限认证使用Redis。
* 流量控制框架选型Sentinel，分布式事务选型Seata。
* 提供了技术栈（Vue3 Element Plus Vite）版本RuoYi-Cloud-Vue3，保持同步更新。
* 如需不分离应用，请移步 RuoYi，如需分离应用，请移步 RuoYi-Vue
* 阿里云折扣场：点我进入，腾讯云秒杀场：点我进入  
* 阿里云优惠券：点我领取，腾讯云优惠券：点我领取 

#### 1.2、系统模块
```powershell
com.ruoyi     
├── ruoyi-ui              // 前端框架 [80]
├── ruoyi-gateway         // 网关模块 [8080]
├── ruoyi-auth            // 认证中心 [9200]
├── ruoyi-api             // 接口模块
│       └── ruoyi-api-system                          // 系统接口
├── ruoyi-common          // 通用模块
│       └── ruoyi-common-core                         // 核心模块
│       └── ruoyi-common-datascope                    // 权限范围
│       └── ruoyi-common-datasource                   // 多数据源
│       └── ruoyi-common-log                          // 日志记录
│       └── ruoyi-common-redis                        // 缓存服务
│       └── ruoyi-common-seata                        // 分布式事务
│       └── ruoyi-common-security                     // 安全模块
│       └── ruoyi-common-swagger                      // 系统接口
├── ruoyi-modules         // 业务模块
│       └── ruoyi-system                              // 系统模块 [9201]
│       └── ruoyi-gen                                 // 代码生成 [9202]
│       └── ruoyi-job                                 // 定时任务 [9203]
│       └── ruoyi-file                                // 文件服务 [9300]
├── ruoyi-visual          // 图形化管理模块
│       └── ruoyi-visual-monitor                      // 监控中心 [9100]
├──pom.xml                // 公共依赖
```
#### 1.3、架构图
![image](https://user-images.githubusercontent.com/78718204/230854462-ad874ec8-5238-4f62-9930-8b30859394d8.png)

#### 1.4、在线体验
admin/admin123
演示地址：http://ruoyi.vip
文档地址：http://doc.ruoyi.vip

#### 1.5、本地部署RuoYi-Cloud
##### 1.5.1、本地拉取RuoYi-Cloud代码
https://gitee.com/y_project/RuoYi-Cloud

##### 1.5.2、准备mysql、redis

##### 1.5.3、准备nacos
###### （1）单机部署nacos
https://nacos.io/zh-cn/docs/v2/guide/admin/deployment.html
###### （2) 修改application.properties数据库
###### （2) 单机启动nacos
./startup -m standalone

##### 1.5.4、微服务注册nacos
###### （1）mysql中初始化sql
###### （2）重启nacos并修改nacos上的微服务配置文件中的mysql,redis
###### （3）启动微服务，注册nacos

##### 1.5.5、启动前端vue
###### （1）部署node.js
###### （2）安装依赖
###### （3）启动前端vue

### 1.6、kubesphere部署RuoYi-Cloud
#### 1.6.1、部署有状态中间件
###### （1）部署mysql
###### （2）部署redis
###### （3）部署nacos
https://nacos.io/zh-cn/docs/v2/guide/admin/cluster-mode-quick-start.html

#### 1.6.2、部署无状态微服务
###### （1）编写DockerFile
```powershell
FROM openjdk:8-jdk
LABEL maintainer=xiaoguangbiao

#docker run -e PARAMS="--server.port 9090"
ENV PARAMS="--server.port=8080 --spring.profiles.active=prod --spring.cloud.nacos.discovery.server-addr=his-nacos.his:8848 --spring.cloud.nacos.config.server-addr=his-nacos.his:8848 --spring.cloud.nacos.config.namespace=prod --spring.cloud.nacos.config.file-extension=yml"
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

COPY target/*.jar /app.jar
EXPOSE 8080

ENTRYPOINT ["/bin/sh","-c","java -Dfile.encoding=utf8 -Djava.security.egd=file:/dev/./urandom -jar app.jar ${PARAMS}"]
```
###### （2）打镜像tag
```powershell
docker build -t ***:v1.0 -f DockerFile .
```
###### （3）重命名镜像tag
```powershell
docker tag 461955fe1e57 registry.cn-shenzhen.aliyuncs.com/lfy_ruoyi/ruoyi-visual-monitor:v1
```
###### （4）推送到阿里云镜像仓库
```powershell
docker push registry.cn-shenzhen.aliyuncs.com/ruoyi-xgb/ruoyi-visual-monitor:v1
```

###### （4）部署应用

#### 1.6.3、部署网络
#### 1.6.4、部署配置





### 1、kubesphere部署尚医通
#### 1.1、项目介绍
项目地址：
https://gitee.com/leifengyang/yygh-parent
https://gitee.com/leifengyang/yygh-admin
https://gitee.com/leifengyang/yygh-site

尚医通是一套全部开源的快速开发平台，毫无保留给个人及企业免费使用。
* 离的模式，微服务版本前端(基于 RuoYi-Vue)。
* 后端采用Spring Boot、Spring Cloud & Alibaba。
* 注册中心、配置中心选型Nacos，权限认证使用Redis。
* 流量控制框架选型Sentinel，分布式事务选型Seata。
* 提供了技术栈（Vue3 Element Plus Vite）版本RuoYi-Cloud-Vue3，保持同步更新。
* 如需不分离应用，请移步 RuoYi，如需分离应用，请移步 RuoYi-Vue
* 阿里云折扣场：点我进入，腾讯云秒杀场：点我进入  
* 阿里云优惠券：点我领取，腾讯云优惠券：点我领取 

#### 1.2、系统模块
```powershell
yygh-parent
|---common                                  //通用模块
|---hospital-manage                         //医院后台				[9999]   
|---model																		//数据模型
|---server-gateway													//网关    				[80]
|---service																	//微服务层
|-------service-cmn													//公共服务				[8202]
|-------service-hosp												//医院数据服务		[8201]
|-------service-order												//预约下单服务		[8206]
|-------service-oss													//对象存储服务		[8205]
|-------service-sms													//短信服务				[8204]
|-------service-statistics									//统计服务				[8208]
|-------service-task												//定时服务				[8207]
|-------service-user												//会员服务				[8203]


====================================================================

yygh-admin																	//医院管理后台		[9528]
yygh-site																		//挂号平台				[3000]
```
#### 1.3、架构图
![image](https://user-images.githubusercontent.com/78718204/231414767-e379967a-c30a-4de1-bfa5-9aad1a858c4b.png)

#### 1.4、在线体验
暂无

#### 1.5、本地部署尚医通
##### 1.5.1、本地拉取RuoYi-Cloud代码
https://gitee.com/y_project/RuoYi-Cloud

##### 1.5.2、准备mysql、redis

### 1.6、kubesphere部署尚医通（depops）
#### 1.6.1、部署有状态中间件
###### （1）部署mysql
###### （2）部署redis
###### （3）部署nacos
https://nacos.io/zh-cn/docs/v2/guide/admin/cluster-mode-quick-start.html
###### （4）部署RabbitMq
可以从应用商店部署
###### （5）部署MongoDb
可以从应用商店部署



