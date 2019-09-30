###Windows 下安裝php redis擴充套件

1. 印出 phpinfo 查看資訊
2. 至 [網頁](https://windows.php.net/downloads/pecl/releases/redis/5.0.1/) 下載 與phpinfo對應之zip檔案
   >Architecture => x86   
   >Compiler => MSVC14   
3. 再php.ini中加入:
     
       ;redis
       extension=php_igbinary.dll
       extension=php_redis.dll
       
4. 重啟wampserver, 若能在phpinfo()中能看到 redis, 代表擴展成功。