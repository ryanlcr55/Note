## Redis 數據類型    
Redis有五種數據類型 : String, Hash, List, Set 及 Zset

---
### String（字符串）

  * string 是 Redis最基本的類型, 類型是二進制安全的, 意思是String可以包含任何數據, 例如JPG圖面或序列話的對象     
  * string 是一個 key 對應一個  value, 最大能儲存512MB
 
 *實例*
 
    redis 127.0.0.1:6379> SET test "測試"
    OK
    redis 127.0.0.1:6379> GET test 
    "測試"
    redis 127.0.0.1:6379>
    
  `注意：一個键最大能儲存 512MB。`
  
- - -
### Hash
 
  * hash 是一個键值(key=>value)對集合 
  * hash 是一個string 類型的 field 和 value 的映射表，hash 特别適合用於儲存對象。        
  
 *實例*
 
    redis 127.0.0.1:6379> HMSET test field1 "一號" field2 "二號"
    "OK"
    redis 127.0.0.1:6379> HGET test field1
    "一號"
    redis 127.0.0.1:6379> HGET test field2
    "二號"
  
  `每個Hash可儲存 2的32次方 -1 键值對（40多億）`

- - - 
### List（列表）
 * 列表是簡單的字串列表，按照插入順序排序。你可以添加一個元素到列表的頭部（左邊）或者尾部（右邊）
 
 *實例*
 
    redis 127.0.0.1:6379> LPUSH runoobkey redis
    (integer) 1
    redis 127.0.0.1:6379> LPUSH runoobkey mongodb
    (integer) 2
    redis 127.0.0.1:6379> LPUSH runoobkey mysql
    (integer) 3
    redis 127.0.0.1:6379> LRANGE runoobkey 0 10
    
    1) "mysql"
    2) "mongodb"
    3) "redis"
       
 `一個列表最多可以包含 2的32次方 - 1 個元素 (4294967295, 每個列表超过40亿個元素)。` 
    
- - -
### Set (集合)

 * Set 是 String類型的無序集合, 成員是唯一的, 即`集合中不可出現重複的值`
 * Set 是通過 Hash實現的, 時間複雜度為 O(1)
 
 *實例*
 
    redis 127.0.0.1:6379> SADD runoobkey redis
    (integer) 1
    redis 127.0.0.1:6379> SADD runoobkey mongodb
    (integer) 1
    redis 127.0.0.1:6379> SADD runoobkey mysql
    (integer) 1
    redis 127.0.0.1:6379> SADD runoobkey mysql
    (integer) 0
    redis 127.0.0.1:6379> SMEMBERS runoobkey
    
    1) "mysql"
    2) "mongodb"
    3) "redis"
    
>重複輸入 "mysql" 但因 SET值是唯一的, 故結果中 "mysql"只有一個

- - -
### Sort Set (有序集合)

 * 與 SET不同之處為每個元素都會關聯一個double類型的分數, redis正式透過該分數進行排列
 
 *實例*
 
    redis 127.0.0.1:6379> ZADD runoobkey 1 redis
    (integer) 1
    redis 127.0.0.1:6379> ZADD runoobkey 2 mongodb
    (integer) 1
    redis 127.0.0.1:6379> ZADD runoobkey 3 mysql
    (integer) 1
    redis 127.0.0.1:6379> ZADD runoobkey 3 mysql
    (integer) 0
    redis 127.0.0.1:6379> ZADD runoobkey 4 mysql
    (integer) 0
    redis 127.0.0.1:6379> ZRANGE runoobkey 0 10 WITHSCORES
    
    1) "redis"
    2) "1"
    3) "mongodb"
    4) "2"
    5) "mysql"
    6) "4"
  
>重複輸入 "mysql" 同 SET不會存在重複值, 故結果中 "mysql" 只會出現一次, 並對應最後輸入 "mysql" 的分數 "4"

- - -
### HyperLogLog
 * Redis再2.8.9版中添加`HyperLogLog`結構
 * HyperLogLog 是用來做基數統計, 該優點是, 當輸入元素的數量或體積過大時, 計算的空間總是固定的, 且很小
 * Redis中 每個 HyperLogLog鍵只需花12KB內存, 就可計算2^64個不同元素的基數
 * 但是, 因為HyperLogLog只會根據輸入的元素來計算基數, 而不會儲存元素本身, 所以 HyperLogLog不能像集合, 返回輸入的個個元素
 
 >##### 何謂基數?
 >>比如数据集 {1, 3, 5, 7, 5, 7, 8}， 那么这个数据集的基数集为 {1, 3, 5 ,7, 8}, 基数(不重复元素)为5。 基数估计就是在误差可接受的范围内，快速计算基数

 *實例*
 
    redis 127.0.0.1:6379> PFADD runoobkey "redis"
    
    1) (integer) 1
    
    redis 127.0.0.1:6379> PFADD runoobkey "mongodb"
    
    1) (integer) 1
    
    redis 127.0.0.1:6379> PFADD runoobkey "mysql"
    
    1) (integer) 1
    
    redis 127.0.0.1:6379> PFCOUNT runoobkey
    
    (integer) 3
    
    redis 127.0.0.1:6379> PFCOUNT runoobkey
        
    (integer) 3
    
    
- - - 
參考資料 : http://www.runoob.com/redis/redis-data-types.html
