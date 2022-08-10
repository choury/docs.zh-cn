# StarRocks基本概念

* FE：FrontEnd简称FE，是StarRocks的前端节点，负责管理元数据，管理客户端连接，进行查询规划，查询调度等工作。
* BE：BackEnd简称BE，是StarRocks的后端节点，负责数据存储，计算执行，以及compaction，副本管理等工作。
* CN: ComputeNode简称CN，是StarRocks的计算节点，用来执行计算任务，提升集群的计算能力。
* Broker：StarRocks中和外部HDFS/对象存储等外部数据对接的中转服务，辅助提供导入导出功能。
* StarRocksManager：StarRocks的管理工具，提供StarRocks集群管理、在线查询、故障查询、监控报警的可视化工具。
* Tablet：StarRocks中表的逻辑分片，也是StarRocks中副本管理的基本单位，每个表根据分区和分桶机制被划分成多个Tablet存储在不同BE节点上。
