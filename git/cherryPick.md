## Cherry-Pick
### 分支commit 挑選 合併 
切換到要合併的branch上   
並下以下指令
````
git cherry-pick COMIT編號
````
>也可以一次檢好幾個commit
>````
>git cherry-pick COMIT編號1 COMIT編號2 COMIT編號3
>````

###檢過來但先不合併
######使用 --no-commit參數
````
git cherry-pick COMIT編號 --no-commit
````

---

### ㄋ在gitLab

1. 要檢取的commit 內 
![GITHUB]( http://larrynung.github.io/2018/11/28/GitLab-Cherry-pick-changes/1.png "圖片名稱")

2. 點選左上方 Options 選單並選取 Cherry-pick 選單選項。
![GITHUB]( http://larrynung.github.io/2018/11/28/GitLab-Cherry-pick-changes/2.png "圖片名稱")

3. 在 Cherry-pick this commit 對話框中選取要 merge 到的 branch，如果要發送 Merge request 可勾選下方的 Start a new merge request with these changes 勾選框，最後按下下方的 Cherry-pick 按鈕。
![GITHUB]( http://larrynung.github.io/2018/11/28/GitLab-Cherry-pick-changes/3.png "圖片名稱")

>如果沒有勾選 Start a new merge request with these changes 勾選框，則 Cherry-pick 會立即 merge。  
>如果有勾選，則會走回一般 Merge request 的流程

---
資料來源 : [【狀況題】如果你只想要某個分支的某幾個 Commit？](https://gitbook.tw/chapters/faq/cherry-pick.html)    
資料來源 : [GitLab - Cherry-pick changes](http://larrynung.github.io/2018/11/28/GitLab-Cherry-pick-changes/)

