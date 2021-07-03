

查看远程库的信息

```java
git remote
```

查看更详细的信息

```
git remote -v
```

### 创建版本库：

克隆版本库 git clone

```
git clone <版本库url> [本地目录名]
```

git clone 是将其他仓库克隆到本地，包括被 clone 仓库的版本变化，因此本地无需是一个仓库，且克隆将设置额外的远程跟踪分支。因为是克隆来的，所以 .git 文件夹里存放着与远程仓库一模一样的版本库记录，clone 操作是一个从无到有的克隆操作

如果不指定本地目录，则会在本地生成一个远程仓库同名的目录。

```javascript
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a
$ git clone https://github.com/dizhongdia/git-tips.git
Cloning into 'git-tips'...
remote: Enumerating objects: 59, done.
remote: Counting objects: 100% (59/59), done.
remote: Compressing objects: 100% (48/48), done.
remote: Total 59 (delta 26), reused 31 (delta 7), pack-reused 0
Unpacking objects: 100% (59/59), 19.96 KiB | 3.00 KiB/s, done.

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a
$ cd git-tips/

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/git-tips (main)
$ git remote -v
origin  https://github.com/dizhongdia/git-tips.git (fetch)
origin  https://github.com/dizhongdia/git-tips.git (push)

```

初始化本地版本库 git init

```javascript
git init
```

**远程操作：**

拉取远程更新并快速合并 git pull

git pull 是拉取远程分支更新到本地仓库再与本地分支进行合并，即：git pull = git fetch + git merge

```javascript
git pull <远程主机名> [远程分支名]:[本地分支名]
```

如果不指定分支名，会将远程的master分支拉取下来和本地当前分支合并。

```javascript
示例：
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/git-usage-training (main)
$ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 638 bytes | 2.00 KiB/s, done.
From https://github.com/dizhongdia/git-tips
   4db02aa..d236514  main       -> origin/main
Updating 4db02aa..d236514
Fast-forward
 6.html | 1 +
 1 file changed, 1 insertion(+)

```

初始化仓库并git pull远程仓库:

```javascript
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/git98
$ git init
Initialized empty Git repository in I:/JAVA_WAIT_TO_DELETE/a/git98/.git/

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/git98 (master)
$ git pull https://github.com/dizhongdia/git-tips.git
remote: Enumerating objects: 62, done.
remote: Counting objects: 100% (62/62), done.
remote: Compressing objects: 100% (50/50), done.
remote: Total 62 (delta 27), reused 31 (delta 7), pack-reused 0
Unpacking objects: 100% (62/62), 20.55 KiB | 3.00 KiB/s, done.
From https://github.com/dizhongdia/git-tips
 * branch            HEAD       -> FETCH_HEAD

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/git98 (master)
$ git push
fatal: No configured push destination.
Either specify the URL from the command-line or configure a remote repository us
ing

    git remote add <name> <url>

and then push using the remote name

    git push <name>

```
通过以上代码发现当使用pull时，push是不可以直接推送到远程的，需要先git remote add <name> <url>，fetch命令也是，和git clone有区别。

拉取远程代码 git fetch

方法一：

```javascript
git fetch <远程仓库名> <远程分支名> #从远程仓库的分支拉代码到本地
git log -p <本地分支名>.. <远程仓库名>/<远程分支名> #比较本地和远程的区别
git merge <远程仓库名>/<远程分支名>  #合并远程到本地
```

示例：

```javascript
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/git使用技巧 (main)
$ git fetch origin main
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 638 bytes | 2.00 KiB/s, done.
From https://github.com/dizhongdia/git-tips
 * branch            main       -> FETCH_HEAD
   4db02aa..d236514  main       -> origin/main

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/git使用技巧 (main)
$ git log -p main.. origin/main
commit d236514e1ba2b30dc85fc4ad750416e7c13ed17d (origin/main, origin/HEAD)
Author: youngma <46380119+dizhongdia@users.noreply.github.com>
Date:   Sun Jul 4 01:07:22 2021 +0800

    Update 6.html

diff --git a/6.html b/6.html
index e69de29..cefa0da 100644
--- a/6.html
+++ b/6.html
@@ -0,0 +1 @@
+1111111^M

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/git使用技巧 (main)
$ git merge origin/main
Updating 4db02aa..d236514
Fast-forward
 6.html | 1 +
 1 file changed, 1 insertion(+)

```

方法二：

```javascript
git fetch origin master:temp           #从远程的origin仓库的master分支下载到本地并新建一个分支temp
git diff temp                          #比较master分支和temp分支的不同
git merge temp                         #合并temp分支到master分支
git branch -d temp                     #删除temp
```

### 修改和提交
本来打算继续写的，但是因为个人对这些剩下的命令能够掌握，且写前面的文档浪费了<br>
不少时间，所以暂时搁置。<br>
   ![image](https://user-images.githubusercontent.com/46380119/124363360-5e812500-dc6d-11eb-95bf-dcb30aa3c34f.png)

   
