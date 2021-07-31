# 練習git的專案
###### tags:`資策會-前端工程師就業養成班` `git`
## 介紹專案:
這個專案是我用來練習版本控制的專案，會說明怎麼安裝git及使用
### 什麼是版本控制？
版本控制系統 Version Control System (VCS)
版本控制（Version Control）是一种软体工程技巧，籍以在开发的过程中，确保由不同人所编辑的同一档案都得到更新。版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。主要分為三種:
* 本地版本控制系统
其中最流行的一种叫做 RCS，现今许多计算机系统上都还看得到它的踪影

* 集中化的版本控制系统（Centralized Version Control Systems，CVCS）
这类系统，诸如 CVS、Subversion 以及 Perforce 等，都有一个单一的集中管理的服务器

* 分散式版本控制系统（Distributed Version Control System， DVCS）
在这类系统中，像 Git、Mercurial、Bazaar 以及 Darcs 等，客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。

分散式相比于集中式的最大区别在于开发者可以提交到本地，每个开发者通过克隆（git clone），在本地机器上拷贝一个完整的Git仓库。

[資料來源: 版本控制系统Version Control System](https://www.jianshu.com/p/8cf7fa473028)

那我們的專案是使用git，因為git使用上非常普及，是工程師必備的基本能力之一。
### Git
Git是一款免费、开源的分布式版本控制系统，版本控制可以分一人或多人，基本上我們希望，將每一個檔案的不同的版本，都保存下來。

多人(團隊)版本控制，就會需要一個穩定版的版本，將他放在遠端github，個人的檔案會在本地端，這樣遠端有一個穩定版，個人本地端，由個人去撰寫程式，程式完成在放到遠端，供他人使用。



### 第一步 安裝 Git
確認電腦裡是否有安裝過 git:

```bash=
$ git --version
```
在 Windows 上面要安裝 Git 很簡單，只要去官網上面下載即可

[git下載](https://git-scm.com/)右邊 Downloads 點下去，一直下一步就好了
![](https://i.imgur.com/30Pvofx.png)

安裝完以後可以在桌面按右鍵，你會看到 git-bash點下去，打開git-bash後，試著輸入：`git --version `並且按 enter，看有沒有印出什麼訊息就知道是否成功了！
![](https://i.imgur.com/kJjydbO.png)

### 第二步 設定環境變數
#### 設定識別資料
在你安裝 Git 後首先應該做的事是設定使用者名稱及電子郵件。 這一點非常重要，因為每次 Git 的提交會使用這些資訊，而且提交後不能再被修改：
建議可以打 github 的帳號跟註冊的 email
```bash=
$ git config --global user.name "github 的帳號"
$ git config --global user.email "github 的email"
```

### 第三步 建立 repo
```bash=
# 在桌面建立檔案夾
$ mkdir git-workshop

# 進入該檔案夾
$ cd git-workshop

# 初始化 git 專案
$ git init

# 檢查看看是否有建立 .git 檔案夾
$ ls -al
# rm -r .git:不要版本控制
```
版本控制的狀態分為工作區、暫存區與儲存庫
![](https://i.imgur.com/hGK7bxd.png)
![](https://i.imgur.com/luUKlnD.png)

```bash=
# 建立一個檔案hello.txt

# 把檔案從 工作目錄 加到 暫存區
$ git add hello.txt

# 提交暫存區的檔案到儲存庫(repo)
$ git commit -m "紀錄這次提交的緣由"

# 查看紀錄
$ git log

```


---
### git add加入版本控制

```bash=
# 加入版本控制
$ git add <file>

# 全部加入檔案版本控制
$ git add .

# 回到上一個狀態(工作目錄區)不要版本控制(暫存區)
$ git rm --cached <file檔案名稱>
```
### git commit新建一個新版本
```bash=
# 新建一個版本，會進入vim視窗，編輯敘述:q退出
$ git commit

# 新建一個版本，並加入敘述(一定要先add)
$ git commit -m"敘述"

# 加入版本控制跟新建一個版本 (不會包含新建立的檔案還是要git add .一次)
$ git commit -am"敘述"
一定要先git add . 才能 git commit -am "test"
```

### git log歷史紀錄
```bash=
# 看commitID跟歷史紀錄...
$ git log

# 簡短的歷史紀錄只會顯示7碼
$ git log --oneline

# 查看特定檔案的紀錄
$ git log a.txt
$ git log -p a.txt
$ git log --stat

# 可以搜尋關鍵字
$ git log --grep="delete"

# 查看內容是誰編寫的
$ git blame hello.txt

```
```bash=
# 從暫存區域回到工作目錄
$ git restore --staged {檔案名稱}
 
# 捨棄在工作目錄的改變(包括修改與刪除)
$ git restore {檔案名稱}
```
### git checkout回到過去
```bash=
# 回到某一個版本
$ git checkout <版本號>

# 回到 master 這個 branch 的最新版本
$ git checkout master
```

### .gitignore不要被控管的檔案
* .gitignore裡加的檔案名稱後，要Enter多留一行空行，用git status看時才會被忽略掉
```bash=
# 輸入不要被控管的檔案
$ touch .gitignore
$ vim .gitignore
```
### git diff看板本前後的差別
```bash=

$ git status

# 比較檔案的差異    確認後，可以按 q 離開
$ git diff

$ git add hello.txt

$ git commit -m "add 2222"

$ git status

# 同時 add 跟 commit，只有針對已經 tracked 檔案才有效
$ git commit -am "delete 1 and add 3"

$ git log

```

移除檔案：
```bash=
# 從 git 中移除，且真的移掉檔案
$ git rm {檔案名稱}

# 從 git 中移除，但是檔案還在，仍保留硬碟中的檔案
$ git rm --cached {檔案名稱}
```

1. 直接刪除(rm)檔案，git add -> 把這個刪除的動作加進去 git 裡
2. git rm = 刪除 + git add這個刪除的動作
### Git 基本指令複習
|  |動作|指令|
| -------- | -------- | -------- |
|第零步|初始化|git init|
|第一步|建立.gitignore忽略不要的檔案|touch .gitignore|
|第二步|將所有檔案加入版本管理|git add .|
|第三步|版本控制的狀態|git status|
|第四步|建立第一個commit|git commit -m"first commit"|
|第五步|看commitID跟歷史紀錄|git log|
|第六步|修改檔案後commit (不會包含新建立的檔案)還是要git add .一次|git commit -am"second commit"|
|第七步|看commitID跟歷史紀錄...有兩個版本|git log|
|第八步|回到某個版本|git checkout <commitID>|

|動作|指令|
| -------- | -------- |
|建立分支|git branch <branch-name>|
|查看分支|git branch -v|
|刪除分支|git branch -d <branch-name>|
|切換分支|git checkout <branch>|
|合併分支|git merge <branch>|
|同步資料push更新GitHub與本地端同步|git push origin <branch>|
|同步資料pull更新本地端與GitHub同步|git pull origin master|