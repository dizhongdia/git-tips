**情景2:**
情景1更多是适用于个人开发的情况，实际上公司的开发更像是：公司建立远程版本库，你克隆到个人仓库，然后再克隆到本地，建立新分支，切换到该分支进行开发。具体的不同公司工作流程不一样。

以Git flow为例，公司远程仓库地址为XXX, 那么找到项目主仓库并fork到自己的空间，克隆到本地，新建feature分支用于开发新功能，开发自测，提交本地仓库，检查上游仓库（公司的项目仓库）是否有改动（先添加上游仓库，和它建立连接，然后再pull下来），然后可能涉及到代码冲突，要修正冲突，完毕后向上游仓库发起Merge Request，进行code review，有问题就修改，然后回撤提交，拉取请求以防远程仓库变动，再发起MR。MR通过后再合并代码到主仓库，然后可以删除本地分支，更新本地和origin代码。

远程：https://github.com/scutma/learn-to-git

自己fork的仓库：https://github.com/dizhongdia/learn-to-git.git

克隆到本地：

```java
语法规则：
git clone <url>
示例：
git clone https://github.com/dizhongdia/learn-to-git.git
结果：    
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a

$ git clone https://github.com/dizhongdia/learn-to-git.git

Cloning into 'learn-to-git'...

remote: Enumerating objects: 4, done.

remote: Counting objects: 100% (4/4), done.

remote: Compressing objects: 100% (4/4), done.

remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0

Unpacking objects: 100% (4/4), 884 bytes | 2.00 KiB/s, done.

```

![image](https://user-images.githubusercontent.com/46380119/124348030-43d19080-dc1a-11eb-85e3-e304f22caaf7.png)

进入项目并新建分支并切换到该分支进行开发：

```java
建立分支：
语法：
git branch <分支名>
切换分支:
语法：
git checkout <分支名>
切换到上一次的分支：
git checkout - 
建立分支并切换:
git checkout -b <分支名>

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a

$ cd learn-to-git/

 

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (master)

$ git branch feat-beauty

 

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (master)

$ git checkout feat-beauty

Switched to branch 'feat-beauty'
```

开发新功能，开发自测，提交本地仓库：

```java
语法：
1）添加到暂存区：
git add .
2）提交到本地的仓库作为一个版本：
git commit -m "版本说明"
版本说明格式最好统一，如功能命名为[feat:]开头，bug以[fix:]开头。
修复了issues可以附加fix #2关联并关闭issue
示例：
git add .
git commit -m "[feat:]新增美图功能，issue1开发完成,fix #1"
解析：
这样到时候提交会把issue1给关闭掉。

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (feat-beauty)

$ touch 1.html 2.html
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (master)

$ git add .
 

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (feat-beauty)

$ git commit -m "<feat>创建1，2.html实现了beauty功能"

[feat-beauty d03b705] <feat>创建1，2.html实现了beauty功能

 2 files changed, 0 insertions(+), 0 deletions(-)

 create mode 100644 1.html

 create mode 100644 2.html

```


检查上游仓库（公司的项目仓库）是否有改动（先添加上游仓库，和它建立连接，然后再pull下来）:

```java
添加上游仓库:
git remote add upstream <上游仓库url>
解析：
就是把上游仓库的url命名为upstream添加到本地，建立连接。
pull语法：
git pull upstream master --rebase
解析：master是上游仓库的主分支名，rebase可以避免本地多了merge commit。
示例：
git remote add upstream https://github.com/scutma/learn-to-git.git
git pull upstream master --rebase
结果：
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (feat-beauty)

$ git remote add upstream https://github.com/scutma/learn-to-git.git

 

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (feat-beauty)

$ git pull upstream master --rebase

remote: Enumerating objects: 4, done.

remote: Counting objects: 100% (4/4), done.

remote: Compressing objects: 100% (2/2), done.

remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0

Unpacking objects: 100% (3/3), 686 bytes | 0 bytes/s, done.

From https://github.com/scutma/learn-to-git

 \* branch      master   -> FETCH_HEAD

 \* [new branch]   master   -> upstream/master

Successfully rebased and updated refs/heads/feat-beauty.
```
![image](https://user-images.githubusercontent.com/46380119/124348043-59df5100-dc1a-11eb-831d-b0359e13ab17.png)

这个时候是有可能会出现冲突的，比如说你改了1.html,然后上游仓库也有人改了1.html并且成功提交到了上游，这个时候就会发生冲突。

这个时候再把公司的1.html的代码改一改，再同步一次看看，我觉得会冲突。

```java


mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (feat-beauty)

$ git pull upstream master --rebase

remote: Enumerating objects: 5, done.

remote: Counting objects: 100% (5/5), done.

remote: Compressing objects: 100% (2/2), done.

remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0

Unpacking objects: 100% (3/3), 730 bytes | 1024 bytes/s, done.

From https://github.com/scutma/learn-to-git

 \* branch      master   -> FETCH_HEAD

  4ffc738..e9c8417 master   -> upstream/master

Successfully rebased and updated refs/heads/feat-beauty.

```


结论：并没有冲突，上游的直接把我本地的覆盖了。因为公司的1.html可以说是v2.0，而我本地的还是v1.0，我自己也没有修改1.html的内容，所以没有冲突。

![image](https://user-images.githubusercontent.com/46380119/124348052-64014f80-dc1a-11eb-99f4-0aa271a5f2a8.png)

那么怎么样才会冲突呢？

公司再提交一次版本：![image](https://user-images.githubusercontent.com/46380119/124348060-6cf22100-dc1a-11eb-8418-d8f315d7c65c.png)

本地同时也修改1.html：![image](https://user-images.githubusercontent.com/46380119/124348064-711e3e80-dc1a-11eb-8459-b51d96c16f99.png)
```java
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/a/learn-to-git (feat-beauty)

$ git pull upstream master --rebase

remote: Enumerating objects: 5, done.

remote: Counting objects: 100% (5/5), done.

remote: Compressing objects: 100% (3/3), done.

remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0

Unpacking objects: 100% (3/3), 758 bytes | 2.00 KiB/s, done.

From https://github.com/scutma/learn-to-git

 \* branch      master   -> FETCH_HEAD

  d975d7c..9a4916a master   -> upstream/master

error: could not apply fe5c16f... <feat>往1上面加了一行代码

Resolve all conflicts manually, mark them as resolved with

"git add/rm <conflicted_files>", then run "git rebase --continue".

You can instead skip this commit: run "git rebase --skip".

To abort and get back to the state before "git rebase", run "git rebase --abort"

.

Could not apply fe5c16f... <feat>往1上面加了一行代码

Auto-merging 1.html

CONFLICT (content): Merge conflict in 1.html
```
![image](https://user-images.githubusercontent.com/46380119/124348097-97dc7500-dc1a-11eb-9bd9-fc3952813748.png)
