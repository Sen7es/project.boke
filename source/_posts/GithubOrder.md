---
title: 常用Git命令手册
tags:
  - Git 
categories: Git
---

以下内容是我在学习和研究Git时，对Git操作的特性、重点和注意事项的提取、精练和总结，可以做为Git操作的字典，方便大家查阅；如果你从未接触过Git，希望看一个入门级别的教程，请移步到[《Git基础教程》](https://www.jianshu.com/p/fd40460ffb37)

此文只是对Git有一定基础的人当记忆使用，比较简略，初级学员强烈推荐廖雪峰老师的Git系列教程，通俗易懂，

<escape><!-- more --></escape>

### 一些命令快捷指南

> ```bash
> git三个选项的作用域：
> git config --system：  //使对应配置针对系统内所有的用户有效
> git config --global：  //使对应配置针对当前系统用户的所有仓库生效
> git config --local：   //使对应配置只针对当前仓库有效
> ```
>
> #### local选项设置的优先级最高。
>
> > ##### 查看对应作用域的设置：
> >
> > ```bash
> > git config --system --list
> > git config --global --list
> > git config --local --list
> > ```
>
> #### 提交
>
> ```bash
> git add .  ：  //创建变更集
> git commit ：  //将这个变更集提交到git仓库中。
> 我们可以利用git add选择性的将那些变动文件加入到变更集中然后由git commit提交至仓库中。
> ```
>
> 
>
> #### 在git中有一些“区域”的概念，我们在使用git时，其实一直都在使用这些“区域”。所以了解git区域的概念是必须的，这有助于我们使用git和理解git的工作原理。
>
> ```bash
> git status  //查看文件的变更状态
> git log     //查看当前提交历史
> git log --oneline  //使用简洁模式查看提交历史
> git cat-file -t [哈希值]  //查看对应的对象类型，-p选项查看相关内容
> git rev-parse [哈希值] //通过简短的哈希值获取到整个哈希值
> git reset --hard [哈希值] //返回之前版本状态，通过log去查想要返回状态的哈希值
> git reflog  //查看所有历史提交
> git branch  //查看现在都有哪些分支
> git branch [分支名] //创建新的分支
> git checkout [分支名] //切换分支
> git reset --hard HEAD~0   //回退到上一次提交代码的状态
> git reset --hard HEAD~1   //回退到上上次提交代码的状态
> git reset --hard HEAD [版本号] //回退到指定版本号
> git reflog  //可以查看每一次切换版本的记录以及所有的版本号
> git merge [分支名]   //合并分支在master分支执行。
> git breanch -d [分支名] //删除分支，在master分支执行
> ```
>
> #### github远程仓库
>
>   1. 创建SSH key： ssh-keygen -t rsa -f /root/.ssh/id_rsa -N ''
>      -t 指定算法
>      -f 秘钥文件名
>      -N 指定秘钥密码双引号密码为空
>      
>   2. 登入 github -> settings -> SSH and GPG keys -> NEW SSH Key 
>
>         > 1. 输入名字（自定义）>  Add SSH key
>         >
>         > 2. 粘贴服务器的公钥
>         >
>         > 3. 关联仓库： 
>         >
>         >    > ```bash
>         >    > git remote add origin git@github.com:aptxhb/test.git
>         >    > git push -u origin master   //第一次推送github
>         >    > git push origin master      //以后都是用这个命令推送
>         >    > ```
>         >
>         > 4. 克隆已存在的远程仓库：git clone git@github.com:aptxhb/test.git
>         >
>         > 5. git pull   //拉取远程仓库代码
>         >
>         > 6. PS：多人协作先拉去成为最新的文件在推送这样避免冲突

### 安装Git

- Linux

```bash
sudo apt-get install git
```

- Window:到Git官网下载安装：https://git-scm.com/downloads

### 配置全局用户Name和E-mail

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

### 初始化仓库

```bash
git init
```

### 添加文件到Git仓库

```bash
git add <file>
```

提示：可反复多次使用，添加多个文件；

### 提交添加的文件到Git仓库

```bash
git commit
```

然后会弹出一个Vim编辑器输入本次提交的内容；

或者

```bash
git commit -m "提交说明"
```

### 查看仓库当前的状态

```bash
git status
```

### 比较当前文件的修改

```bash
$ git diff <file>
```

### 查看历史提交记录

```bash
git log
```

或者加上参数查看就比较清晰了

```bash
$ git log --pretty=oneline
```

### 回退版本

```bash
$ git reset --hard HEAD^
```

说明：在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，以此类推，如果需要回退几十个版本，写几十个^容易数不过来，所以可以写，例如回退30个版本为：HEAD~30。

如果你回退完版本又后悔了，想回来，一般情况下是回不来的，但是如果你可以找到你之前的commit id的话，也是可以的，使用如下即可：

```bash
$ git reset --hard + commit id 
```

提示：commit id不需要写全，Git会自动查找；

补充说明：Git中，commit id是一个使用SHA1计算出来的一个非常大的数字，用十六进制表示，你提交时看到的一大串类似3628164...882e1e0的就是commit id（版本号）；

在Git中，版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，Git仅仅是把HEAD从指向回退的版本，然后顺便刷新工作区文件；

### 查看操作的历史命令记录

```bash
$ git reflog
```

结果会将你之前的操作的commit id和具体的操作类型及相关的信息打印出来，这个命令还有一个作用就是，当你过了几天，你想回退之前的某次提交，但是你不知道commit id了，通过这个你可查找出commit id,就可以轻松回退了，用一句话总结：穿越未来，回到过去，so easy！

### diff文件

```bash
git diff HEAD -- <file>
```

说明：查看工作区和版本库里面最新版本文件的区别，也可以不加HEAD参数；

### 丢弃工作区的修改

```bash
$ git checkout -- <file>
```

说明：适用于工作区修改没有add的文件

### 丢弃暂存区的文件

```bash
$ git reset HEAD <file>
```

说明：适用于暂存区已经add的文件，注意执行完此命令，他会将暂存区的修改放回到工作区中，如果要想工作区的修改也丢弃，就执行第12条命令即可；

### 删除文件

```bash
$ rm <file>
```

然后提交即可；

如果不小心删错了，如果还没有提交的话使用下面命令即可恢复删除，注意的是它只能恢复最近版本提交的修改，你工作区的修改是不能被恢复的！

```bash
$ git checkout -- <file>
```

### 创建SSH key

```bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```

一般本地Git仓库和远程Git仓库之间的传输是通过SSH加密的，所以我们可以将其生成的公钥添加到Git服务端的设置中即可，这样Git就可以知道是你提交的了；

### 与远程仓库协作

```bash
$ git remote add origin git@github.com:xinpengfei520/IM.git
```

删除本地库与远程库的关联：

```bash
$ git remote rm origin
```

作用：有时候我们需要关联其他远程库，需要先删除旧的关联，再添加新的关联，因为如果你已经关联过了就不能在关联了，不过想关联多个远程库也是可以的，前提是你的本地库没有关联任何远程库，操作如下：

先关联Github远程库：

```bash
$ git remote add github git@github.com:xinpengfei520/IM.git
```

接着关联码云远程库：

```bash
$ git remote add gitee git@gitee.com:xinpengfei521/IM.git
```

现在，我们用`git remote -v`查看远程库的关联信息，如果看到两组关联信息就说明关联成功了；

ok,现在我们的本地库可以和多个远程库协作了

如果要推送到GitHub，使用命令：

```bash
$ git push github master
```

如果要推送到码云，使用命令：

```bash
$ git push gitee master
```

### 推送到远程仓库

```bash
$ git push -u origin master
```

注意：第一次提交需要加一个参数-u,以后不需要

### 克隆一个远程库

```bash
$ git clone git@github.com:xinpengfei520/IM.git
```

### Git分支管理

#### 创建一个分支branch1

```bash
$ git branch branch1
```

#### 切换到branch1分支：

```bash
$ git checkout branch1
```

#### 创建并切换到branch1分支：

```bash
$ git checkout -b branch1
```

#### 查看分支：

```bash
$ git branch
```

提示：显示的结果中，其中有一个分支前有个*号，表示的是当前所在的分支；

#### 合并branch1分支到master：

```bash
$ git merge branch1
```

#### 删除分支：

```bash
$ git branch -d branch1
```

### 查看提交的历史记录

```bash
$ git log

```

### 命令可以看到分支合并图

```bash
$ git log --graph
```

### 合并分支

禁用Fast forward模式合并分支

```bash
$ git merge --no-ff -m "merge" branch1
```

说明：默认Git合并分支时使用的是Fast forward模式，这种模式合并，删除分支后，会丢掉分支信息，所以我们需要强制禁用此模式来合并；

补充内容：实际开发中分支管理的策略

- master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面提交；
- 我们可以新开一个dev分支，也就是说dev分支是不稳定的，到版本发布时，再把dev分支合并到master上，在master分支发布新版本；
- 你和你的协作者平时都在dev分支上提交，每个人都有自己的分支，时不时地往dev分支上合并就可以了；

### 保存工作现场

```bash
$ git stash
```

作用：当你需要去修改其他内容时，这时候你的工作还没有做完，先临时保存起来，等干完其他事之后，再回来回复现场，再继续干活；为什么？因为暂存区是公用的，如果不通过stash命令隐藏，会带到其它分支去；

查看已经保存的工作现场列表：

```bash
$ git stash list
```

恢复工作现场(恢复并从stash list删除)：

```bash
$ git stash pop
```

或者：

```bash
git stash apply
```

恢复工作现场，但stash内容并不删除，如果你需要删除执行如下命令：

```bash
$ git stash drop
```

恢复指定的stash:

```bash
$ git stash apply stash@{0}
```

说明：其中stash@{0}为`git stash list`中的一种编号

### 丢弃一个没有被合并过的分支

强行删除即可：

```bash
$ git branch -D <name>
```

作用：实际开发中，添加一个新feature，最好新建一个分支，如果要丢弃这个没有被合并过的分支，可以通过上面的命令强行删除；

### 查看远程库的信息

```bash
$ git remote
```

显示更详细的信息：

```bash
$ git remote -v
```

### 推送分支

推送master到远程库

```bash
$ git push origin master
```

推送branch1到远程库

```bash
$ git push origin branch1
```

### 创建本地分支

```bash
$ git checkout -b branch1 origin/branch1
```

说明：如果远程库中有分支，clone之后默认只有master分支的，所以需要执行如上命令来创建本地分支才能与远程的分支关联起来；

### 指定本地branch1分支与远程origin/branch1分支的链接

```bash
$ git branch --set-upstream branch1 origin/branch1
```

作用：如果你本地新建的branch1分支，远程库中也有一个branch1分支(别人创建的)，而刚好你也没有提交过到这个分支，即没有关联过，会报一个`no tracking information`信息，通过上面命令关联即可；

### 创建标签

```bash
$ git tag <name>
```

例如：`git tag v1.0`

#### 查看所有标签：

```bash
$ git tag
```

对历史提交打tag

先使用`$ git log --pretty=oneline --abbrev-commit`命令找到历史提交的commit id

例如对commit id 为123456的提交打一个tag:

```bash
$ git tag v0.9 123456
```

#### 查看标签信息：

```bash
$ git show <tagname>
```

eg:`git show v1.0`

#### 创建带有说明的标签，用-a指定标签名，-m指定说明文字，123456为commit id：

```bash
$ git tag -a v1.0 -m "V1.0 released" 123456
```

#### 用私钥签名一个标签：

```bash
$ git tag -s v2.0 -m "signed V2.0 released" 345678
```

说明：签名采用PGP签名，因此，必须先要安装gpg（GnuPG），如果没有找到gpg，或者没有gpg密钥对，就会报错，具体请参考GnuPG帮助文档配置Key；

作用：用PGP签名的标签是不可伪造的，因为可以验证PGP签名；

#### 删除标签：

```bash
$ git tag -d <tagname>
```

#### 删除远程库中的标签：

> 比如要删除远程库中的 **V1.0** 标签，分两步：

> > 1. 先删除本地标签：`$ git tag -d V1.0`

> > 2. 再推送删除即可：`$ git push origin :refs/tags/V1.0`

#### 推送标签到远程库：

```bash
$ git push origin <tagname>
```

#### 推送所有标签到远程库：

```bash
$ git push origin --tags
```

### 自定义Git设置

Git显示颜色，会让命令输出看起来更清晰、醒目：

```bash
$ git config --global color.ui true
```

设置命令别名：

```bash
$ git config --global alias.st status
```

说明：--global表示全局，即设置完之后全局生效，st表示别名，status表示原始名

好了，现在敲`git st`就相当于是`git status`命令了，是不是方便？

当然还有其他命令可以简写，这里举几个：很多人都用co表示checkout，ci表示commit，br表示branch...
根据自己的喜好可以设置即可，个人觉得不是很推荐使用别名的方式；

推荐一个比较丧心病狂的别名设置：

```bash
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

```

效果自己去体会...

其他说明：配置的时候加上--global是针对当前用户起作用的，如果不加只对当前的仓库起作用；每个仓库的Git配置文件都放在 **.git/config** 文件中，我们可以打开对其中的配置作修改，可以删除设置的别名；而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中，我们也可以对其进行配置和修改。

### 忽略文件规则

原则：

- 忽略系统自动生成的文件等；
- 忽略编译生成的中间文件、可执行文件等，比如Java编译产生的.class文件，自动生成的文件就没必要提交；
- 忽略你自己的带有敏感信息的配置文件，个人相关配置文件；
- 忽略与自己相关开发环境相关的配置文件；
- ...

使用：在Git工作区的根目录下创建一个特殊的 **.gitignore** 文件，然后把要忽略的文件名或者相关规则填进去，Git就会自动忽略这些文件，不知道怎么写的可参考：[github.com/github/giti…](https://github.com/github/gitignore),这里提供了一些忽略的规则，可供参考；

如果你想添加一个被 **.gitignore** 忽略的文件到Git中，但发现是添加不了的，所以我们可以使用强制添加`$ git add -f <file>`

或者我们可以检查及修改 **.gitignore** 文件的忽略规则：

```bash
$ git check-ignore -v <file>

```

Git会告诉我们具体的 **.gitignore** 文件中的第几行规则忽略了该文件，这样我们就知道应该修改哪个规则了；

如何忽略已经提交到远程库中的文件？
如果你已经将一些文件提交到远程库中了，然后你想忽略掉此文件，然后在 **.gitignore** 文件中添加忽略，然而你会发现并没有生效，因为Git添加忽略时只有对没有跟踪的文件才生效，也就是说你没有add过和提交过的文件才生效，按如下命令：

比如说：我们要忽略.idea目录，先删除已经提交到本地库的文件目录

```bash
git rm --cached .idea

```

格式：git rm --cached + 路径

如果提示：fatal: not removing '.idea' recursively without -r

加个参数 -r 即可强制删除

```bash
$ git rm -r --cached .idea

```

然后，执行`git status`会提示你已经删除.idea目录了，然后执行commit再push就可以了，此时的.idea目录是没有被跟踪的，将.idea目录添加到 **.gitignore** 文件中就可以忽略了。