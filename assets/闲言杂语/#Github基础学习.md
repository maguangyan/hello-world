# Github基础学习

## 一 熟悉github

### 1.  github特点

#### 1. 直接记录快照，而非差异比较

#### 2.近乎所有操作都是在本地执行 

因为本地磁盘有项目的完整历史，在没有网络的情况下我们可以在本地仓库进行工作和保存，等到有网络的时候再push到GitHub的仓库

#### 3.Git保证完整性

Git中所有数据在存储前都计算校验和，然后以校验和来引用。
Git数据库中保存的信息都是以文件内容的哈希值来索引，而不是文件名

#### 4.Git 一般只添加数据

我们可以随便浪 反正有所有的数据历史版本记录

#### 5. Git有三种状态

* committed（已提交） 
  
* modified （已修改）
  
* staged（已暂存）

引入三个概念 Working Directory（工作目录） Staging Area（暂存区域） Repository（Git 仓库）

基本的git工作流程如下：

1. git touch  _ file /vi _ file 创建文件_file或 对已有文件进行修改
  
2. git add  _file  把文件 _file的快照放入本地暂存区
  
3. git commit -m'这里是对此次提交的描述m文件'
### 2.  Github操作
***git命令行***

命令行模式下才能执行Git的所有命令   GUI软件的功能有限 
安装完 Git 应该做的第一件事就是设置你的用户名称与邮件地址：
`git config --global user.name "John Doe"`
`$ git config --global user.email johndoe@example.com`

再次强调，**如果使用了 `--global` 选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事情， Git 都会使用那些信息。** 当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有 `--global` 选项的命令来配置。

* **查看所有配置**
`git config --list`
![1570858526617](..\typora-pic\1570858526617.png)

* **查看某些配置**

`git config user.name`

![1570858725104](..\typora-pic\1570858725104.png)

* **找到Git命令的使用手册:**

`git help<verb>`

`git  <verb> --help`

`man git-<verb>`

比如想获得config命令的手册：

`git help config`

结果如下：![1570859257516](..\typora-pic\1570859257516.png)

## 二 获取Git仓库

### 1.获取Git仓库

1. #### 在现有目录里初始化仓库

·`git init`

`git add License`

`git commit m'initial project version'`

2. #### 克隆现有的仓库

`git clone url` url为你要克隆仓库的地址

如果想把克隆的仓库保存为自己想要的名字，则

`git clone url myName` 即在后面加上要修改为的名字

url 除了用https://协议 也可以使用SSH传输协议。这个稍后在服务器上搭建Git的时候再说

### 2.记录每次更新到仓库

工作目录的文件状态：已跟踪 未跟踪（即有没有同步到远程仓库）

 Git时文件的生命周期如下：

![Git 下文件生命周期图。](..\typora-pic\lifecycle.png)

 #### 1. 检查当前文件状态

可以使用git status 命令：

![1570861495827](..\typora-pic\1570861495827.png)

git status -s 可以查看状态报告的精简版本

git diff     通过文件补丁的格式显示具体哪些行为发生了改变  此命令比较的是工作目录中当前文件和暂存区域快照之间的差异， 也就是修改之后还没有暂存起来的变化内容。

#### 2.  跟踪新文件（添加文件到暂存区）并提交到本地仓库

使用git add _files 

_files 可以是文件名字也可以是文件路径   如果是文件夹的话 该命令就跟踪该文件夹下的所有文案路径

已经添加到本地仓库或添加到暂存区的文件在被修改后 都要重新使用add 命令重新添加到暂存区 然后使用commit 命令提交到本地仓库

**忽略文件** 

有些文件无需纳入Git的管理  当想忽略这些文件的时候 我们可以创建一个名为.gitignore的文件，列出要忽略的文件格式

`cat .gitignore //cat可以读取文件内容·`

![1570863385642](..\typora-pic\1570863385642.png)

第一行告诉 Git 忽略所有以 `.o` 或 `.a` 结尾的文件。一般这类对象文件和存档文件都是编译过程中出现的。 

第二行告诉 Git 忽略所有以波浪符（~）结尾的文件，许多文本编辑软件（比如 Emacs）都用这样的文件名保存副本。 此外，你可能还需要忽略 log，tmp 或者 pid 目录，以及自动生成的文档等等。 要养成一开始就设置好 .gitignore 文件的习惯，以免将来误提交这类无用的文件。

具体怎么匹配要忽略的文件有点复杂，GitHub 有一个十分详细的针对数十种项目及语言的 `.gitignore` 文件列表，可以在 <https://github.com/github/gitignore> 找到它.

#### 3.  提交到本地仓库(纳入版本管理)

使用`git commit -m'This is a changed'`进行提交  m后面的是对此次提交的描述

提交时记录的是放在暂存区域的快照。 任何还未暂存的仍然保持已修改状态，可以在下次提交时纳入版本管理。 每一次运行提交操作，都是对你项目作一次快照，以后可以回到这个状态，或者进行比较。

**跳过使用暂存区域**  ：

`git commit -a -m'This is a changed'`

这样提交前就不需要git add了

#### 4. 移除文件

操作：从暂存区移除>>提交

`rm _files`可以删除文件夹（工作目录）里面的文件

`git rm _files`  删除暂存区的文件

#### 5. 移动文件

`git mv file_from file_to`  给文件改名字

#### 4.撤销提交

` git commit --amend`

```console
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amen
```

最终你只会有一个提交——第二次提交将代替第一次提交的结果

##### 取消暂存的文件

`git reset HEAD _files`

```console
$ git reset HEAD CONTRIBUTING.md
Unstaged changes after reset:
M	CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
      
renamed:    README.md -> README
      
Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)
      
modified:   CONTRIBUTING.md
```
##### 撤消对文件的修改

如何方便地撤消修改——将它还原成上次提交时的样子（或者刚克隆完的样子，或者刚把它放入工作目录时的样子）

`git checkout --_files`

```console
$ git checkout -- CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
      
renamed:    README.md -> README
```

#### 5.使用远程仓库

`git remote`

```console
$ git remote
origin
```

如果你已经克隆了自己的仓库，那么至少应该能看到 origin ——这是 Git 给你克隆的仓库服务器的默认名字

也可以指定选项 `-v`，会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL。

```console
$ git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
```
 #####  添加远程仓库

运行 `git remote add <shortname> <url>` 添加一个新的远程 Git 仓库，同时指定一个你可以轻松引用的简写：

      ```console
      $ git remote
      origin
      $ git remote add pb https://github.com/paulboone/ticgit
      $ git remote -v
      origin	https://github.com/schacon/ticgit (fetch)
      origin	https://github.com/schacon/ticgit (push)
      pb	https://github.com/paulboone/ticgit (fetch)
      pb	https://github.com/paulboone/ticgit (push)
      ```

现在你可以在命令行中使用字符串 `pb` 来代替整个 URL

* ##### ==从远程仓库中抓取与拉取==

```console
git fetch [remote-name]
```
这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。
git fetch 与git pull的区别：
`git fetch` 命令会将数据拉取到你的本地仓库——它并不会自动合并或修改你当前的工作
`git pull` 命令会自动的抓取然后**合并**远程分支到当前分支

* ##### 推送到远程仓库

`git push [remote-name] [branch-name]`

比如当你想要将 master 分支推送到 `origin` 服务器时（再次说明，克隆时通常会自动帮你设置好那两个名字），那么运行这个命令就可以将你所做的备份到服务器：

```console
$ git push origin master
```
需要注意的是：*只有当你有所克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。 当你和其他人在同一时间克隆，他们先推送到上游然后你再推送到上游，你的推送就会毫无疑问地被拒绝。 你必须先将他们的工作拉取下来并将其合并进你的工作后才能推送。*
* 查看某个远程仓库

`git remote show [remote-name]` 
    

* ##### 远程仓库的移除与重命名

**重命名**可以使用`git remote rename`

```console
$ git remote rename pb paul
$ git remote
origin
paul
```

值得注意的是这同样也会修改你的远程分支名字。 那些过去引`pb/master` 的现在会引用 `paul/master`
 **移除**可以使用 `git remote rm`

```console
$ git remote rm paul
$ git remote
origin
```
####  6.  打标签

Git 可以给历史中的某一个提交打上标签，以示重要
    
* ##### 查看标签
  

列出已有的标签： `git tag`
    
```console
$ git tag
v0.1
v1.3
```

使用特定的模式查找标签：
    
如果只对 1.8.5 系列感兴趣，可以运行：`git tag -l 'v1.8.5*'` 

* ##### 创建标签
  

Git 使用两种主要类型的标签：轻量标签（lightweight）与附注标签（annotated）

轻量标签很像一个不会改变的分支——它只是一个特定提交的引用

附注标签是存储在 Git 数据库中的一个完整对象。 它们是可以被校验的；其中包含打标签者的名字、电子邮件地址、日期时间

**通常建议创建附注标签，这样你可以拥有以上所有信息；但是如果你只是想用一个临时的标签，或者因为某些原因不想要保存那些信息，轻量标签也是可用的。**

创建一个*附注标签*：

``` 
$ git tag -a v1.4 -m "my version 1.4
```

`-m` 选项指定了一条将会存储在标签中的信息。 如果没有为附注标签指定一条信息，Git 会运行编辑器要求你输入信息。

通过使用 `git show` 命令可以看到标签信息与对应的提交信息

创建一个*轻量标签*：（不需要使用 `-a`、`-s` 或 `-m` 选项，只需要提供标签名字）

```console
git tag v1.4-lw
```

**删除标签**：`git tag -d <tagname>`

**检出标签:**`git checkout 2.0.0 ` 查看某个标签所指向的文件版本

#### 7. Git别名

（类似于用户自定义命令）

```console
 git config --global alias.ci commit
```

这意味着，当要输入 `git commit` 时，只需要输入 `git ci`

## 三 Git分支

### 1.创建分支

> ```console
> $ git branch testing
> ```

这会在当前所在的提交对象上创建一个指针。



![两个指向相同提交历史的分支。](..\typora-pic\two-branches.png)





关于HEAD的特殊指针：

*HEAD指向谁谁就是工作目录*

在 Git 中，HEAD是一个指针，指向当前所在的本地分支（将 `HEAD` 想象为当前分支的别名）。 在本例中，你仍然在 `master` 分支上。 因为 `git branch` 命令仅仅 *创建* 一个新分支，并不会自动切换到新分支中去





![HEAD 指向当前所在的分支。](..\typora-pic\head-to-master.png)





使用 `git log` 命令查看各个分支当前所指的对象。 提供这一功能的参数是 `--decorate`

```console
$ git log --oneline --decorate
f30ab (HEAD, master, testing) add feature #32 - ability to add new
34ac2 fixed bug #1328 - stack overflow under certain conditions
98ca9 initial commit of my project
```

由结果可知，当前 “master” 和 “testing” 分支均指向校验和以 `f30ab` 开头的提交对象。

### 2.分支切换

使用 `git checkout` 命令即可切换到一个已存在的分支

```console
$ git checkout testing
```



![HEAD 指向当前所在的分支。](..\typora-pic\head-to-testing.png)

这样指向本地的HEAD指针就指向了刚创建的分支testing

如果我们再提交一次：

> ```console
> vim test.rb
> $ git commit -a -m 'made a change'
> ```


  ![HEAD 分支随着提交操作自动向前移动。](..\typora-pic\advance-testing.png)

如图所示，我们的`testing` 分支向前移动了，但是 `master` 分支却没有，它仍然指向运行 `git checkout` 时所指的对象

现在我们切换回 `master` 分支看看：

> ```console
> $ git checkout master
> ```

![检出时 HEAD 随之移动。](..\typora-pic\checkout-master.png)

这条命令做了两件事。 一是使 HEAD 指回 `master` 分支，二是将工作目录恢复成 `master` 分支所指向的快照内容。 也就是说，你现在做修改的话，项目将始于一个较旧的版本。 本质上来讲，这就是忽略 `testing` 分支所做的修改，以便于向另一个方向进行开发。

我们不妨再稍微做些修改并提交：

> ```console
> $ vim test.rb
> $ git commit -a -m 'made other changes'
> ```

![项目分叉历史。](..\typora-pic\advance-master.png)

现在，这个项目的提交历史已经产生了分叉

**而所有这些工作，我们需要的命令只有 `branch`、`checkout` 和 `commit`。**

### 3.合并分支

先切换到要合并的主分支上，然后再把其他分支合并进来：

> ```console
> $ git checkout master
> $ git merge hotfix
> ```

### 4.分支管理

`git branch` 命令不只是可以创建与删除分支。 如果不加任何参数运行它，会得到当前所有分支的一个列表：

> ```console
> $ git branch
>   iss53
> * master
>   testing
> ```

如果需要查看每一个分支的最后一次提交，可以运行 `git branch -v` 命令：

> ```console
> $ git branch -v
>   iss53   93b412c fix javascript issue
> * master  7a98805 Merge branch 'iss53'
>   testing 782fd34 add scott to the author list in the readmes
> ```

## 四 远程仓库引用

常见的做法是利用远程跟踪分支。

远程跟踪分支是远程分支状态的引用。 它们是你不能移动的本地引用，当你做任何网络通信操作时，它们会自动移动。 远程跟踪分支像是你上次连接到远程仓库时，那些分支所处状态的书签。

假设你的网络里有一个在 `git.ourcompany.com` 的 Git 服务器。 如果你从这里克隆，Git 的 `clone` 命令会为你自动将其命名为 `origin`，拉取它的所有数据，创建一个指向它的 `master` 分支的指针，并且在本地将其命名为 `origin/master`。 Git 也会给你一个与 origin 的 `master` 分支在指向同一个地方的本地 `master` 分支，这样你就有工作的基础。

![克隆之后的服务器与本地仓库。](..\typora-pic\remote-branches-1.png)

### 1.更新远程仓库引用

如果要同步你的工作，运行 `git fetch origin` 命令。 这个命令查找 “origin” 是哪一个服务器（在本例中，它是 `git.ourcompany.com`），**从中抓取本地没有的数据，并且更新本地数据库，移动 `origin/master` 指针指向新的、更新后的位置。**



![`git fetch` 更新你的远程仓库引用。](..\typora-pic\remote-branches-3.png)

### 2.向远程服务器推送一个公开的分支（用于一起工作）

先创建一个分支 ,然后推送到远程端：

> ```c++
> git branch branchName
> git checkout branchname
> git push origin branchName//origin为远程服务器端的名字
> ```

推送之后，下一次其他协作者从服务器上抓取数据时，他们会在本地生成一个远程分支 `origin/serverfix`

```CQL
$ git fetch origin
remote: Counting objects: 7, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/schacon/simplegit
 * [new branch]      serverfix    -> origin/serverfix
```

*要特别注意的一点是当抓取到新的远程跟踪分支时，本地不会自动生成一份可编辑的副本（拷贝）。 换一句话说，这种情况下，不会有一个新的 `serverfix` 分支——只有一个不可以修改的 `origin/serverfix` 指针。*

可以运行 `git merge origin/serverfix` 将这些工作合并到当前所在的分支。 如果想要在自己的 `serverfix` 分支上工作，可以将其建立在远程跟踪分支之上：

```console
$ git checkout -b serverfix origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

这会给你一个用于工作的本地分支，并且起点位于 `origin/serverfix`。

### 3.跟踪分支（类似于一个指针，指向其跟踪的分支>>上游分支）

从一个远程跟踪分支检出一个本地分支会自动创建所谓的“跟踪分支”（它跟踪的分支叫做“上游分支”）。 跟踪分支是与远程分支有直接关系的本地分支。 如果在一个跟踪分支上输入 `git pull`，Git 能自动地识别去哪个服务器上抓取、合并到哪个分支。

* 如果想要将本地分支与远程分支设置为不同名字，你可以轻松地使用上一个命令增加一个不同名字的本地分支：

```console
$ git checkout -b sf origin/serverfix
Branch sf set up to track remote branch serverfix from origin.
Switched to a new branch 'sf'
```

现在，本地分支 `sf` 会自动从 `origin/serverfix` 拉取。

* 设置已有的本地分支跟踪一个刚刚拉取下来的远程分支，或者想要修改正在跟踪的上游分支：

```console
$ git branch -u origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
```

* 查看设置的所有跟踪分支，可以使用 `git branch` 的 `-vv` 选项：

### 4.删除远程分支：

假设你已经通过远程分支做完所有的工作了——也就是说你和你的协作者已经完成了一个特性并且将其合并到了远程仓库的 `master` 分支（或任何其他稳定代码分支）。 可以运行带有 `--delete` 选项的 `git push` 命令来删除一个远程分支。 如果想要从服务器上删除 `serverfix` 分支，运行下面的命令：

```console
$ git push origin --delete serverfix
To https://github.com/schacon/simplegit
 - [deleted]         serverfix
```

基本上这个命令做的只是从服务器上移除这个指针。 Git 服务器通常会保留数据一段时间直到垃圾回收运行，所以如果不小心删除掉了，通常是很容易恢复的。

## 五  变基

在 Git 中整合来自不同分支的修改主要有两种方法：`merge` 以及 `rebase`。

你可以使用 `rebase` 命令将提交到某一分支上的所有修改都移至另一分支上，就好像“重新播放”一样。

![将 `C4` 中的修改变基到 `C3` 上。](..\typora-pic\basic-rebase-3.png)

eg:先使用rebase 把experient里面的修改c4 **续到**master上

```console
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
```

然后 合并:

```console
$ git checkout master
$ git merge experiment
```

![master 分支的快进合并。](..\typora-pic\basic-rebase-4.png)

变基也并非完美无缺，要用它得遵守一条准则：

**不要对在你的仓库外有副本的分支执行变基。**

## 六 服务器上的Git协议

## 七 Git工具

### 1. 储藏（存档）与清理

* 想要切换分支，但是还不想要提交之前的工作；所以使用stash将当前状态储藏。 将新的储藏推送到栈上，运行 `git stash`
  或 `git stash save`：

> ```
> $ git stash
> Saved working directory and index state \
>   "WIP on master: 049d078 added the index file"
> HEAD is now at 049d078 added the index file
> (To restore them type "git stash apply")
> ```
>
> 

*  要查看存档的东西，可以使用`git stash list`

> ```
> $ git stash list`
> `stash@{0}: WIP on master: 049d078 added the index file`
> `stash@{1}: WIP on master: c264051 Revert "added file_size"`
> `stash@{2}: WIP on master: 21d80a5 added number to log
> ```

* 重新打开存档

将刚刚储藏的工作重新应用：`git stash apply。` 如果想要应用其中一个更旧的储藏，可以通过名字指定它，像这样：`git stash apply stash@{2}`。 如果不指定一个储藏，Git 认为指定的是最近的储藏

* 删除栈上的存档

以运行 `git stash drop` 加上将要移除的储藏的名字来移除它

或者也可以运行 `git stash pop` 来*应用储藏然后立即从栈上扔掉它。*

* 存档的几种变种

 第一个非常流行的选项是 stash save 命令的 --keep-index 选项。 它告诉 Git **不要**储藏任何你通过 git add 命令**已暂存**的东西。

当你做了几个改动并只想提交其中的一部分，过一会儿再回来处理剩余改动时，这个功能会很有用。

*默认情况下，git stash 只会储藏**已经在索引**中的文件。 如果指定 --include-untracked 或 -u 标记，Git 也会储藏任何创建的未跟踪文件。*

* 从存档创建一个分支

如果在当前分支在某个时间存档了，但是又继续在这个分支工作了一段时间，，可能在重新应用工作时可能会有问题。 如果应用尝试修改刚刚修改的文件，你会得到一个合并冲突并不得不解决它。 如果想要一个轻松的方式来再次测试储藏的改动，可以运行 git stash branch 创建一个新分支，检出储藏工作时所在的提交，重新在那应用工作，然后在应用成功后扔掉储藏：

* 清理工作目录

 移除每一样东西并存放在栈中（比较安全的做法）：`git stash --all`

去除冗余文件或者清理工作目录：

使用 `git clean -f -d` 命令来移除工作目录中所有**未追踪的文件以及空的子目录**。 -f 意味着 强制 或 “确定移除”。

如果只是想要看看它会做什么，可以使用 *-n* 选项来运行命令（比较安全）

删除所有文件（包括.gitiignore文件中忽略的文件），可以使用-x命令

### 2.搜索

无论仓库里的代码量有多少，你经常需要查找一个函数是在哪里调用或者定义的，或者一个方法的变更历史。Git 提供了两个有用的工具来快速地从它的数据库中浏览代码和提交

* Git Grep

Git 提供了一个 grep 命令，你可以很方便地从提交历史或者工作目录中查找一个字符串或者正则表达式

> ```
>  git grep -n gmtime_r
> ```
>
> 

使用 --count 选项来使 Git 输出概述的信息，仅仅包括哪些文件包含匹配以及每个文件包含了多
少个匹配:(以搜索gmtime_r函数为例)

> ```
> $ git grep --count gmtime_r
> compat/gmtime.c:4
> compat/mingw.c:1
> compat/mingw.h:1
> date.c:2
> git-compat-util.h:2
> ```



看匹配的行是属于哪一个方法或者函数，可以传入 -p 选项:

> ```python
> $ git grep -p gmtime_r *.c
> date.c=static int match_multi_number(unsigned long num, char c, const char
> *date, char *end, struct tm *tm)
> date.c: if (gmtime_r(&now, &now_tm))
> date.c=static int match_digit(const char *date, struct tm *tm, int
> *offset, int *tm_gmt)
> date.c: if (gmtime_r(&time, tm)) {
> ```
>
> 

* Git 日志搜索

如果我们想找到 ZLIB_BUF_MAX 常量是什么时候引入的，我们可以使用 -S 选项来显示新增和删除该字
符串的提交。

> ```c#
> $ git log -SZLIB_BUF_MAX --oneline
> e01503b zlib: allow feeding more than 4GB in one go
> ef49a7a zlib: zlib can only process 4GB at a time
> ```

### 3. 合并冲突

做一次可能有冲突的合并前尽可能保证**工作目录是干净**的。 如果你有正在做的工作，要么提交到一个临时分支要么储藏它。 这样我们可以有撤销的机会 。

* **如果产生了合并冲突**，可以使用`git merge --abort` 来简单地退出合并。

`git merge --abort` 选项会尝试恢复到你运行合并前的状态。 但当运行命令前，在工作目录中有未储藏、未提交的修改时它不能完美处理，除此之外它都工作地很好。

* **合并的时候可以忽略某些不同**（比如空格问题）

默认合并策略可以带有参数，其中的几个正好是关于忽略空白改动的。 如果你看到在一次合并中有大量的空白问题，你可以简单地中止它并重做一次，这次使用 `-Xignore-all-space` 或 `-Xignore-space-change` 选项。 第一个选项忽略所有空白修改，第二个选项忽略任意 数量 的已有空白的修改。

```
$ git merge -Xignore-space-change whitespace
Auto-merging hello.rb
Merge made by the 'recursive' strategy.
 hello.rb | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

因为在本例中，实际上文件修改并没有冲突，*一旦我们忽略空白修改，每一行都能被很好地合并。*

因为在本例中，实际上文件修改并没有冲突，一旦我们忽略空白修改，每一行都能被很好地合并。

### 4. 撤销合并（已经提交成功但是想撤销这一操作）

* **修复引用**

如果这个不想要的合并提交只存在于你的本地仓库中，最简单且最好的解决方案是移动分支到你想要它指向的地方。 大多数情况下，如果你在错误的 git merge 后运行 git reset --hard HEAD~，这会重置分支指向。

* **还原提交**

```
$ git revert -m 1 HEAD
[master b1d8379] Revert "Merge branch 'topic'"
```

-m 1 标记指出 “mainline” 需要被保留下来的父结点。 当你引入一个合并到 HEAD（git merge topic），新提交有两个父结点：第一个是 HEAD（C6），第二个是将要合并入分支的最新提交（C4）。本例中，我们想要撤消所有由父结点 #2（C4）合并引入的修改，同时保留从父结点 #1（C4）开始的所有内容。有还原提交的历史看起来像这样：



![在 `git revert -m 1` 后的历史](..\typora-pic\undomerge-revert.png)

### 5.子模块

子模块允许你将一个 Git 仓库作为另一个 Git 仓库的子目录。 它能让你将另一个仓库克隆到自己的项目中，同时还保持提交的独立。



## 八 图形界面中的git

### 1.gitk和git-gui

* 调出gitk图形界面

`gitk` 是一个历史记录的**图形化查看器**

> ```
> gitk --all
> ```

![`gitk` 历史查看器。](..\typora-pic\gitk.png)

这张图看起来就和执行 `git log --graph` 命令的输出差不多；每个点代表一次提交，线代表父子关系，而彩色的方块则用来标示一个个引用。 黄点表示 HEAD，红点表示尚未提交的本地变动。 下方的窗口用来显示当前选中的提交的具体信息；评论和补丁显示在左侧，摘要显示在右侧。 中间则是一组用来搜索历史的控件。

* git gui

`git-gui` 则主要是一个用来**制作提交的工具**。 打开它的最简单方法也是从命令行启动

使用`git gui`命令后：

![`git-gui` 提交工具。](..\typora-pic\git-gui.png)

# Git命令随手记

## 操作性命令：

- 创建分支：

> `git branch iss53`

- 切换到当前分支：

> `git checkout iss53`

- 创建分支并切换到该分支(相当于上面两条指令的简写)：

> `git checkout -b iss53`



## 查看型命令：

- 查看分叉历史(不含当前时间段之后的分叉)：

> `git log oneline`

- 输出你的提交历史、各个分支的指向以及项目的分支分叉情况(最全):

> `git log --oneline --decorate --graph --all` 

![返回主页](https://www.cnblogs.com/skins/custom/images/logo.gif)

**一般 -i 命令是交互模式命令i**

## git的一些常用命令



## **一般配置**

```
git --version //查看git的版本信息
git config --global user.name //获取当前登录的用户
git config --global user.email //获取当前登录用户的邮箱
```

## 登录git

```
/* 如果刚没有获取到用户配置，则只能拉取代码，不能修改  要是使用git，你要告诉git是谁在使用*/
 
git config --global user.name 'userName'    //设置git账户，userName为你的git账号，
git config --global user.email 'email'
```

## 创建一个文件夹

```
mkdir nodejs    //创建文件夹nodejs
cd nodejs       //切换到nodejs目录下
```

## 初始化git仓库

```
git init //在nodejs文件夹下初始化一个仓库，此时文件里会到一个.git的隐藏文件夹
```

## 创建忽略文件

```
touch .gitignore    //不需要服务器端提交的内容可以写到忽略文件里
    /*
        .git
        .idea
    */
```

## 查看当前文件夹下的文件目录

```
ls -al
```

## 创建文件并写入内容

```
echo "hello git" > index.html       //将'hello git' 写入到index.html中
//单个>箭头表示写入， >>表示追加
```

## 查看文件内容

```
cat index.html
```

## 增加到暂存区中

```
git add index.html
git add -A      //全部添加到缓存区
git add .      //全部添加到缓存区
```

## 增加到版本库中

```
git commit -m '备注信息'       //如果不加-m则会进入vim编辑器模式来填写备注信息 
git commit -am "备注信息"    //-am相当于git add . +git commit -m "备注信息"（不适用于新增文件）
```

## 查看版本

```
git log --oneline
```

## 比较差异

```
git diff //比较的是暂存区和工作区的差异

git diff --cached //比较的是暂存区和历史区的差异

git diff master //比较的是历史区和工作区的差异（修改）
```

## 撤回内容

(如果修改了工作区的文件后发现改错了，可以用暂存区或者版本库里的文件替换掉工作区的文件)

```
git checkout index.html //用暂存区中的内容或者版本库中的内容覆盖掉工作区

git reset HEAD index.html //取消增加到暂存区的内容（添加时）
```

## 显示目录的修改文件列表

```
git status
```

## 删除本地文件

```
rm fileName
```

## 删除暂存区

```
git rm index.html --cached //使用--cached 表示只删除缓存区中的内容
```

## 回滚版本

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
git reset --hard HEAD/commit_id //回滚最近的一个版本 git log
//回退命令：

git reset --hard HEAD^         //回退到上个版本
git reset --hard HEAD~3        //回退到前3次提交之前，以此类推，回退到n次提交之前
git reset --hard commit_id     //退到/进到 指定commit的sha码

//强推到远程：
git push origin HEAD --force

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

## 回滚到未来

```
git reflog

```

# 分支管理

## 创建分支

```
git branch dev

```

## 切换分支

```
git checkout dev

```

## 创建分支并切换分支

```
git checkout -b dev

```

## 删除分支

```
git branch -d dev

```

## 在分支上提交新的版本

```
git commit -a -m 'dev1'

```

## 合并分支

```
git merge dev

```

## 分支的合并后显示log

```
git log --oneline --graph --decorate

```

## 在分支开发的过程中遇到其他问题需要切换其他分支

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//保留写好的内容在切换到主干

git stash //保留内容

git stash apply //在次切换分之后需要应用一下保留的内容

git stash drop //丢掉保存的内容

git stash pop //使用并丢掉

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

## 合并分支把树杈掰到主干上

```
git rebase

```

# 添加远程的仓库

### push -u

-u参数 upstream

```
git push origin master -u   //获取最新代码

```

## 连接远程仓库

```
git remote add origin 仓库的地址

```

## 查看远程仓库

```
git remote -v

```

## 删除远程仓库

```
git remote rm origin

```

 

 

# git常用命令

### 安装及配置：

- Ubuntu下安装：`sudo apt-get install git`
- 配置用户名：`git config --global user.name "你的名字"`
- 配置e-mail：`git config --global user.email "你的邮箱@xx.com"`

### 与添加有关的：

- 将当前目录变为仓库：`git init`
- 将文件添加到暂存区：`git add 文件名 [可选：另一个文件名]`
- 将暂存区提交到仓库：`git commit –m "描述"`

### 与查询有关的：

- 查询仓库状态：`git status`
- 比较文件差异（请在git add之前使用）：`git diff 文件名`
- 查看仓库历史记录(详细)：`git log`
- 查看仓库历史记录(单行)：`git log --pretty=oneline` 或 `git log --oneline`
- 查看所有版本的commit ID：`git reflog`

### 与撤销有关的：

- 撤销工作区的修改：`git checkout -- 文件名`
- 撤销暂存区的修改：`git reset HEAD 文件名`
- 回退到历史版本：`git reset --hard 该版本ID`
- 回退到上个版本：`git reset --hard HEAD^`
- 上上版本是`HEAD^^`，也可用`HEAD~2`表示，以此类推

### 与标签有关的：

- 为当前版本打标签：`git tag 标签名`
- 为历史版本打标签：`git tag 标签名 该版本ID`
- 指定标签说明：`git tag –a 标签名 –m "标签说明" [可选：版本ID]`
- 查看所有标签：`git tag`
- 查看某一标签：`git show 标签名`
- 删除某一标签：`git tag –d 标签名`

### 与GitHub有关的：

先有本地库，后有远程库，将本地库push到远程库

关联本地仓库和GitHub库：**git remote add origin 网站上的仓库地址**
第一次将本地仓库推送到GitHub上：**git push –u origin master**

先有远程库，后有本地库，从远程库clone到本地库

从远程库克隆到本地：**git clone 网站上的仓库地址**

**网站地址可以选择HTTPS协议（https://github.com...）、SSH协议（git@github.com...）。如果选择SSH协议，必须将Ubuntu的公钥添加到GitHub上。见下一步**

SSH Key

生成SSH Key：**ssh-keygen –t rsa –C "你的邮箱@xx.com"**
生成Key时弹出选项，回车选择默认即可。
Key保存位置：**/root/.ssh**
登陆GitHub，创建new SSH key，其内容为`/root/.ssh/id_rsa.pub`中文本

已经有了本地库和远程库，二者实现同步

