[TOC]



# Github 学习笔记——从零开始学习

## 一.Git简介

### 1.什么是Github

​	Git是目前世界上最先进的分布式版本控制系统，所谓的版本控制系统简单来说就是一个开发软件他可能经过多次的修改，版本控制系统会记录软件版本修改的操作，以便达到对软件版本进行管理的目的

### 2.Github 的开发语言

​	Git是Linus（Linux创始人）用C语言开发的。

### 3.集中式和分布式的区别

​	集中式版本控制系统，版本库是存放在中央服务器的，需要进行任务工作，必须要从中央服务器取得最新的版本，然后才能进行任务操作，任务完成之后，在将完成好的工作推送给中央服务器。特点就是集中管理存储，需要联网，一旦中央服务器坏的，工作任务就丢失了。

​	分布式版本控制系统，没有所谓的中央服务器，每个人的电脑上都是一个完整的版本库，个人电脑的损坏并不影响整个任务，依旧可以从其他人那里拿到该任务。分布式版本的多人协作就是不同的人对任务进行修改了之后，互相将修改的任务推送给对方，就可以合并修改。分布式版本控制系统的服务器只起到一个中转站的作用，即使服务器损坏，也只是不能通讯，并不会造成丢失。

### 4.Github的安装

​	这里只说Linux系统的使用，在Ubuntu Linux系统，使用`git`命令就能查看系统是否安装Git：

![image-20240326010830274](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326010830274.png)

如果没有安装Git，使用`sudo apt-get install git`命令进行安装。

## 二.Github 的使用（常用命令）

### 1.创建版本库

​	使用一个合适的文件夹，可以自己创建一个空目录：

```
	$ mkdir learngit
	$ cd learngit
```

​	通过`git init`命令把目录变成Git管理的仓库。

![image-20240326011606475](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326011606475.png)

这个.git里面的文件不要随意修改。请谨慎的在现有文件加上创建Git仓库，以免造成不必要的麻烦。

​	编写一个文件：`vim readme.txt`，内容如下：

```
Git is a version control system.
Git is free software.
```

​	第一步使用`git add`命令将文件添加到仓库

​	`$ git add readme.txt`

​	第二步使用`git commit`将文件提交到仓库

​	`$ git commit -m "wrote a readme file"`

-m 后面的双引号内容为解释信息，可以随意写，但是最好是有意义的文字，可以解释该次提交内容。这里为什么提交内容需要两步呢？解释就是第一步的add命令只是将需要提交的文件放入暂存区，并没有真正的提交，可以随时撤回，真正需要提交时，才使用git commit命令进行提交。

```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

### 2.Git状态查看和修改

​	使用`git status`命令可以查看当前状态

![image-20240326014147928](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326014147928.png)

​	修改文件后，使用`git diff`命令可以查看对比文件修改前后的差别：

​	`$ git diff readme.txt`

![image-20240326014432507](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326014432507.png)

​	然后再使用add和commit命令可对修改后的内容进行提交

### 3.版本的回退

​	使用`git log`命令可以查看修改的内容和时间节点：

​	`$ git log`

![image-20240326014751283](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326014751283.png)

​	在命令后面加上`--pretty=oneline`参数可以减少信息量：

​	`$ git log --pretty=oneline`

![image-20240326015010723](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326015010723.png)

​	在Git中使用`HEAD`表示当前版本，上一个版本是`HEAD^`，上上一个版本是`HEAD^^`，当版本数目过多时，比如前100个版本就是`HEAD~100`。

​	使用`git reset`命令进行版本回退

​	`$ git reset --hard HEAD^`

![image-20240326015434060](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326015434060.png)

查看readme.txt内容，版本确实会被还原。

![image-20240326015605816](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326015605816.png)

​	此时查看版本历史

​	`$ git log`

​	![image-20240326015719225](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326015719225.png)

之前的最新版本已经没有了。

​	也可以使用版本号回到指定的版本`git reset --hard commit_id`，版本号不必写全，Git会自动联想，只要写开头一部分即可。比如再回到之前的最新版本：

​	`$ git reset --hard 8ad2d`

![image-20240326015944370](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326015944370.png)

查看readme.txt内容，版本确实又回到了最新

![image-20240326020038869](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326020038869.png)

​	最后使用`git reflog`可以记录每一次的命令，即使电脑关电，也能查看之前的版本号

​	`$ git reflog`

![image-20240326020330095](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326020330095.png)

然后根据版本号进行指定的版本回退。

### 4.细说工作区和暂存区

​	工作区：电脑里面能看到的目录，比如前面的learngit文件夹就是一个工作区

​	版本库：工作区的隐藏目录`.git`，这个文件夹是Git的版本库。暂存区就是在版本库里面，称为stage（index），本测试用系统Git暂存区实际是index。还有一个自动创建的第一个分支`master`，还有指向`master`的指针叫做`HEAD`。

![image-20240326185145666](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326185145666.png)

​	Git中将文件像Git版本库添加时，分两步执行：第一步使用`git add`将文件修改添加到暂存区；第二步使用`git commit`提交更改，实际就是把暂存区的所以内容提交到当前分支。总的来说，就是把需要提交的文件修改通通放大暂存区，然后一次性提交暂存区的所有修改。

​	修改readme.txt和添加LICENSE文件后，使用`git status`查看状态：

![image-20240326185328952](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326185328952.png)

​	使用`git add`添加到暂存区：

​	`$ git add readme.txt LICENSE`

![image-20240326185420310](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326185420310.png)

​	使用vim 编辑器查看index文件`vim index`可以看到暂存区内容：

![image-20240326185623463](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326185623463.png)

​	HEAD内容为：

![image-20240326185714299](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326185714299.png)

​	执行`git commit`命令可以把暂存区所有修改提交到分支master：

​	`$ git commit -m "understand how stage works"`

![image-20240326190141435](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326190141435.png)

​	此时再查看工作区状态，工作区变得很干净：

​	`git status`

![image-20240326190315704](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326190315704.png)

​	再查看暂存区index里面的内容，发现没有stage相关的任何内容：

![image-20240326190428171](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326190428171.png)



### 5.修改的管理

​	Git跟踪管理的不是文件，而是修改。所谓的修改，就是对某个文件的增删改查，Git就是对这个修改进行记录。

​	进行实验，继续对readme.txt进行修改，增加一行内容`Git tracks changes.`：

![image-20240326191108016](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326191108016.png)

​	进行添加：

​	`$ git add readme.txt`

​	`$ gut status`

![image-20240326191809750](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326191809750.png)

​	继续修改readme.txt，增加·`of files.`：

![image-20240326192009764](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326192009764.png)

​	直接提交：

​	`$ git commit -m "git tracks changes"`

![image-20240326192643506](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326192643506.png)

​	查看状态：

![image-20240326220604915](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326220604915.png)

可以看到，第二次的修改其实是没有被提交的，这是因为第二次的修改并没有使用`git add`命令，只有第一次的修改使用了该命令，修改被放入暂存区，准备提交，第二次修改没有放入暂存区，没有被提交，`git commit`只负责把暂存区的修改进行提交。

### 6.撤销修改

​	对readme.txt进行修改，加入一个错误行，内容为`My stupid boss still prefers SVN`

![image-20240326221514267](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326221514267.png)

​	查看使用`git status`

![image-20240326221722973](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326221722973.png)

​	使用`git checkout -- file`可以丢弃工作区的修改，即把file文件在工作区的修改全部撤销。注意，该撤销只能撤销回到最近一次`git commit`或者`git add`时的状态

​	`git checkout -- readme.txt`

![image-20240326222155921](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326222155921.png)

​	

​	注意，这里的命令里面的`--`不能省略，否则命令含义会发生变化。

​	除了使用`git checkout -- file`之外，还可以使用命令`git reset HEAD <file>`来把暂存区的修改撤掉，重新放回工作区，其中`HEAD`表示最新的版本。

​	如果已经将版本提交到版本库，那么就可以使用版本回退功能回退到上一个版本。

### 7.文件的删除

​	文件删除也是一种修改，通常有两种选择从版本库删除该文件。

​	一种就是使用命令`git rm`并且`git commit`

​	`$ git rm test.txt`

![image-20240326224626224](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326224626224.png)

​	`$ git commit -m "remove test.txt"`

![image-20240326224820764](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240326224820764.png)

​	另一种是删除错了，需要对误删除的文件进行恢复到最新版本

​	`git checkout -- test.txt`

​	`git checkout`的实际操作就是用版本库里面的版本替换工作区里面的版本，无论工作区是删除或者修改，都可以一键还原。

## 三.Github远程仓库

### 1.添加远程仓库

​	之前的操作是基于本地的Git仓库，需要在Github创建一个远程仓库，并且让两个仓库进行远程同步，远程仓库的可以当做备份也能够进行共享，进行协同开发。

​	想要创建远程仓库，首先需要登录Github，使用Creat a new repository，创建一个新仓库。

![image-20240329161257584](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329161257584.png)

创建好的新仓库后，会提示使用这个仓库克隆新的仓库，或者把已有的本地仓库和它相关联，之后把本地仓库内容推送到Github。

![image-20240329162129516](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329162129516.png)

​	使用`git remote add origin git@github.com:nofishisme/learngit.git` 添加远程仓库，将本地仓库和远程仓库关联，远程仓库名字默认是`origin`，可以进行修改，但是一般不建议。

​	然后使用`git push -u origin master`将本地库的内容推送到远程库上面去。最新2024年3/29进行操作，出现了错误，存在以下提示：

![image-20240329170140417](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329170140417.png)

可以使用https的方式解决，将.git/config里面url后的内容改成https的形式。

![image-20240329170530194](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329170530194.png)

改成

![image-20240329170609688](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329170609688.png)

改完之后直接使用`git push -u origin master`会提示输入账号密码，但是最后又报错说该方式已经无法使用，需要继续更换方式。

![image-20240329171202848](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329171202848.png)

​	解决办法使用生成令牌token，具体教程参考[【突发】解决remote: Support for password authentication was removed on August 13, 2021. Please use a perso-CSDN博客](https://blog.csdn.net/yjw123456/article/details/119696726)，其核心就是将生成的令牌号与之前url 后的链接相结合，url后的链接变为`https://<your_token>@github.com/<USERNAME>/<REPO>.git`，其中<your_token>用令牌码替换，<USERNAME>使用用户名替换，<REPO>用项目名字替换，最终结果为如下：

![image-20240329173012196](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329173012196.png)

又出现问题，截图如下：

![image-20240329174712928](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329174712928.png)

解决办法是查看git是否使用代理。后发现是因为挂了梯子，代理出现了问题，关闭掉梯子后可正常提交。

![image-20240329174831106](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329174831106.png)

​	终于，艰难操作之后，将本地库的内容推送到了远程，将本地库内容推送到远程，使用git push命令，实际上是把当前分支master推送到远程。

​	**总结，关联一个远程库，有效的做法是使用命令以下命令：**

​	**`git remote add origin https://<your_token>@github.com/<USERNAME>/<REPO>.git`**

**其中的token需要自己在Git上申请。**

​	远程库是空的，第一次推送`master`分支时，加上`-u`参数，Git会同时把本地的`master`分支内容推送远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，以后推送和拉取就能简化命令。

​	后续，本地的提交，都可以通过`git push origin master`将本地`master`分支的最新修改推送到Github。

### 2.删除远程库

​	使用`git remote rm <name>`命令可以删除远程库，删除前，使用`git remote -v`查看远程库信息。

​	该删除只是解除远程和本地的绑定关系，并不是物理上删除了远程库，远程库本身没有任何改动。真正的删除远程库，需要登录到Github进行删除。

​	补充（2024/4/4）：语句命令`find . -name ".git" | xargs rm -Rf`可以解除本地文件夹的仓库身份

### 3.远程库克隆

​	前面是先创建本地库，再关联远程库，但是最好的方式就是先创建远程库，然后从远程库进行克隆。

​	新建一个仓库，取名为gitskills，勾选`Initialize this repository with a README`，Github就会自动创建一个README.md文件。

![image-20240329223013705](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329223013705.png)

​	使用命名`git clone`克隆一个本地库

​	`$ git clone https://github.com/nofishisme/gitskills.git`

![image-20240329223636385](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240329223636385.png)

​	<font color='red'>在这里使用命令`git clone git@github.com:nofishisme/gitskills.git`还是会报错，提示无法识别远程仓库，后续提供解决使用SSH的解决办法。</font>

### 4.解决SSH无法使用的办法

​	从一开始，使用SSH相关的命令，都会提示出错：

![image-20240330163607318](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330163607318.png)

显示无法读取到远程仓库，这是因为没有使用SSH秘钥，需要对Github配置SSH秘钥连接。

## 四.Git分支管理

### 1.分支管理

​	分支管理就是在原来分支上提取一个分支，该分支不对原分支造成影响，再对提取的分支进行操作后，再与原来的分支进行合并，这样的分支功能既安全又不会影响别人的正常工作。

### 2.创建和合并分支

​	每次提交，Git就把它们串成一条时间线，这条时间线就是一个分支。最开始，只有一条时间线，被称之为主分支，也就是`master`分支。`HEAD`并不是指向提交而是指向`master`，而<font color='red'>`master`是指向提交的</font>，也就是说，<font color='red'>`HEAD`指向当前分支</font>。

​	`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点。

![image-20240330210804245](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330210804245.png)

​	每一次提交，`master`分支都会向前移动一步，随着不断的提交，`master`分支会越来越长。

​	可以创建一个新的分支，取名叫`dev`，Git会新建一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上。

![image-20240330211003451](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330211003451.png)

​	新增了`dev`分支后，后续的工作区的修改就是针对`dev`分支了，每产生一次新的提交，`dev`指针就往前移动一步，但是`master`指针不变。

![image-20240330211301479](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330211301479.png)

​	合并分支最简单的方法就是直接把`master`指向`dev`的当前提交，就能完成合并。

![image-20240330211538039](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330211538039.png)

​	合并完成之后，也可以直接删除`dev`分支，删掉后就剩下`master`一条分支。

![image-20240330211723712](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330211723712.png)

​	首先，创建`dev`分支并切换到`dev`分支，其中`-b`参数表示创建并切换：

​	`$ git checkout -b dev`或者`$ git switch -c dev`

或者

​	`$ git branch dev`

​	`$ git checkout dev`或者`$ git switch dev`

![image-20240330212728803](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330212728803.png)

可以换使用`git branch`命令查看当前分支

​	`$ git branch`

![image-20240330213110302](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330213110302.png)

可以看见，当前分支就是`dev`，前面会加上`*`号。

​	在`dev`分支上对`readme.txt`进行修改，新增一行`Creating a new branch is quick.`，并进行提交。

![image-20240330213403992](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330213403992.png)

完成`dev`分支工作后，使用命令`git checkout master`切回主分支。

![image-20240330213549904](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330213549904.png)

切换为主分支后发现`readme.txt`里面并没有新添加的内容，这是因为那个提交在分支`dev`上，但是`master`分支没有变。

![image-20240330213808972](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330213808972.png)

![image-20240330213941825](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330213941825.png)

​	使用命令`git merge dev`可以将`dev`分支的工作成果合并到当前的`master`分支上。

​	`$ git merge dev`

![image-20240330214222923](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330214222923.png)

​	注意提示中的`Fast-forward`，其表示这次合并是“快进模式”，直接把`master`指针指向`dev`的当前提交，所以合并速度非常快。

​	合并完成之后，就可以删除分支`dev`

​	`$ git branch -d dev`

![image-20240330214626426](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330214626426.png)

​	使用branch很快，也很安全，所以提倡使用分支来完成某个任务。

​	注意，如果使用命令`git switch -c <name>`提示不是一个git命令，那么可能是本地git的版本有问题，使用命令`git --version`可以查看当前的git版本。

​	`git --version`

![image-20240330221434777](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330221434777.png)

​	可以使用命令将git版本升级，无论是否安装git，都可以使用以下命令安装最新版本的git。

​	`$ sudo add-apt-repository ppa:git-core/ppa`

​	`$ sudo apt update`

​	`$ sudo apt install git`

![image-20240330222225349](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330222225349.png)

### 3.分支冲突解决

​	新建一个分支，进行冲冲突测试，创建一个分支`feature1`，并切换到分支，修改`readme.txt`内容，最后一行添加`Creating a new branch is quick AND simple.`，并在分支`feature1`上进行提交，再切换会`master`分支，会提示当前的`master`分支比远程的`master`分支要超前一个提交。

![image-20240330222801601](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330222801601.png)

同时修改`master`分子里面的`readme.txt`文件，最后一行添加`Creating a new branch is quick & simple.`。可以看到，`master`分支里面添加的内容和`feature1`分支里面添加内容不一致，也将`master`分支内容提交。

![image-20240330223643971](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330223643971.png)

于是`master`分支和`feature1`分支都有了自己新的提交：

![image-20240330223944465](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330223944465.png)

​	在这种情况下，Git无法执行快速合并，只能尝试将各自修改合并，但是可能产生冲突。

![image-20240330224139469](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330224139469.png)

​	合并产生冲突，必须要解决冲突之后才能提交。

![image-20240330224238595](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330224238595.png)

​	可以直接查看待修改文件的内容进行修正，这里是`readme.txt`文件：

![image-20240330224441136](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330224441136.png)

​	`<<<<<<<`，`=======`，`>>>>>>>`表示不同分支的内容。可以直接手动修改内容，然后提交，这里修改为

`Creating a new branch is quick and simple`，合并的情况如下：

![image-20240330224822991](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330224822991.png)

![image-20240330224921848](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330224921848.png)

​	使用带参数的命令`git log`可以查看分支合并情况。

​	`$ git log --graph --pretty=oneline --abbrev-commit`

![image-20240330225225751](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330225225751.png)

​	最后，再删除`feature1`分支。

​	`$ git branch -d feature1`

![image-20240330225401642](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240330225401642.png)

### 4.分支管理策略

​	Git通常会倾向于使用`Fast forward`的合并模式，但是这种模式下删除分支会丢掉分支信息。强行禁用`Fast forward`模式，Git会在merge时生成一个新的commit，这样就可以从分支历史上看出分支信息。

​	以下为`--no-ff`方式的`git merge`

​	创建新的分支`dev`并且切换到分支`dev`，在分支`dev`修改`readme.txt`的内容然后进行提交，在切换会主`master`分支。

![image-20240331113854165](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240331113854165.png)

这里提示分支领先‘origin/master’共四个提交时因为本地仓库没有提交更新到远程仓库。

​	使用`--no-ff`参数来进行分支`dev`的合并，表示禁用`Fast forward`：

​	`$ git merge --no-ff -m "merge with no-ff" dev`

![image-20240331114257986](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240331114257986.png)

本次合并要创建一个新的`commit`，所以要加上`-m`参数，把`commit`的描述写进去。

​	查看分支历史：

​	`$ git log --graph --pretty=oneline --abbrev-commit`

![image-20240331115907594](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240331115907594.png)

​	`fast forward`模式的合并看不出曾经有合并，而加上`--no-ff`参数后就可以用普通模式合并，能看到历史分支。

### 5.用于BUG的分支

​	当软件开发中遇到bug时，可以创建一个临时分支来进行修复，修复后在合并分支，然后删除临时分支。‘

​	当遇到bug需要处理，但是当前工作区任务却并没有完成，则可以使用`git stash`命令可以将当前工作现场”储藏“起来，等后面恢复现场后继续工作，然后再创建分支进行bug处理。需要再哪个分支进行bug处理，就要在哪个分支创建上创建临时分支。

![image-20240331232650035](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240331232650035.png)

​	使用命令`git stash list`可以查看被保存的工作现场，可以使用两种方法进行恢复。一是使用命令`git stash apply`进行恢复，恢复后stash内容并不会删除，需要使用`git stash drop`来删除。二是使用命令`git stash pop`，恢复的同时把stash内容也删除了。

​	如果除了主分支`master`外，在`dev`分支上也有同样的bug，怎么解决呢？解决办法有两种。

​	操作一是在`dev`分支上进行之前同样的操作。

​	更简单的操作二是把`b196443 fix bug 101`这个提交所做的修改“复制”到`dev`分支，使用命令`git cherry-pick`可以复制一个特定的提交到当前分支。

![image-20240331233022179](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240331233022179.png)

​	可以看到这里的提交就是分支`dev 2e26da0`，虽然两个提交改动相同，但是实际是和master不同的分支。

### 5.新功能Feature分支

​	每当要添加一个新功能时，为了防止实验代码把主分支代码打乱，会新建一个feature分支，在上面开发完成后再进行合并，然后再删除feature分支。

​	
