# SHOW COMPUTE NODES

## 功能

该语句用于查看 cluster 内的 CN 节点。

## 语法

```sql
SHOW COMPUTE NODES;
```

命令返回结果说明：

1. **LastStartTime** 表示最近一次 CN 启动时间。
2. **LastHeartbeat** 表示最近一次心跳。
3. **Alive** 表示节点是否存活。
4. **SystemDecommissioned** 为 true 表示节点正在安全下线中。
5. **ClusterDecommissioned** 为 true 表示节点正在当前 cluster 中下线。
11. **ErrMsg** 用于显示心跳失败时的错误信息。
12. **Status** 用于以 JSON 格式显示 CN 的一些状态信息, 目前包括最后一次 CN 汇报其状态的时间信息。
