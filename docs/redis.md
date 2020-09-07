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
