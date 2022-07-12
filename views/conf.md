## 平台环境、组件要求

>概述

iPlat4J V6平台的运行需要依赖一些组件，分为必须组件和可选组件。
>必须组件

必须组件为开发过程必要的组件，也是运行过程中最基础的组件。  

* JDK(Java Development Kit) 

  版本：1.8及以上。

* 数据库
| 编号<img width=60/>  | 软件<img width=120/>  | 推荐版本<img width=200/>  |
| :----| :----| :----|
| 1 | Oracle | 11g-11.2.0.1 |
| 2 | MySql | 5.7 |
| 3 | DB2 | 10.5.5 |

* 应用服务器（中间件）
| 编号<img width=60/>  | 软件<img width=120/>  | 推荐版本<img width=200/>  |
| :----| :----| :----|
| 1 | Tomcat | 8.5.23 |
| 2 | Weblogic | 12.2.1.0.0 |
| 3 | WAS | 8.5.5 |

>可选组件

可选组件是用户使用平台时，根据实际应用需求进行选择，用于项目集成测试、投运使用所需的组件。

* 分布式缓存redis  
用于会话session共享，以及多台服务器间缓存共享。

* 自动化部署iPlatCode  
负责自动化获取代码变更、发布应用更新，灰度发布的管理工具。

* 日志收集、分析、展示组件  
包括日志采集Logstash、日志搜索引擎ElasticSearch、日志可视化Kibana、监控管理平台iPlatAPM。用于日常监控、分析。

* nginx反向代理  
将不同模块的访问地址统一暴露到同一个外部入口的组件，解决分布式系统路由问题。

## 开发工具&发布包
|  | 软件 | 推荐版本 |  获取途径  |
| :----| :----| :----| :----|
| 1 | <div style="width:350px">STS-iplat.zip（含JDK1.8.0_31、Tomcat8.5.23、Maven3.3.3、STS3.9.5和iPlat4J代码自动生成插件）</div> | 针对64位系统 | |
| 2 | JDK | 1.8 |  <div style="width: 450px"> <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html></div> |
| 3 | Tomcat | 8.5 | <http://tomcat.apache.org/> |
| 4 | Maven |3.3.9及以上 | <http://maven.apache.org/> |
| 5 | STS | 3.9.5 | <https://spring.io/tools> |
| 6 | iPlat4J V6发布包 | 6 | 参见：[02 开发工具&发布包](https://confluence.baocloud.cn/pages/viewpage.action?pageId=17137955)|

