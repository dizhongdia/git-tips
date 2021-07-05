# 用 Angular 规范来约束 git 提交

## 背景

知乎上有个问题: [如何写好 Git commit log?](https://www.zhihu.com/question/21209619/answer/257574960) 很有意思, 能看到各种提交风格: 有用 emoji 的, 有用唐诗的, 有用随机生成的. 风格没有对错, 只要能够体现出 commit 所做的修改即可.

但是最让我印象深刻的是 @李华桥 的答案:

> 这种东西，当然要借助工具了，才能够写得即规范，又格式化，还能够支持后续分析。
> 目前比较建议的是，使用终端工具 [commitizen/cz-cli](https://link.zhihu.com/?target=https%3A//github.com/commitizen/cz-cli) + [commitizen/cz-conventional-changelog](https://link.zhihu.com/?target=https%3A//github.com/commitizen/cz-conventional-changelog) + [conventional-changelog/standard-version](https://link.zhihu.com/?target=https%3A//github.com/conventional-changelog/standard-version) 一步解决提交信息和版本发布。
> 甚至，如果想更狠一点，在持续集成里面加入 [marionebl/commitlint](https://link.zhihu.com/?target=https%3A//github.com/marionebl/commitlint) 检查 commit 信息是否符合规范，也不是不可以。

> 摘自[优雅的提交你的 Git Commit Message](https://zhuanlan.zhihu.com/p/34223150)

现在业界用的最多的就是Angular团队使用的规范，本文通过使用[cz-cli](https://github.com/commitizen/cz-cli)工具代替 `git commit`，并遵循Angular团队使用的规范，来规范提交。主要介绍Angular团队使用的规范是什么（格式问题，它的规范是定义了一个怎么样的格式），怎么用（样例问题，有没有靠谱的例子啊），如何配置cz-cli，安装了cz-cli后模拟完整的规范提交流程。

## Angular 规范格式

### 提交格式规范：

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

**简要解析：**

> <type>(<scope>): <subject>

type为提交的类型，scope为提交的范围，哪个位置的文件改变了，可以看到，(<scope>)用()包起来了，表示是可选的，可以要或者不要在提交的时候说明位置，subject为提交的主题，当成标题来写。

> <BLANK LINE>

<BLANK LINE>意思是空行，表示上面的`<type>(<scope>): <subject>`写完之后，空一行。

> <body>

body为主体内容。

> <BLANK LINE>

空行

>/ <footer>

footer字面意思是注脚。

下面对规范的细节进行更详尽的解析：

**详细解析：**

### Type:

必须是以下其中之一：

- **feat**: feature的缩写，表示一个新的功能

- **fix**: 表示一个bug的修复

- **docs**: Documentation only changes，表示只是更改了文本内容

- **style**: 表示不影响代码含义的更改（空格、格式、缺少分号等）

- **refactor**: refactor意为重构，表示既不修复错误也不添加功能的代码更改

- **perf**: performance的缩写，表示提高性能的代码更改

- **test**: 表示添加缺失的测试或纠正现有的测试

- **chore**: 表示对构建过程的修改或者辅助工具和库的更改（例如文档生成工具）

### Scope:

范围用来指明本次提交作用于哪个方面。例如`$location`， `$browser`，`$compile`，`$rootScope`，`ngHref`，`ngClick`，`ngView`，等...

如果作用于不止一个方面，可以用*

### Subject:

理解为标题，是对于本次更改的简介描述。

当用英文提交时，遵循的规范为：

- 使用祈使句，现在时：“change”不是“changed”也不是“changes”
- 不要大写第一个字母
- 末尾没有点 (.)

### Body:

正文应包括改变的动机，并将其与以前的行为进行对比。

英文格式同样为祈使句。

### Footer:

放 Breaking Changes 或 Closed Issues。

Closed Issues很好理解，就是放关联的Issues或者关闭Issues；

Breaking Changes表示重大更改，因为官方文档



## 遵循Angular规范的提交的案例

github上Angular官方的Angular规范说明项目本身就遵循了规范，项目地址为[Angular团队使用的规范](https://github.com/angular/angular.js)。<br>

![image-20210706005917299](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706005917299.png)

![image-20210706004939734](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706005905356.png)

![image-20210706005105541](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706005105541.png)

![image-20210706005221227](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706005221227.png)

![image-20210706005346148](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706005346148.png)

[**AngularJS Git Commit Message Conventions**文档中的例子](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#heading=h.uyo6cb12dt6w)

![image-20210706010607419](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706010607419.png)

![image-20210706010710205](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706010710205.png)

## cz-cli配置

cz-cli配置方法分为全局配置和项目级配置。

全局配置就是一次配置好了之后在任意项目下输入特定代码即可完成提交。

### 全局配置

```
npm install -g commitizen cz-conventional-changelog

echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
```

代码解析：

> npm install -g commitizen cz-conventional-changelog

全局安装commitizen依赖并初始化cz-conventional-changelog适配器。

最浅显的就是命令执行完毕，在路径C:->users->XX用户->AppData->Roaming->npm->node_modules中会多了commitizen和cz-conventional-changelog两个文件夹。

**存在的疑惑：**是怎么和git相作用使得git cz生效的，package.json文件配置的含义。

疑惑解答参考：http://www.babyitellyou.com/details?id=60669c980a6c6440e056057b

> echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc

在路径C:->Users->XX用户下生成.czrc文件，并写入`{ "path": "cz-conventional-changelog" }`。

### 项目级安装

> 来源：[优雅的提交你的 Git Commit Message](https://zhuanlan.zhihu.com/p/34223150)

```bash
npm install -D commitizen cz-conventional-changelog
```

package.json中配置:

```json
"script": {
    ...,
    "commit": "git-cz",
},
 "config": {
    "commitizen": {
      "path": "node_modules/cz-conventional-changelog"
    }
  }
```

如果没有安装npm，如何安装npm以及合理配置达到下载速度快可参见另一篇文章或者自行查找资料。

至此，安装就完成了。



## 完整规范的提交流程

安装完成之后，使用 `git cz` 代替 `git commit`就可以了。

假设我们新建了一个1.html并实现了某些功能，那么规范流程如下：

```javascript
mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/11/git-tips (main)
$ touch 1.html

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/11/git-tips (main)
$ git add .

mayangwu@BAOMAGEGE MINGW64 /i/JAVA_WAIT_TO_DELETE/11/git-tips (main)
$ git cz
```

`git cz`之后，会弹出如下界面，

1.选择feat<br>

![image-20210706011502428](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706011502428.png)

2.scope输入*<br>

![image-20210706011623038](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706011623038.png)

3.subject输入增加了美图的功能<br>

![image-20210706011721749](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706011721749.png)

4.body输入过去没有美图功能，很真实，没人主动和我聊天；增加了美图功能，巴拉巴拉<br>![image-20210706012042322](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706012042322.png)



5.footer选择n<br>

![image-20210706012129808](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706012129808.png)

执行完毕

![image-20210706012200511](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706012200511.png)

输入`git push`

```
git push
```

![image-20210706012447607](C:\Users\mayangwu\AppData\Roaming\Typora\typora-user-images\image-20210706012447607.png)