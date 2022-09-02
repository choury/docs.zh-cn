# 手动部署计算节点

计算节点（Compute Node，以下简称 CN） 负责 SQL 执行，提升集群的计算能力。本文介绍如何配置部署一个 CN 节点。您可以通过重复以下步骤添加多个 CN 节点。

## 下载并解压安装包

[下载](https://www.starrocks.com/zh-CN/download) StarRocks 并解压二进制安装包。

```bash
tar -xzvf StarRocks-x.x.x.tar.gz
```

> 注意
> 将以上文件名修改为下载的二进制安装包名。

## 配置 CN 节点

进入 **StarRocks-x.x.x/be** 路径。

```bash
cd StarRocks-x.x.x/be
```

> 注意
> 将以上路径名修改为解压后的路径名。
修改 CN 节点配置文件 **conf/cn.conf**。因默认配置即可启动集群，以下示例并未修改 CN 节点配置。如需在生产环境中对集群进行详细优化配置，因为大部分参数均继承自BE，可以参考 [BE 参数配置](../administration/Configuration.md#BE-参数配置)。

## 添加 CN 节点

通过 MySQL 客户端将 CN 节点添加至 StarRocks 集群。

```sql
mysql> ALTER SYSTEM ADD COMPUTE NODE "host:port";
```

> 注意
> `host` 需要与 `priority_networks` 相匹配，`port` 需要与 **cn.conf** 文件中的设置的 `heartbeat_service_port` 相同，默认为 `9050`。
如添加过程出现错误，需要通过以下命令将该 CN 节点从集群移除。

```sql
mysql> ALTER SYSTEM drop COMPUTE NODE "host:port";
```

> 说明
> `host` 和 `port` 与添加的 CN 节点一致。

## 启动 CN 节点

运行以下命令启动 CN 节点。

```shell
bin/start_cn.sh --daemon
```

## 确认 CN 启动成功

通过 MySQL 客户端确认 CN 节点是否启动成功。

```sql
SHOW PROC '/compute_nodes'\G
```

示例：

```Plain Text
MySQL [(none)]> SHOW PROC '/compute_nodes'\G
*************************** 1. row ***************************
        ComputeNodeId: 78825
              Cluster: default_cluster
                   IP: 172.26.xxx.xx
        HeartbeatPort: 9050
               BePort: 9060
             HttpPort: 8040
             BrpcPort: 8060
        LastStartTime: NULL
        LastHeartbeat: NULL
                Alive: true
 SystemDecommissioned: false
ClusterDecommissioned: false
               ErrMsg: 
              Version: 2.4.0-76-36ea96e
1 row in set (0.01 sec)
```

当 `Alive` 为 `true` 时，当前 CN 节点正常接入集群。

如果 CN 节点没有正常接入集群，可以通过查看 **log/cn.WARNING** 日志文件排查问题。

### 停止 CN 节点

运行以下命令停止 CN 节点。

```bash
./bin/stop_cn.sh
```
