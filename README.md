# Git使用教程
### 环境说明：
已经下载了Git并且配置好了本地环境变量，windows下鼠标右键有Git GUI和Git Bash如图
![image](https://user-images.githubusercontent.com/46380119/124349630-ab8bd980-dc22-11eb-8571-8cae2a1f05aa.png)    
**Git下载地址:** https://git-scm.com/downloads    
**环境变量的作用**：就是你在cmd下可以直接使用git的命令，不配也行，因为主要就是在Git Bash下进行操作，Bash顾名思义，使用的就是linux命令。<br>
**环境变量配置方法：**<br>
![image](https://user-images.githubusercontent.com/46380119/124349964-5cdf3f00-dc24-11eb-9d47-ac54fa23c31e.png)   
![image](https://user-images.githubusercontent.com/46380119/124350125-6b7a2600-dc25-11eb-9db0-b1c5ecb11fb4.png)   
![image](https://user-images.githubusercontent.com/46380119/124350145-7c2a9c00-dc25-11eb-8324-4a18a446c3d5.png)     
![image](https://user-images.githubusercontent.com/46380119/124350177-a3816900-dc25-11eb-82fd-9dc5f9139213.png)   
双击Path进入，点击新建： <br>    
![image](https://user-images.githubusercontent.com/46380119/124350202-d166ad80-dc25-11eb-8bfe-63b17f5f7b4a.png)    
![image](https://user-images.githubusercontent.com/46380119/124350210-df1c3300-dc25-11eb-828c-eab2c29a85fe.png)    
最后记得确定：![image](https://user-images.githubusercontent.com/46380119/124350222-ff4bf200-dc25-11eb-9029-fb1831c3f50f.png)    

查看配置：   
在任意文件夹下右键打开Git Bash Here     
git config --global -l	查看个人配置
git config -l 查看全部配置     
个人配置文件名为：.gitconfig    
![image](https://user-images.githubusercontent.com/46380119/124350328-aaf54200-dc26-11eb-9b0b-91abd48acb3f.png)   
可以通过命令行或者编辑器直接编辑配置文件来修改配置以达到某些目的如乱码，代理，免验证。   

本地免登陆方法：
一种是通过SSH密钥认证，一种是HTTPS通信协议。
SSH密钥认证：
1.	确认一下自己是否已经拥有密钥了，默认情况下，用户的 SSH 密钥存储在其 ~/.ssh 目录下。
![image](https://user-images.githubusercontent.com/46380119/124350377-045d7100-dc27-11eb-89de-9497b7986a0b.png)

有的直接跳转到3。
2.	通过ssh-keygen 程序生成
ssh-keygen -t rsa -C "873048629@qq.com"
首先 ssh-keygen 会确认密钥的存储位置和文件名（默认是 .ssh/id_rsa）,然后他会要求你输入两次密钥口令，留空即可。所以一般选用默认，全部回车即可。
![image](https://user-images.githubusercontent.com/46380119/124350384-0c1d1580-dc27-11eb-9af3-07156b56c015.png)

![image](https://user-images.githubusercontent.com/46380119/124350386-0d4e4280-dc27-11eb-9fb1-a630ac59df6b.png)

3.	需要寻找一对 id_rsa 或 id_dsa 命名的文件，其中一个带 .pub 扩展名。 '.pub'文件是你的公钥，另一个则是私钥。
4.	接下来我们登陆到GitHub上，右上角小头像->Setting->SSH and GPG keys中，点击new SSH key。
![image](https://user-images.githubusercontent.com/46380119/124350389-14755080-dc27-11eb-898d-266552f915f3.png)

5.	Title：可以随便填写，但最好起的名字能让自己知道这个公钥是哪个设备的。
Key：将上面生成的.pub文件中的所有内容复制到这里。
点击下面的Add SSH key即可。
然后你就会发现可以免密码访问了
![image](https://user-images.githubusercontent.com/46380119/124350390-19d29b00-dc27-11eb-973a-f000616e5bf6.png)
HTTPS通信协议：
接下来讲一下越来越常用的HTTPS方式的免密码，就是在本地生成.git-credentials文件，添加用户账号密码，然后在git配置中添加配置使得git能访问到这个.git-credentials文件，相当于每次git会先访问.git-credentials去找密码，找到了就不需要我们输入密码了。这样的坏处就是密码是明码保存在本地的，如果是公司的电脑有一定的风险，github还提供了一种Personal access tokens的方法来支持免密登录，github会提供一个token，我们选择要赋予这个token的权限，复制token到本地并配置，就能够免密登录，可以在github上修改这个token 的权限（增加或者删除权限）。
特别说明：从 2021 年 8 月 13 日开始，我们将在 GitHub.com 上对 Git 操作进行身份验证时不再接受帐户密码。2021年8 月 13 日- 所有经过身份验证的 Git 操作都需要令牌（或 SSH 密钥）身份验证。
https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/
![image](https://user-images.githubusercontent.com/46380119/124350392-20611280-dc27-11eb-97ef-0da7789fce6b.png)
（1）	token方法
懒人一键直达：https://github.com/settings/tokens
或者右上角小头像->Setting->Developer settings->Personal access tokens
![image](https://user-images.githubusercontent.com/46380119/124350395-26ef8a00-dc27-11eb-87ca-6d6eacc309fa.png)
![image](https://user-images.githubusercontent.com/46380119/124350398-2951e400-dc27-11eb-842a-7eb82f12f245.png)

![image](https://user-images.githubusercontent.com/46380119/124350403-2bb43e00-dc27-11eb-9517-a7d14599bbb6.png)
生成成功后会有邮件，请妥善保管好 token
注意事项
to­ken 具有极高权限，请妥善保管。
请牢记 to­ken，不会再次显示了。如果第二次需要用，只能刷新 to­ken。
刷新 to­ken 后旧 to­ken 会失效。 
![image](https://user-images.githubusercontent.com/46380119/124350406-3242b580-dc27-11eb-95c6-707fde562a55.png)
任意Git Bash下输入代码：
git config --global credential.helper store
然后git push -u
弹出登录框后，输入用户名和密码（密码是刚刚复制的token）。![image](https://user-images.githubusercontent.com/46380119/124350412-38389680-dc27-11eb-8d1c-63a55cb35330.png)
![image](https://user-images.githubusercontent.com/46380119/124350414-3b338700-dc27-11eb-823e-3402888fbc58.png)

至此，免密输入就完成了。
在Personal access tokens中可以重新修改token的权限，以及要是忘了token，可以点击Regenerate token重心生成令牌，原来的令牌就会失效，需要重新更新。![image](https://user-images.githubusercontent.com/46380119/124350419-41296800-dc27-11eb-92ce-4b094055e3f7.png)
另外附上官方token创建文档：
https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-token

（2）	明码方法
废弃。
地址：.git-credentials

Git的作用：分布式版本管理，有其他的版本管理工具，但是Git比较先进。所谓的分布式就是没有“中央服务器”，每个人的电脑都是一个完整的版本库。

Git分支之工作流程：
除了简单的个人使用Git外，如果一个团队共同协作，如何分配好工作流程并使用适当的Git分支方式。
首先要定义分支：
	以master分支为例，每次提交代码，Git都会生成支点（或者说一个小版本），把它们串成一条时间线，这一次次的提交合成的时间线就是一个分支。
这个时候再新建一个分支dev，指向master相同的提交，同时把HEAD指向dev，那么当前使用的分支就是dev了，新的提交会提交到分支dev，master不变。
 
广泛使用的工作流程有三种：
Git flow
Github flow
Gitlab flow
1.	Git flow
Master用于存放对外发布的版本，dev分支用于开发，存放最新的开发版。
三种短期分支用于临时需要，使用完删除，分别是feature分支，命名feature-*，从dev上分出来用于开发某特定功能，开发完并入dev；
release分支，命名release-*，预发版本，从dev上分出来，进行发布前版本测试，结束之后并入dev和master。
Hotfix分支，命名fixbug-*，从master上分出来，修复bug再合并进master和dev。
流程清晰，但是相对复杂，长期要维护两个分支，还要经常切换到dev分支，因为master往往是默认分支。
2.	Github flow
特点：只有一个master长期分支，有新的需求就拉新的分支，不区分功能或补丁，新分支开发完成就pull request请求合并，审核通过就合并并删除新分支。
3.	Gitlab flow（不太理解）
git flow把master当版本分支，github把master当作开发分支，gitlab合并了。
公司有个a项目，你是xyz，流程为：
Fork项目到自己的空间；
克隆到本地，并创建新的分支用于开发新功能；
开发并测试完成，提交到本地仓库；
看上游版本是否有改动，有的话拉取到本地，有可能代码冲突，那就还要修改代码或者协商解决冲突；
发起pull request。




.gitignore:

![image](https://user-images.githubusercontent.com/46380119/124350432-51d9de00-dc27-11eb-9cb3-caf7cbb86653.png)
vpn下如何git:
![image](https://user-images.githubusercontent.com/46380119/124350435-57372880-dc27-11eb-8419-00ddc650c2e2.png)
fatal: unable to access 'https://github.com/wxler/test.git/': OpenSSL SSL_connect: Connection was reset in connection to github.com:443
方案二
如果你开启了VPN，很可能是因为代理的问题，这时候设置一下http.proxy就可以了。

一定要查看自己的VPN端口号，假如你的端口号是7890，在git bash命令行中输入以下命令即可：

git config --global http.proxy 127.0.0.1:7890
git config --global https.proxy 127.0.0.1:7890
1
2
如果你之前git中已经设置过上述配置，则使用如下命令取消再进行配置即可：

git config --global --unset http.proxy
git config --global --unset https.proxy

origin是怎么来的：
![image](https://user-images.githubusercontent.com/46380119/124350441-64541780-dc27-11eb-8e6d-3897d9f4e580.png)

创建仓库的时候，github会默认把远程版本库命名为origin，所以可以自行命名，比如
git remote add akai <url>，那么以后包含origin的命令要替换为akai。

情景模拟：
情景1：你在本地有一个项目，想对它进行版本管理。那么可以按以下流程操作：
在项目下鼠标右键打开Git Bash，输入命令如下：
初始化新版本库，在本地会创建一个.git文件夹
git init
把项目所有文件添加到版本库，不包括空目录
git add .
提交到版本库，我把一次提交称为一个“版本”
git commit -m “提交的信息，最好遵从一定的命名规范” 
本地版本库和远程版本库建立连接，把远程版本库命名为origin，默认是origin，当然
你可以命名为其他，但不建议
git remote add origin [url]
把本地版本库推入远程库
git push origin master 

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
![image](https://user-images.githubusercontent.com/46380119/124348192-1a653480-dc1b-11eb-8995-52280a593e3f.png)

![image](https://user-images.githubusercontent.com/46380119/124348052-64014f80-dc1a-11eb-99f4-0aa271a5f2a8.png)

那么怎么样才会冲突呢？

公司再提交一次版本：![image](https://user-images.githubusercontent.com/46380119/124348060-6cf22100-dc1a-11eb-8418-d8f315d7c65c.png)

本地同时也修改1.html：![image](https://user-images.githubusercontent.com/46380119/124348064-711e3e80-dc1a-11eb-8459-b51d96c16f99.png)
再次执行上游同步：
```java
语法：
git pull upstream master --rebase
结果：
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
![image](https://user-images.githubusercontent.com/46380119/124348250-73cd6380-dc1b-11eb-9f14-fb60283c8b88.png)
出现了版本冲突，其中<<<<到====之间是上游版本的内容，而===到>>>>是本地的内容，可以选择保留某一个来解决冲突，或者撤销这一次的同步操作，或者跳过提交。
比如上游v1.0和本地v1.0是同步的，上游当前是v2.0，本地当前是v2.0，都对1.html进行更改了，   
那么当进行同步的时候，会出现冲突，解决冲突的一个逻辑是：此时本地的分支会切换到本地v1.0来进行和上游v2.0的一个抉择（不只是冲突的文件，是本地所有文件都会回到v1.0没冲突的版本，git log查看可知），抉择完毕再进行本地v2.0和上游v2.0的抉择。
```
Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".
(fix conflicts and then run "git rebase --continue")
(use "git rebase --skip" to skip this patch)
(use "git rebase --abort" to check out the original branch)

```
a)解决冲突：保留要的内容，然后执行命令：
```java
git add .
git rebase --continue
```
b)不解决冲突，把冲突的文件变回原样给我。
```
git rebase --abort
```
版本同步完毕，将分支推送给origin（origin是自己fork的仓库名字）：
```java
git push origin <分支名字>
示例：
git push origin feat-beauty
```
完成后在github上向上游仓库发起Pull Request，请同事进行coding review。
如果代码有问题，则修改，修改完成后：
```java
git add .
git commit --amend 
git push origin feat-beauty -f

解析：git commit --amend 是增补提交，不会产生新的提交记录，可以用git commit -amend -m "修改信息"修改上一次提交的信息，
提交到fork的仓库需要-f来强制合并。
```
PR通过后再合并代码到主仓库，然后可以删除本地分支:
```java
语法：
git checkout master
git branch -D feat-xxx
git push origin :feat-xxx
解析：
切换到主分支，删除本地功能分支，删除origin功能分支。
示例：
git checkout master
git branch -D feat-beauty
git push origin :feat-beauty
```

更新本地和origin代码。
```java
语法:
git pull upstream master --rebase
git pull origin master
```
乱码问题：
gitk中文乱码问题，也是修改.gitconfig的配置解决：
法1）直接编辑器打开
 
法2）git config --global gui.encoding utf-8
CMD乱码问题：
https://lanlan2017.github.io/blog/4f38856c/
https://blog.csdn.net/quzhongxin/article/details/45336333


更多的git学习资源推荐：
Github上高收藏资源，列举了常用的 Git 命令和一些小技巧，还有脑图。
https://github.com/521xueweihan/git-tips
gitee上的git大全：
https://gitee.com/all-about-git
gitee上的通过游戏巩固git：
https://oschina.gitee.io/learn-git-branching/

github上的脑图，很喜欢这个格式，可以包含非常多的信息，以前我自己用脑图使用默认的格式经常是一个个的格子，放的信息少，而且还难看。
这个脑图个人切片并标注了，原始版来源：https://github.com/521xueweihan/git-tips/blob/master/assets/git.png
![1](https://user-images.githubusercontent.com/46380119/124350492-99f90080-dc27-11eb-8df2-1da24530cc5b.png)
![2](https://user-images.githubusercontent.com/46380119/124350494-9b2a2d80-dc27-11eb-8f56-1eaeed1c755c.png)
![3](https://user-images.githubusercontent.com/46380119/124350497-9c5b5a80-dc27-11eb-9e42-83b546068fe1.png)
![4](https://user-images.githubusercontent.com/46380119/124350502-9ebdb480-dc27-11eb-96bc-37bb6904d199.png)

