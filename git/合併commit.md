## 合併多個commit
######本機
先查看commit 紀錄

```
    $ git -log
```

>````
>commit 95f875fd32af2a12cd10cf5f82698e4zzzzzzzz (HEAD -> issue29)
>Author: Ryan <mail>
>Date:   Thu Jun 13 09:31:59 2019 +0800
>
>    modify : codingStyle修改
>    issue #29
>
>commit d37aa6872f64c1bce50d12a672600c7zzzzzzzz (origin/issue29)
>Author: Ryan <mail>
>Date:   Wed Jun 12 15:21:31 2019 +0800
>
>    modify : codingStyle調整
>    issue #29
>
>commit 580bd87cfd56485300dbcac5b691cab3zzzzzzzz
>Author: Ryan <mail>
>Date:   Wed Jun 12 14:45:17 2019 +0800
>
>    feat : 後台違規車輛列表添加違規時間挑選條件
>    issue #29
>
>````

看到有兩個codingStyle  
若想要將他們合併成一個 commit  
請下指令

```
    $ git git rebase -i HEAD~2
```

 我們會看到以下畫面
 
> ````
>pick d37aa687 modify : codingStyle調整
>pick 95f875fd modify : codingStyle修改 issue #29
>
># Rebase 580bd87c..95f875fd onto 580bd87c (2 commands)
>#
># Commands:
># p, pick <commit> = use commit
># r, reword <commit> = use commit, but edit the commit message
># e, edit <commit> = use commit, but stop for amending
># s, squash <commit> = use commit, but meld into previous commit
># f, fixup <commit> = like "squash", but discard this commit's log message
># x, exec <command> = run command (the rest of the line) using shell
># b, break = stop here (continue rebase later with 'git rebase --continue')
># d, drop <commit> = remove commit
># l, label <label> = label current HEAD with a name
>````
>>(commit 是由舊到新排列)
>
>除了第一個commit 將其他的pick 改成 s(或 squash)   
>
>````
>pick d37aa687 modify : codingStyle調整
>s 95f875fd modify : codingStyle修改 issue #29
>
># Rebase 580bd87c..95f875fd onto 580bd87c (2 commands)
>#
># Commands:
># p, pick <commit> = use commit
># r, reword <commit> = use commit, but edit the commit message
># e, edit <commit> = use commit, but stop for amending
># s, squash <commit> = use commit, but meld into previous commit
># f, fixup <commit> = like "squash", but discard this commit's log message
># x, exec <command> = run command (the rest of the line) using shell
># b, break = stop here (continue rebase later with 'git rebase --continue')
>
>````

 保存後退出會到編輯commit message的地方
>````
># This is a combination of 2 commits.
># This is the 1st commit message:
>
>modify : codingStyle調整
>
>issue #29
>
># This is the commit message #2:
>
>modify : codingStyle修改
>issue #29
>
># Please enter the commit message for your changes. Lines starting
># with '#' will be ignored, and an empty message aborts the commit.
>#
># Date:      Wed Jun 12 15:21:31 2019 +0800
>#
># interactive rebase in progress; onto 580bd87c
># Last commands done (2 commands done):
>
>````
>
>在第一個更新想要留的message內容
>
>````
># This is a combination of 2 commits.
># This is the 1st commit message:
>
>modify : 合併後的commit
>
>issue #29
>
># This is the commit message #2:
>
># Please enter the commit message for your changes. Lines starting
># with '#' will be ignored, and an empty message aborts the commit.
>#


 儲存退出後查看log

>````
>$ git log
>commit b7a8144635c6b63dc9e5d426cc3bd322zzzzzzzz (HEAD -> issue29)
>Author: Ryan <mail>
>Date:   Wed Jun 12 15:21:31 2019 +0800
>
>    modify : 合併後的commit
>
>    issue #29
>
>commit 580bd87cfd56485300dbcac5b691cab3zzzzzzzz
>Author: Ryan <mail>
>Date:   Wed Jun 12 14:45:17 2019 +0800
>
>    feat : 後台違規車輛列表添加違規時間挑選條件
>
>    issue #29
>````

###完成! 

-------
######遠端
若要推到遠端  
請下指令

```
    $ git push -f
```

**請勿使用git pull 或 git push**   
**否則前面的做的都會功虧一簣**
