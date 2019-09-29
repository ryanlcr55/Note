## Redis事務 與 Watch
#### 1.MULTI
    事務可以將指令打包, 再透過 `exec` 指令一次執行, 事務在執行時能確保不被中斷 
    
    範例 : 
    
````  
redis> MULTI            # 事務開始
OK

redis> INCR user_id     # 多條命令依照順序待執行
QUEUED

redis> INCR user_id
QUEUED

redis> INCR user_id
QUEUED

redis> PING
QUEUED

redis> EXEC             # 執行
1) (integer) 1
2) (integer) 2
3) (integer) 3
4) PONG
````

####2. EXEC  
    
    執行`multi`內所有指令    
    事務不保證`原子性`, 也就是當指令列有錯誤發生時, 前面的指令`不會回復`, 而在錯誤發生後列隊的指令也會`繼續執行`
     
     範例 :  
     
````
redis＞MULTI
OK
redis＞SET key 1
QUEUED
redis＞SADD key 2
QUEUED
redis＞SET key 3
QUEUED
redis＞EXEC
1) OK
2) (error) ERR Operation against a key holding the wrong kind of value #此處發生錯誤
3) OK #錯誤後仍繼續執行
redis＞GET key
"3"
````  

####3. DISCARD
    * 可用版本 : >= 2.0.0 
    取消事務, 放棄事務中所有佇列的指令, 若事務正在被監控(`WATCH`), 則在執行`discard` 也會自動取消監控 (`UNWATCH`)
    
    範例 : 
    
````
redis> MULTI
OK

redis> PING
QUEUED

redis> SET greeting "hello"
QUEUED

redis> DISCARD
OK
````
    
####4. WATCH    
    * 可用版本 : >= 2.2.0 
    
若在  `mulit` 之前下了 `watch key`的指令, 當 `exce`執行時候, 若 被監控`key`的值發生變動, 
則會阻止 此事務進行。
而 `watch`只保證能在事務執行時, 若被監控的值改動而事務部執行, 不將被監控的值上鎖, 其他用戶仍能改變被監控的值, 可以實現`樂觀鎖`
    
    範例 : 
````
redis> WATCH name #監控name的值
OK

redis> MULTI
OK

redis> SET name peter
QUEUED

redis> EXEC 
(nil)  #name的值被更動, 故執行失敗
````
    
####5. UNWATCH
此指令`無參數`, 取消`所有`被監控的KEY, 若事務被取消(`discard`), 則有等同效果, 無須再下此指令
````
redis> WATCH lock lock_times
OK

redis> UNWATCH
OK
````

- - - 
參考資料 : http://redisdoc.com/transaction/unwatch.html     
參考資料 : http://www.runoob.com/redis/redis-transactions.html  
參考資料 : https://www.jianshu.com/p/361cb9cd13d5       
參考資料 : https://redisbook.readthedocs.io/en/latest/feature/transaction.html  
    

    