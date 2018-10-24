#Spark
1. spark与hadoop对比
- hadoop表达能力有限，磁盘io开销大（都写到hdfs里），延迟高，任务之间的连接涉及io开销，难以胜任复杂/多阶段的任务。
- 提供了多种数据集操作，提供了内存计算效率更高，DAG迭代机制。
2. 架构 
优点：利用多线程执行任务，减少任务启动开销。executor有一个blockmanager存储模块，将内存和磁盘作为存储设备，较少io开销。
![](https://upload-images.jianshu.io/upload_images/5401649-1e3259b78b33b2e9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
一个application有一个driver和多个job，一个job包含多个stage，一个stage包括多个task。执行一个application，driver向集群管理器申请资源，启动executor，执行task，结束后把结果返回。
3. 流程
![](https://upload-images.jianshu.io/upload_images/5401649-3a03176de0394230.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 每个aoolication都有自己的executor进程，以多线程的方式运行task。
- spark运行与资源管理器无关，只需获取executor进程并保持通信。
- task数据本地性，推测执行。
4. RDD 弹性分布式数据集 resillient distributed dataset
一个RDD是一个分布式对象几何，只读。避免中间数据存储。
- 执行过程：读入外部数据源，经过一系列转换每次都产生不同的RDD，最后一个RDD经过动作操作计算并输出。
- 高容错性。血缘关系结构决定，从父RDD转换恢复。
- 中间结果持久化到内存。数据在内存中RDD传递，避免io开销。
- 存放对象可以是Java对象，避免了不必要的对象序列化
5. RDD的依赖关系，帮助划分stage。在DAG中反向解析，遇到宽依赖就断开，遇到窄依赖就加入stage。将窄依赖尽量划分在一个stage中，形成流水线操作。
- 窄依赖：一对一，多对一。
- 宽依赖：一对多。
- shufflemapstage 
- resultstage 直接输出结果
6. spark部署
![](https://upload-images.jianshu.io/upload_images/5401649-f6e5784f6cd331ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
