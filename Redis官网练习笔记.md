# Redis官网在线练习笔记[Redis官网](http://resid.io)  

> 在线练习[Redis在线练习](http://try.redis.io/)    
命令列表[Commands](https://redis.io/commands)  

## 基本操作  

1. SET name "yhc" => OK;	设置值  

2. GET name	=> 数据（存在）或	（nil）（不存在）;	获取值  

3. SETNX name "yhc"	=> 0失败，1成功; 不存在name才插入，否则返回0  

4. INCR num 10 => 11; num的值变为11，即存在的值+1,不存在时为1  

5. DEL name	=> 0失败，1成功;	删除值  

6. SET resource:lock "Redis Demo" => OK  
   EXPIRE resource:lock 120 =>1 设置自动删除时间为120s  
   TTL resource:lock => 113 还剩113s删除（-2已删除，-1永不删除）  
   重新SET resource:lock的值后，其过期时间也会失效  


## List类型数据  

涉及到的命令：`RPUSH` `LPUSH` `LLEN` `LRANGE` `LPOP` `RPOP`  

1. `RPUSH`插入数据到底部  
RPUSH friends "Tom" => 1  
RPUSH friends "Bob"  

2. `LPUSH`插入数据到顶部  
LPUSH friends "Sam" => 1  

3. `LRANGE`获取List中的值  
LRANGE friends 0 -1 获取全部  
LRANGE friends 0 1	第0个到第1个，不足取全部  

4. `LLEN`获取List长度  
LLEN friends  

5. `LPOP`删除第0个数据，并返回删除的值  
LPOP friends  

6. `RPOP`删除最后一个数据，并返回删除的值  
RPOP friends  


## Set类型数据  

涉及到的命令 `SADD` `SREM` `SISMEMBER` `SMEMBERS` `SUNION`  

1. `SADD`插入数据  
SADD students "zhang" => 1  
SADD students "wang" => 1  

2. `SREM`删除数据  
SREM students "zhang"  

3. `SISMEMBER`判断值是否存在，1存在，0不存在  
SISMEMBER students "wang" => 1  
SISMEMBER students "zhang" => 0  

4. `SMEMBERS`返回所有数据  
SMEMBERS students  

5. `SUNION`整合两个或多个Set，并返回所有值  
SADD teachers "hh" => 1  
SADD teachers "gg"  
SUNION students teachers = > 所有值  


## Sorted Sets类型数据  

> 为数据设置排序值，不同于常规Set，此Set可排序

涉及到的命令 `ZADD` `ZRANGE`  

1. `ZADD`插入数据,以下案例，年份作为排序依照  
ZADD hackers 1940 "Alan" => 1  
ZADD hackers 1906 "Grace"  
ZADD hackers 1932 "Claude"  

2. `ZRANGE`获取值  
ZRANGE hackers 0 1 => 年份最小的两个值  


## Hashes类型数据  

> 类似Map的键值对，用来存储Object，如User对象  

涉及到的命令 `HSET` `HGETALL` `HMSET` `HGET`  

1. `HSET`存储对象  
HSET user:1000 name "John" => 1  
HSET user:1000 email "gg@foxmail.com"  
HSET user:1000 password "123"  

2. `HGETALL`返回对象属性  
HGETALL user:1000 => 对象属性+值  

3. `HMSET`一次插入多个属性  
HMSET user:1001 name "Mary Jones" password "hidden" email "mjones@example.com" => OK  

4. `HGET`得到特定属性值  
HGET user:1001 name => "Mary Jones"  

5. 额外命令  
HSET user:1000 visits 10  
HINCRBY user:1000 visits 1 => 11  
HINCRBY user:1000 visits 10 => 21  
HDEL user:1000 visits  
HINCRBY user:1000 visits 1 => 1  








