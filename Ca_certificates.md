#### 提供PHP 模擬 SSL  
    
1. 下載CA憑證   
    https://curl.haxx.se/docs/caextract.html
      
2. 複製檔案到PHP安裝目錄中  
    可以放在任意位置
>C:\php-7\extras\ssl\cacert.pem
    
3. PHP.ini啟用 mod_ssl 模組     
    將php.ini檔案內 `; extension=php_openssl.dll` 前的 ; 移除
4. 設定cacert.pem
    在 PHP.ini  中查找 curl.cainfo  及 openssl.cafile  這兩行
    填入 **步驟2** cacert.pem 的絕對路徑，和上一個步驟一樣，前方有分號請移除分號，如果找不到這兩行請自行添加

5. 重起php服務  
 `php -S 127.0.0.1:8401`
 
 
 - - - 
 參考資料 : https://vector.cool/fix-curl-error-ssl-certificate-problem-unable-to-get-local-issuer-certificate/
