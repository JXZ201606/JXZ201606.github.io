---
title: git的复习
date: 2019-04-23 14:43:43
tags: [git,github]
categories: Git
---
好早之前学习过git，有些命令不怎么用，已经忘记了，在这里做一个复习，也做个记录。

推荐查看学习廖雪峰的git教程[https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

## git的简介


Git是什么？

Git是目前世界上最先进的分布式版本控制系统（没有之一）。

Git有什么特点？简单来说就是：高端大气上档次！

那什么是版本控制系统？

如果你用Microsoft Word写过长篇大论，那你一定有这样的经历：

想删除一个段落，又怕将来想恢复找不回来怎么办？有办法，先把当前文件“另存为……”一个新的Word文件，再接着改，改到一定程度，再“另存为……”一个新文件，这样一直改下去，最后你的Word文档变成了这样：

![](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013848606651673ff1c83932d249118bf8fd5c58c15ca2000/0)

过了一周，你想找回被删除的文字，但是已经记不清删除前保存在哪个文件里了，只好一个一个文件去找，真麻烦。

看着一堆乱七八糟的文件，想保留最新的一个，然后把其他的删掉，又怕哪天会用上，还不敢删，真郁闷。

更要命的是，有些部分需要你的财务同事帮助填写，于是你把文件Copy到U盘里给她（也可能通过Email发送一份给她），然后，你继续修改Word文件。一天后，同事再把Word文件传给你，此时，你必须想想，发给她之后到你收到她的文件期间，你作了哪些改动，得把你的改动和她的部分合并，真困难。

于是你想，如果有一个软件，不但能自动帮我记录每次文件的改动，还可以让同事协作编辑，这样就不用自己管理一堆类似的文件了，也不需要把文件传来传去。如果想查看某次改动，只需要在软件里瞄一眼就可以，岂不是很方便？

这个软件用起来就应该像这个样子，能记录每次文件的改动：
![git1](/images/git1.png)

这样，你就结束了手动管理多个“版本”的史前时代，进入到版本控制的20世纪。
## git的安装
在Windows上安装Git（其他系统自行百度)

在Windows上使用Git，可以从Git官网直接[下载安装程序](https://git-scm.com/downloads)，（网速慢的同学请移步[国内镜像](https://pan.baidu.com/s/1kU5OCOB#list/path=%2Fpub%2Fgit)），然后按默认选项安装即可。
![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907073134ef6feff559cf4ce3a2c5c588d2831c0a000/0)

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"

$ git config --global user.email "email@example.com"

```

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。

注意<font color=#FF0000> ***git config***</font>命令的<font color=#FF0000>***--global***</font>参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。
## 创建版本库
什么是版本库呢？版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

### 所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```
<font color=#FF0000>pwd</font>命令用于显示当前目录。在我的Mac上，这个仓库位于/Users/michael/learngit。

 <font color=#FF0000>如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文</font>

### 第二步，通过git init命令把这个目录变成Git可以管理的仓库：
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个<font color=#FF0000>.git</font>的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。
### 把文件添加到版本库
言归正传，现在我们编写一个readme.txt文件，内容如下：

```
Git is a version control system.
Git is free software.
```
#### 用命令git add告诉Git，把文件添加到仓库：
`$ git add readme.txt`
#### 用命令git commit告诉Git，把文件提交到仓库:
```
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```
简单解释一下<font color=#FF0000>git commit</font>命令，<font color=#FF0000>-m</font>后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

嫌麻烦不想输入<font color=#FF0000>-m "xxx"</font>行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。实在不想输入说明的童鞋请自行Google，我不告诉你这个参数。

<font color=#FF0000>git commit</font>命令执行成功后会告诉你，<font color=#FF0000>1 file changed</font>：1个文件被改动（我们新添加的readme.txt文件）；<font color=#FF0000>2 insertions</font>：插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：
```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```
## 时光机穿梭
我们已经成功地添加并提交了一个readme.txt文件，现在，是时候继续工作了，于是，我们继续修改readme.txt文件，改成如下内容：
```
Git is a distributed version control system.
Git is free software.

```
现在，运行<font color=#FF0000>git status</font>命令看看结果：
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
<font color=#FF0000>git status</font>命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，readme.txt被修改过了，但还没有准备提交的修改。

虽然Git告诉我们readme.txt被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你休假两周从国外回来，第一天上班时，已经记不清上次怎么修改的readme.txt，所以，需要用<font color=#FF0000>git diff</font>这个命令看看：
```
$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
```
<font color=#FF0000>git diff</font>顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以从上面的命令输出看到，我们在第一行添加了一个distributed单词。

知道了对readme.txt作了什么修改后，再把它提交到仓库就放心多了，提交修改和提交新文件是一样的两步，第一步是git add：

`$ git add readme.txt`

同样没有任何输出。在执行第二步<font color=#FF0000>git commit</font>之前，我们再运行<font color=#FF0000>git status</font>看看当前仓库的状态：
```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   readme.txt
```
<font color=#FF0000>git status</font>告诉我们，将要被提交的修改包括readme.txt，下一步，就可以放心地提交了：
```
$ git commit -m "add distributed"
[master e475afc] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
```
提交后，我们再用<font color=#FF0000>git status</font>命令看看仓库的当前状态：
```
$ git status
On branch master
nothing to commit, working tree clean
```
Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的。
### 版本回退
现在，你已经学会了修改文件，然后把修改提交到Git版本库，现在，再练习一次，修改readme.txt文件如下：
```
Git is a distributed version control system.
Git is free software distributed under the GPL.
```
然后尝试提交：
```
$ git add readme.txt
$ git commit -m "append GPL"
[master 1094adb] append GPL
 1 file changed, 1 insertion(+), 1 deletion(-)
```
像这样，你不断对文件进行修改，然后不断提交修改到版本库里，就好比玩RPG游戏时，每通过一关就会自动把游戏状态存盘，如果某一关没过去，你还可以选择读取前一关的状态。有些时候，在打Boss之前，你会手动存盘，以便万一打Boss失败了，可以从最近的地方重新开始。Git也是一样，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为<font color=#FF0000>commit</font>。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个<font color=#FF0000>commit</font>恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

现在，我们回顾一下<font color=#FF0000>readme.txt</font>文件一共有几个版本被提交到Git仓库里了：

版本1：wrote a readme file
```
Git is a version control system.
Git is free software.
```
版本2：add distributed
```
Git is a distributed version control system.
Git is free software.
```
版本3：append GPL
```
Git is a distributed version control system.
Git is free software distributed under the GPL.
```
当然了，在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容，不然要版本控制系统干什么。版本控制系统肯定有某个命令可以告诉我们历史记录，在Git中，我们用<font color=#FF0000>git log</font>命令查看：
```
$ git log
commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

commit e475afc93c209a690c39c13a46716e8fa000c366
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
```
<font color=#FF0000>git log</font>命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是<font color=#FF0000>append GPL</font>，上一次是<font color=#FF0000>add distributed</font>，最早的一次是<font color=#FF0000>wrote a readme file</font>。

如果嫌输出信息太多，看得眼花缭乱的，可以试试加上<font color=#FF0000>--pretty=oneline</font>参数：
```
$ git log --pretty=oneline
1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
e475afc93c209a690c39c13a46716e8fa000c366 add distributed
eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
```
需要友情提示的是，你看到的一大串类似<font color=#FF0000>1094adb...</font>的是<font color=#FF0000>commit id</font>（版本号），和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。为什么<font color=#FF0000>commit id</font>需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。

每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线：

![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907545599be4a60a0b5044447b47c8d8b805a25d2000/0)

好了，现在我们启动时光穿梭机，准备把<font color=#FF0000>readme.txt</font>回退到上一个版本，也就是<font color=#FF0000>add distributed</font>的那个版本，怎么做呢？

首先，Git必须知道当前版本是哪个版本，在Git中，用<font color=#FF0000>HEAD</font>表示当前版本，也就是最新的提交<font color=#FF0000>1094adb...</font>（注意我的提交ID和你的肯定不一样），上一个版本就是<font color=#FF0000>HEAD^</font>，上上一个版本就是<font color=#FF0000>HEAD^^</font>，当然往上100个版本写100个^比较容易数不过来，所以写成<font color=#FF0000>HEAD~100</font>。

现在，我们要把当前版本<font color=#FF0000>append GPL</font>回退到上一个版本<font color=#FF0000>add distributed</font>，就可以使用<font color=#FF0000>git reset</font>命令：
```
$ git reset --hard HEAD^
HEAD is now at e475afc add distributed
```
<font color=#FF0000>--hard</font>参数有啥意义？这个后面再讲，现在你先放心使用。

看看<font color=#FF0000>readme.txt</font>的内容是不是版本<font color=#FF0000>add distributed</font>：
```
$ cat readme.txt
Git is a distributed version control system.
Git is free software.
```
果然被还原了。

还可以继续回退到上一个版本<font color=#FF0000>wrote a readme file</font>，不过且慢，然我们用<font color=#FF0000>git log</font>再看看现在版本库的状态：
```
$ git log
commit e475afc93c209a690c39c13a46716e8fa000c366 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
```
最新的那个版本<font color=#FF0000>append GPL</font>已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个<font color=#FF0000>append GPL</font>的<font color=#FF0000>commit id</font>是<font color=#FF0000>1094adb...</font>，于是就可以指定回到未来的某个版本：
```
$ git reset --hard 1094a
HEAD is now at 83b0afe append GPL
```
版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。

再小心翼翼地看看<font color=#FF0000>readme.txt</font>的内容：
```
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
```
果然，我胡汉三又回来了。

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的<font color=#FF0000>HEAD</font>指针，当你回退版本的时候，Git仅仅是把HEAD从指向<font color=#FF0000>append GPL</font>：

┌────┐
│HEAD│
└────┘
   │
   └──> ○ append GPL
        │
        ○ add distributed
        │
        ○ wrote a readme file
改为指向<font color=#FF0000>add distributed</font>：

┌────┐
│HEAD│
└────┘
   │
   │    ○ append GPL
   │    │
   └──> ○ add distributed
        │
        ○ wrote a readme file
然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。

现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的<font color=#FF0000>commit id</font>怎么办？

在Git中，总是有后悔药可以吃的。当你用<font color=#FF0000>$ git reset --hard HEAD^</font>回退到<font color=#FF0000>dd distributed</font>版本时，再想恢复到<font color=#FF0000>append GPL</font>，就必须找到<font color=#FF0000>append GPL</font>的<font color=#FF0000>commit id</font>。Git提供了一个命令<font color=#FF0000>git reflog</font>用来记录你的每一次命令：
```
$ git reflog
e475afc HEAD@{1}: reset: moving to HEAD^
1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
e475afc HEAD@{3}: commit: add distributed
eaadf4e HEAD@{4}: commit (initial): wrote a readme file
```
终于舒了口气，从输出可知，<font color=#FF0000>append GPL</font>的<font color=#FF0000>commit id</font>是<font color=#FF0000>1094adb</font>，现在，你又可以乘坐时光机回到未来了。
### 工作区和暂存区
Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

先来看名词解释。

工作区（Working Directory）
就是你在电脑里能看到的目录，比如我的<font color=#FF0000>learngit</font>文件夹就是一个工作区：

![](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013849082162373cc083b22a2049c4a47408722a61a770000/0)

版本库（Repository）
工作区有一个隐藏目录<font color=#FF0000>.git</font>，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为<font color=#FF0000>stage（或者叫index）</font>的暂存区，还有Git为我们自动创建的第一个分支<font color=#FF0000>master</font>，以及指向<font color=#FF0000>master</font>的一个指针叫<font color=#FF0000>HEAD</font>。

![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)

分支和<font color=#FF0000>HEAD</font>的概念我们以后再讲。

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用<font color=#FF0000>git add</font>把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用<font color=#FF0000>git commit</font>提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个<font color=#FF0000>master</font>分支，所以，现在，<font color=#FF0000>git commit</font>就是往<font color=#FF0000>master</font>分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

俗话说，实践出真知。现在，我们再练习一遍，先对<font color=#FF0000>readme.txt</font>做个修改，比如加上一行内容：
```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
```
然后，在工作区新增一个<font color=#FF0000>LICENSE</font>文本文件（内容随便写）。

先用<font color=#FF0000>git status</font>查看一下状态：
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    LICENSE

no changes added to commit (use "git add" and/or "git commit -a")
```
Git非常清楚地告诉我们，<font color=#FF0000>readme.txt</font>被修改了，而<font color=#FF0000>LICENSE</font>还从来没有被添加过，所以它的状态是<font color=#FF0000>Untracked</font>。

现在，使用两次命令<font color=#FF0000>git add</font>，把<font color=#FF0000>readme.txt</font>和<font color=#FF0000>LICENSE</font>都添加后，用<font color=#FF0000>git status</font>再查看一下：
```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   LICENSE
    modified:   readme.txt
```
现在，暂存区的状态就变成这样了：
![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907720458e56751df1c474485b697575073c40ae9000/0)

所以，<font color=#FF0000>git add</font>命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行<font color=#FF0000>git commit</font>就可以一次性把暂存区的所有修改提交到分支。
```
$ git commit -m "understand how stage works"
[master e43a48b] understand how stage works
 2 files changed, 2 insertions(+)
 create mode 100644 LICENSE
```
一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：
```
$ git status
On branch master
nothing to commit, working tree clean
```
现在版本库变成了这样，暂存区就没有任何内容了：

![](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013849077337835a877df2d26742b88dd7f56a6ace3ecf000/0)