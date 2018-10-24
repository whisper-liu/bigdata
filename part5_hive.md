#数据仓库hive
1. 本来不具有数据的存储和分析，提供了一种语言。
- 采用批处理方式处理海量数据，将hiveQL语句转为mr任务。
- 存储的静态数据，适合采用批处理处理方式。
- 提供了一系列工具对数据进行存储处理。
2. hive对外访问接口，驱动模块（把HiveQL转换为MR语句），元数据存储模块（独立的关系型数据库）
![](https://upload-images.jianshu.io/upload_images/5401649-bf13b56fdbfd3a75.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
