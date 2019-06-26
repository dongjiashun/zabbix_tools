### 前言

  分享个监控的工具基于zabbix
  有人会问为什么已经有zabbix了，还要在做个监控工具
  有以下几点原因:
   告警监控的级别
   
   1.普通告警（不会对业务产生印象且提前准备，类似磁盘，内存使用。。。）

   2.灾难告警（数据库宕机，服务器挂掉，网络不通。。。）

### 怎么才算是告警 

   1.现在我们大家大多数都是用的zabbix或者其他的告警。我想问大家一个问题
   
   2.什么是告警?
   
      a. 通知告警
      
          1. 比如说内存用了百分之50这种是告警？这种应该叫通知
          2. 通知是不需要及时看到，有段时间看到也可以做出处理，严重级别一般
          3. 这类告警，每天有很多，服务器多的话每天就几百份告警邮件或者短信
      
      b.严重告警
      
          1. 就是有问题了必须及时处理，第一时间要感知到


### 目前的情况谁干保证说，凌晨3点钟的时候数据库挂了，大家可以立马在一分钟内就可以感知到？？？有几个人做的到。

### 现在监控告警的情况总结

       1.一大堆告警放到一块，邮件和短信，一大堆无法短时间筛选有效的告警，为什么？每天都有通知类的告警时不时发出来，有效的告警信息都被覆盖了，这个就是表象
       2.除了问题，有谁可以立马感知到，我怕到时还在翻warn这种告警吧
       
       3.有谁可以每隔一分钟或者每隔10分钟看邮件，耐心看报错告警。如果有，也是人才。整天就不用干其他事了，就盯着邮件就好了


### 该工具的出现就是为了解决这几类问题

    功能1：可以自定义告警：可以根据隔离级别发出不同方式告警，可以电话，可以短信，可以邮件。对告警可以分类，分通知方法
    功能2：可以查询历史告警，可以加过滤条件
    功能3：可以变成循环定时器，实时监控zabbix告警，及时通知到目标人
	
	


### 环境 ：

	jdk 1.8 或者 1.7
具体说明 详情看 java -cp dbatools-0.0.1-SNAPSHOT.jar  com.yh.spring.ssm.Controller.Monitor_zabbix --help
 		"功能介绍 " ) ;
		
		"1.过滤告警级别" ) ;
		
		"2.过滤用户组 " ) ;
		
		"3.查询历史告警信息精确到组和具体时间" ) ;
		
		"4.定时监听功能可配置（实时告警）" ) ;
		
		"5.自定义邮件配置，邮件主题可以配置" ) ;
		
		"6.自定义zabbix监听api设定，不局限于本公司" ) ;
		
帮助说明执行以下命令

java -cp dbatools-0.0.1-SNAPSHOT.jar  com.yh.spring.ssm.Controller.Monitor_zabbix --help

### 查询历史告警

案例：：数据库告警 在 2019-04-25 16:42:15 之后的告警 告警基本为4：Disaster 当然不知道告警基本的可以设置--l=0
 java -cp dbatools-0.0.1-SNAPSHOT.jar com.yh.spring.ssm.Controller.Monitor_zabbix --i=10 --d=1556181735l --l=4
 
### 实时告警
  
  java -cp xxx.jar  com.yh.spring.ssm.Controller.Monitor_zabbix --i=10 --d=1556181735 --l=0 --time=1 --send=true
 

配置目录在 resource下
   mail.properties
   zabbix.properties


### 注意
使用方法在使用前需要知道 自己监听的用户组

### 查看自己用户号组 执行以下命令
java -cp dbatools-0.0.1-SNAPSHOT.jar com.yh.spring.ssm.util.zabbixgetHostGroupList


### 后续扩展需求
可更加告警隔离严重级别，区分告警，采用 电话方式

告警邮件样式后期优化
