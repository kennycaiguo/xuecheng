# xuecheng
项目学习，学成在线，一个类似于mooc的在线教育平台

此处用于记录环境开发流程，以及学习过程遇到的问题以及解决方式

学成在线借鉴了MOOC（大型开放式网络课程，即MOOC（massive open online courses））的设计思想，是一个提供IT职业课程在线学习的平台，它为即将和已经加入IT领域的技术人才提供在线学习服务，用户通过在线学习、在线练习、在线考试等学习内容，最终掌握所学的IT技能，并能在工作中熟练应用。

​	当前市场的在线教育模式多种多样，包括：B2C、C2C、B2B2C等业务模式，学成在线采用B2B2C业务模式，即向企业或个人提供在线教育平台和学生完成教学活动，市场上类似的平台有：网易云课堂、腾讯课堂等，学成在线的特点是IT职业课程在线教学。

1.2 项目的功能模块 ​	学成在线是一个在线教育平台，提供IT职业课程在线学习，平台包括：门户、学习中心、教学管理中心、系统管理中心、社交系统等子系统。

项目的功能架构如下图：

​	门户是整个平台的入口，功能包括：门户首页、注册/登录、课程搜索、职业规划，客服等。

​	学习中心为用户提供在线学习服务，包括：我的课程、视频点播、视频直播、在线考试、在线答疑、学习统计等功能；

​	教学管理中心为教育机构或个人讲师提供教学管理功能，包括：课程管理、媒资管理、考试管理、问答管理等功能；

​	系统管理中心提供系统参数配置、CMS、数据字典、分类管理等功能。

1.3 项目的技术架构 ​	项目采用前后端分离的技术架构，前端采用vue.js技术栈，服务端采用SpringBoot、SpringCloud等Spring全家桶技术栈。

具体见问题2.

2 项目采用什么技术架构？ ​	项目采用前后端分离的技术架构，前端采用vue.js构建，服务端采用Spring Cloud微服务架构，系统分为用户层、CDN、负载均衡、前端UI、微服务层、数据层、接口层及DevOps等部分组成，下图是完整的技术架构图：

1-技术架构

业务流程举例：

1、用户可以通过pc、手机等客户端访问系统进行在线学习。

2、 系统应用CDN技术，对一些图片、CSS、视频等资源从CDN调度访问。

3、所有的请求全部经过负载均衡器。

4、对于PC、H5等客户端请求，首先请求UI层，渲染用户界面。

5、客户端UI请求服务层获取进行具体的业务操作。

6、服务层将数据持久化到数据库。

下图是技术架构简图：

1532072294112

1、用户层

用户层描述了本系统所支持的客户端用户有哪些，本项目目前为各用户提供服务，包括H5、PC、Android和IOS等。

2 CDN全称Content Delivery Network，即内容分发网络，本系统所有静态资源全部通过CDN加速来提高访问速度。系统静态资源包括：html页面、js文件、css文件、image图片、pdf和ppt及doc教学文档、video视频等。

3 负载均衡 系统的CDN层、UI层、服务层及数据层均设置了负载均衡服务，系统采用LVS+Nginx实现负载均衡均衡。

4 UI层 UI层描述了系统向pc用户、app用户、h5用户提供的产品界面。本项目在PC和H5端采用vue.js+elementUI实现。

5 微服务层将系统服务分类三类：前端服务、后端服务及系统服务。 前端服务：主要为学习用户提供学习服务。 后端服务：主要为管理用户提供教学管理服务。 系统服务：公共服务，为系统的所有微服务提供公共服务功能。

7 外部系统接口 包括如下接口：

1）第三方登录接口，如QQ、微博、微信等。 2）支付宝、微信支付接口 3）短信接口 （阿里大于）4）邮件接口，通过smpt邮件服务器对外发送电子邮件。 5）微信公众号 6）点播、直播。 7）OSS存储 8）CDN，使用最里云CDN服务加速视频访问速度。

8 DevOps提供了本系统开发、运营、维护支撑的系统，包括如下内容：

Eureka服务治理中心：提供服务治理服务，包括：服务注册、服务获取等。

Docker容器化部署服务：将本系统所有服务采用容器化部署方式。

Maven项目管理工具：提供管理项目所有的Java包依赖、项目工程打包服务。

Git/GitLab代码管理服务:提供git代码管理服务。

Spring Boot Admin服务健康监控：监控微服务的健康状态、会话数量、并发数等。

2.1 微服务技术栈 所有微服务基于Spring Boot、Spring Cloud构建

1）控制层：

Spring MVC、Spring Security Oauth2 、Swagger

2）业务层：

事务控制：Spring

任务处理：Spring Task

数据缓存：Spring Data Redis

消息队列：Spring RabbitTemplate

搜索： Elasticsearch

持久层：
操作MySQL：MyBatis、com.alibaba.druid（采用druid-spring-boot-starter）Spring Data Jpa

操作MongoDB：Spring Data Mongodb

数据层，采用MySQL和MongoDb存储数据，MySQL存储用户、课程等系统核心信息，MongoDb存储
cms、配置信息等

