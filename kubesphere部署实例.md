## 一、微服务篇
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
###### （2）修改nacos上的mysql,redis配置
###### （3）启动微服务，注册nacos

#### 1.6、kubesphere部署RuoYi-Cloud
##### 1.6.1、部署有状态中间件
##### 1.6.2、部署无状态微服务
##### 1.6.3、部署网络
##### 1.6.4、部署配置

