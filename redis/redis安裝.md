## Redis 安裝

#### Windows

1. 點擊下列下載網址下載, 並執行安裝檔  
下載網址: [請按此](https://github.com/microsoftarchive/redis/releases)
2. 安裝完後, 打開CMD 切換至 Redis安裝位置 (C:\Program Files\Redis) 執行指令

        redis-server.exe redis.windows.conf

    (可以把redis的路徑加入到系統的環境變量 `redis.windows.conf` 即可省略)   
  
3. 沒錯誤的話再開啟一個窗口, 原來的不要關閉, 並切換到新的窗口並切換到redis目錄下運行

       redis-cli.exe -h 127.0.0.1 -p 6379

``
- - -
#### Ubuntu 下安装
1. 在 Ubuntu 系统安装 Redis 可以使用以下命令:

        $sudo apt-get update
        $sudo apt-get install redis-server
        
2. 啟動Redis

        $ redis-server
        
3. 查看Redis是否啟動

        $ redis-cli

redis 127.0.0.1:6379>
 >127.0.0.1 是本机 IP ，6379 是 redis 服务端口。现在我们输入 PING 命令。
 
        redis 127.0.0.1:6379> ping
        PONG
 
*以上说明我们已经成功安装了redis。*

#### Redis配置 請至[網址](http://www.runoob.com/redis/redis-conf.html)參考

---
參考資料   
http://www.runoob.com/redis/redis-conf.html