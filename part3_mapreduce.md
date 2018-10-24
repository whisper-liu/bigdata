#MapReduce
1. 一种分布式变成框架。计算向数据靠拢，将应用程序分发到数据所在的机器。map函数输入是一个键值对，输入是一堆键值对。reduce函数输入是一个<key,value-list>，输出是一个<key,value>。
2. 体系结构。
- client客户端
- jobtracker 作业跟踪
- tasktracker 任务调度 执行jobtracker发送的命令
- slot是一个任务调度单位（资源单位，2.0已经取消），分为map类型和reduce类型。task也分为map类型和reduce类型。
3. 工作流程。from hdfs对大规模数据集进行分片操作（split，逻辑上），生成很多map任务（由分片数量决定），对每一个map分成多个reduce任务（shuffle），输出到hdfs。
- map任务和reduce任务之间不进行通信。
4. shuffle过程。
![](https://upload-images.jianshu.io/upload_images/5401649-0bc7f61ca9d1b265.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

输入数据进行分片处理，map之后输入处理结果（一堆键值对），写入缓存，满了之后溢写到磁盘中。通过reduce任务取走，经过归并，合并输入到reduce函数，输出到hdfs。
- 写到缓存是因为：减少寻址开销，一次寻址批量写入
- 溢写包括：分区，排序，合并
- map端的shuffle：分区，分区给不同的reduce任务，按照key排序，合并是为了减少溢写到磁盘的数量（如果不经过combine，结果是key-value list，经过的话，结果是key-value n）。
-reduce端的shuffle：从多个map任务拷贝到reducer，归并数据，写入磁盘。
![](https://upload-images.jianshu.io/upload_images/5401649-5e34d8f3ee8b5879.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)