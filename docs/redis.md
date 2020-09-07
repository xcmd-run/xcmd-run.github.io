# Redis 命令速查

## Keys
---
- `EXISTS key [key ...]` key是否存在    
- `TYPE key` 获取key的存储类型  
- `TTL key` 获取key的有效时间(秒)  
- `PTTL key` 获取key有效时间(毫秒)  
- `EXPIRE key seconds` 设置key过期时间  
- `RENAME key newkey` 重命名  
- `RENAMENX key newkey` 重命名,新key必须不存在  
- `DEL key [key ...]`  删除  
- `KEYS pattern` 按没事查找  
- `SCAN cursor [MATCH pattern] [COUNT count]` 增量迭代key  

## String
---
- `SET key value [EX secondes] [PX milliseconds] [NX|XX]` NX - key不存在才设置值，XX - key存在才设置值  
- `MSET key value [key value ...]` 批量设置  
- `SETNX key value` key不存在是设置值    
- `MSETNX key value [key value ...]` 批量设置，key不存在时设置值  
- `SETEX key seconds value` 指定key value 指定过期时间  
- `SETRANGE key offset value`  覆盖key从offset开始的字符  
- `INCR key` 执行原子加1操作  
- `INCRBY key incremnet` 原子执行增加c  
- `INCRBYFLOAT key incremnet` 原子执行增加一个浮点数值  
- `DECR key` 整数原子减1  
- `DECRBY key decrment` 整数原子减整数  
- `STRLEN key`  获取key值的长度  
- `GET key` 返回key的值  
- `MGET key [key ...]` 返回多个key的值  
- `GETRANGE key start end` 获取子串  
- `GETSET key value` 设置值并返回之前的值    

## Hash
---
- `HSET key field value` 设置一个字段  
- `HMSET key field value [field value ...]` 批量设置字段    
- `HSETNX key field value` 当field不存在是设置
- `HINCRBY key field increment` 指定field增加整数值  
- `HINCRBYFLOAT key field incremnet` 指定field增加浮点数值    
- `HDEL key field [field ...]` 删除field
- `HEXISTS key field` 判断field是否存在
- `HLEN key` 获取hash元素数量
- `HKEYS key` 获取hash的所有field 
- `HVALS key` 获取hash的所有field值 
- `HGET key field` 获取field值  
- `HMGET key field [field ...]` 批量获取field值  
- `HGETALL key` 获取所有field值 
- `HSTRLEN key field` 获取field值的字符长度  
- `HSCAN key cursor [MATCH pattern] [COUNT count]` 迭代hash元素    


## List
---
- `LLEN key` 获取list的长度  
- `LPUSH key value [value ...]` 在队列头部插入元素
- `LPUSHX key value` 当队列存在时，在队列头部插入元素    
- `LPOP kye` 从队列头部移出一个元素  
- `RPUSH key value [value ...]` 从队列尾部插入元素
- `RPUSHX key value` 当队列存在时，在队列尾部插入元素
- `RPOP kye` 从队列尾部移出一个元素
- `RPOPLPUSH source destination` 从source队列尾部移出并写入destination队列头部并返回元素  
- `LPOS key value [RANK rank] [COUNT num-matches] [MAXLEN len]` 返回value在lust中的索引位置  
- `LINDEX key index` 返回list中index位置的元素  
- `LINSERT key BEFORE|AFTER poivot value` 在poivot元素之前或之后插入value
- `LSET key index value` 设置队列index位置的值为value  
- `LRANGE key start stop` 返回指定区间的元素  
- `LREM key count value` 移除前 count 次出现的值为 value 的元素, count >0,从头开始，count<0,从尾部开始，count = 0，全部
- `LTRIM key start stop` 修建list,保留start 到 stop之间的元素
- `BLPOP key [key ...] timeout` 阻塞模式从队列头部移出一个元素，只至有一个可用元素或超时，timeout=0不超时
- `BRPOP key [key ...] timeout` 阻塞模式从队列尾部移出一个元素，只至有一个可用元素或超时，timeout=0不超时
- `BRPOPLPUSH source destination timeout` 阻塞模式从source队列尾部移出并写入destination队列头部并返回元素，只至有一个可用元素或超时，timeout=0不超时  


## Set
---
- `SCARD key` 获取集合元素数量  
- `SADD key member [member ...]` 向集合中添加元素
- `SREM key member [member ...]` 删除集合中的元素
- `SPOP key [count]` 删除count个元素，并返回元素
- `SISMEMBER key member` 判断member是否是集合成员  
- `SMEMBERS key` 获取集合所有元素  
- `SRANDMEMBER key [count]` 随机返回count个元素
- `SMOVE source distination member` 将source集合member移动到distination集合 
- `SINTER key [key ...]` 求集合交集
- `SUNION key [key ...]` 求集合并集
- `SDIFF key [key ...]` 求集合差集
- `SINTERSTORE destination key [key ...]` 求集合交集,并存储在集合destination中
- `SUNIONSTORE destination key [key ...]` 求集合并几,并存储在集合destination中
- `SDIFFSTORE destination key [key ...]` 求集合差集,并存储在集合destination中  
- `SSCAN key cursor [MATCH pattern] [COUNT count]` 迭代集合元素

  
## ZSet
---
- `ZCARD key` 返回有序集合成员数量 
- `ZCOUNT key min max` 返回score在min和max之间的成员数量 
- `ZLEXCOUT key min max` 返回指定分值范围的元素数量
- `ZADD key [NX|XX] [CH] [INCR] score member [score member ...]` 向有序集合添加或更新元素  
- `ZINCRYBY key incremnet member` 增加member的score评分
- `ZRANK key member` 返回成员在集合中的索引
- `ZREVRANK key member` 返回成员在集合中的倒序索引
- `ZSCORE key member` 返回成员的score值
- `ZRANGE key start stop [WITHSOCRES]` 根据index返回集合元素 WITHSOCRES 返回score和value
- `ZREVRANGE key start stop [WITHSOCRES]` 根据index返回集合元素,分值倒序 WITHSOCRES 返回score和value
- `ZRANGEBYLEZ key min max [LIMIT offset count]` 返回指定成员区间内的成员，按成员字典正序排序, 分数必须相同
- `ZRANGEBYSCORE key min max [WITHSOCRES] [LIMIT offset count]` 根据score范围返回集合元素
- `ZREVRANGEBYSCORE key max min [WITHSOCRES] [LIMIT offset count]` 根据score范围返回集合元素,分值倒序
- `ZREVRANGEBYLEZ key min max [LIMIT offset count]` 返回指定成员区间内的成员，按成员字典倒序排序, 分数必须相同
- `ZREM key member [member ...]` 删除集合中的成员
- `ZREMRANGEBYRANK key start stop` 移除有序集key中，指定排名(rank)区间内的所有成员
- `ZREMRANGEBYSCORE key min max` 移除有序集key中，所有score值介于min和max之间(包括等于min或max)的成员。
- `ZREMRANGEBYLEX key min max` 删除名称按字典由低到高排序成员之间所有成员
- `ZPOPMAX key [count]` 移除并返回分值最大的成员
- `ZPOPMIN key [count]` 移除并返回分值最小的成员
- `BZPOPMAX key ` 阻塞模式移除并返回分值最大的成员，只至有一个可用元素或超时
- `BZPOPMIN key ` 阻塞模式移除并返回分值最小的成员，只至有一个可用元素或超时
- `ZUNIONSTORE destination numkeys key [key ...] [WEIGHTS weight] [SUM|MIN|MAX]` 计算给定的numkeys个有序集合的并集，并且把结果放到destination中。在给定要计算的key和其它参数之前，必须先给定key个数(numberkeys)。
- `ZINTERSTORE destination numkeys key [key ...] [WEIGHTS weight] [SUM|MIN|MAX]` 计算给定的numkeys个有序集合的交集，并且把结果放到destination中。 在给定要计算的key和其它参数之前，必须先给定key个数(numberkeys)。
- `ZSCAN key cursor [MATCH pattern] [COUNT count]` 迭代集合元素