#### axios檔案上傳範例           
  html
  
  ```
  <input type="file" id="input" onchange="uploadFile(this.files)">
  ```
  
  js      
  
  ```
  function uploadFile(files){
  const selectedfile = files[0];
  const fd = new FormData();
  fd.append('file', new Blob([selectedFile]));
  axios.post('/uploadFileAPI', fd , {
    headers: { 'Content-Type': 'multipart/form-data' },
    transformRequest: [(data, headers) => data], //預設值，不做任何轉換
  });
}
  ```
      
 - - - 
 參考資料 : https://yuugou727.github.io/blog/2018/03/04/axios/
