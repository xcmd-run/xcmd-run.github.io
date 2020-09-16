# Zookeeper 速查

## Zookeeper 架构
![Zookeeper server](https://zookeeper.apache.org/doc/r3.6.1/images/zkservice.jpg)
  
![Zookeeper dir](https://zookeeper.apache.org/doc/r3.6.1/images/zknamespace.jpg)

## 常用命令
- `create [-s] [-e] path data acl` 创建节点
- `delete path [version]` 删除节点
- `set path data [version]` 写数据
- `get path [watch]` 读数据
- `ls path [watch]` ls节点
- `sync path` 同步数据

## 常用配置
zoo.cfg
```sh
tickTime=2000
dataDir=/var/lib/zookeeper/
clientPort=2181
initLimit=5
syncLimit=2
server.1=zoo1:2888:3888
server.2=zoo2:2888:3888
server.3=zoo3:2888:3888
```

---
参考资料：
https://developer.aliyun.com/article/772373?utm_content=g_1000182349