##hadoop introduction
1. hadoop核心：HDFS（解决海量数据存储问题），MapReduce（解决处理问题），可以用普通pc构成集群
2. 离线分析：hive，pig，mr 实时查询：solr，redis，hbase bi分析：mahout
3. hadoop1.0与2.0区别
   - 2.0具有HDFS，MR，YARN三个核心
   - yarn负责资源调度，mr只负责处理，运行在yarn上的mr
   - hdfs：NN federation（分区管理），高可用性（HA，热备份）
4. 架构
   - 采集层：flume（日志收集），kalfka，sqoop（fromsql数据导入导出）
   - 存储层：HDFS
   - 调度层：YARN
   - 计算层：MR（离线计算），Tez，Spark（内存计算）
   - 交互层：hive，pig，hbase
   - ambari（安装部署工具）
   - zookeeper（管家）
5. 命令
   - hadoop fs 包括本地&HDFS
   - hadoop dfs HDFS
   - hdfs dfs HDFS
