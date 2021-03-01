---
title: Hexo搭建个人博客并部署到Github
tags:
  - 博客
  - hexo
  - GitHub
categories: 
 - hexo
---

# GitHub+Hexo 搭建个人网站详细教程

### **前言:**

随着互联网浪潮的翻腾，国内外涌现出越来越多优秀的社交网站让用户分享信息更加便捷。然后，如果你是一个不甘寂寞的程序猿（媛），是否也想要搭建一个属于自己的个人网站，如果你曾经或者现在正有这样的想法，请跟随这篇文章发挥你的Geek精神，让你快速拥有自己的博客网站，写文章记录生活，享受这种从0到1的过程。

### 什么是Hexo

![hexo-logo](https://sen7es.github.io/images/hexoCreate/hexo-logo.png)



Hexo是一款基于Node.js的静态博客框架，依赖少易于安装使用，可以方便的生成静态网页托管在GitHub和Heroku上，是搭建博客的首选框架。这里我们选用的是GitHub，你没看错，全球最大的同性恋交友网站（逃……）。Hexo同时也是GitHub上的开源项目，参见：[hexojs/hexo](https://link.zhihu.com/?target=https%3A//github.com/hexojs/hexo) 如果想要更加全面的了解Hexo，可以到其官网 [Hexo](https://link.zhihu.com/?target=https%3A//hexo.io/) 了解更多的细节，因为Hexo的创建者是台湾人，对中文的支持很友好，可以选择中文进行查看。这里，默认各位猿/媛儿都知道GitHub就不再赘述。

下面正式从零开始搭建年轻人的第一个网站。

<escape><!-- more --></escape>

### **搭建步骤：**

- 获得个人网站域名

- GitHub创建个人仓库

- 安装Git

- 安装Node.js

- 安装Hexo

- 推送网站

- 绑定域名

- 更换主题

- 初识MarkDown语法

- 发布文章

- 寻找图床

- 个性化设置

- 其他

- 附录

  

#### **GitHub创建个人仓库**

登录到GitHub,如果没有GitHub帐号，使用你的邮箱注册GitHub帐号：[Build software better, together](https://link.zhihu.com/?target=https%3A//github.com/) 点击GitHub中的New repository创建新仓库，仓库名应该为：**用户名**.[http://github.io](https://link.zhihu.com/?target=http%3A//github.io) 这个**用户名**使用你的GitHub帐号名称代替，这是固定写法，比如我的仓库名为：

![](https://sen7es.github.io/images/hexoCreate/v2-832168e58b4ac4ce7c3cca797711d2d3_720w.jpg)



#### **安装Git**

什么是Git ?简单来说Git是开源的分布式版本控制系统，用于敏捷高效地处理项目。我们网站在本地搭建好了，需要使用Git同步到GitHub上。如果想要了解Git的细节，参看[廖雪峰](https://link.zhihu.com/?target=http%3A//weibo.com/liaoxuefeng)老师的Git教程：[Git教程](https://link.zhihu.com/?target=http%3A//www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000) 从Git官网下载：[Git - Downloading Package](https://link.zhihu.com/?target=https%3A//git-scm.com/download/win) 现在的机子基本都是64位的，选择64位的安装包，下载后安装，在命令行里输入git测试是否安装成功，若安装失败，参看其他详细的Git安装教程。安装成功后，将你的Git与GitHub帐号绑定，鼠标右击打开Git Bash

![](https://sen7es.github.io/images/hexoCreate/v2-8b1cbe253d6e0301bd9a68c6f98a9f52_720w.jpg)



或者在菜单里搜索Git Bash，设置user.name和user.email配置信息：

```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```

生成ssh密钥文件：

```bash
ssh-keygen -t rsa -C "你的GitHub注册邮箱"
```

然后直接三个回车即可，默认不需要设置密码
然后找到生成的.ssh的文件夹中的id_rsa.pub密钥，将内容全部复制  

![](https://sen7es.github.io/images/hexoCreate/v2-d1e47103ec1aa8675f68688c5d63bd27_720w.jpg)



打开[GitHub_Settings_keys](https://link.zhihu.com/?target=https%3A//github.com/settings/keys) 页面，新建new SSH Key 

![](https://sen7es.github.io/images/hexoCreate/v2-72a3f22c080e99343c3cc4aabce10e3c_720w.jpg)

Title为标题，任意填即可，将刚刚复制的id_rsa.pub内容粘贴进去，最后点击Add SSH key。
在Git Bash中检测GitHub公钥设置是否成功，输入 ssh git@github.com ：  

![](https://sen7es.github.io/images/hexoCreate/v2-da481ffa686410becd4186c656b4ebd6_720w.jpg)



如上则说明成功。这里之所以设置GitHub密钥原因是，通过非对称加密的公钥与私钥来完成加密，公钥放置在GitHub上，私钥放置在自己的电脑里。GitHub要求每次推送代码都是合法用户，所以每次推送都需要输入账号密码验证推送用户是否是合法用户，为了省去每次输入密码的步骤，采用了ssh，当你推送的时候，git就会匹配你的私钥跟GitHub上面的公钥是否是配对的，若是匹配就认为你是合法用户，则允许推送。这样可以保证每次的推送都是正确合法的。

![](https://sen7es.github.io/images/hexoCreate/v2-76ea38e9545e606f975781e47933b010_720w.jpg)



检测npm是否安装成功，在命令行中输入npm -v :

![](https://sen7es.github.io/images/hexoCreate/v2-bede250b8456df92475b455fda8c1dd9_720w.jpg)



到这了，安装Hexo的环境已经全部搭建完成。

#### **安装Hexo**

Hexo就是我们的个人博客网站的框架， 这里需要自己在电脑常里创建一个文件夹，可以命名为Blog，Hexo框架与以后你自己发布的网页都在这个文件夹中。创建好后，进入文件夹中，按住shift键，右击鼠标点击命令行

![](https://sen7es.github.io/images/hexoCreate/v2-a5450a466c0927c25dff8ad6f1d2046c_720w.jpg)



使用npm命令安装Hexo，输入：

```bash
npm install -g hexo-cli 
```



这个安装时间较长耐心等待，安装完成后，初始化我们的博客，输入：

```bash
hexo init blog
```

注意，这里的命令都是作用在刚刚创建的Blog文件夹中。

为了检测我们的网站雏形，分别按顺序输入以下三条命令：

```bash
hexo new test_my_site

hexo g

hexo s
```

这些命令在后面作介绍，完成后，打开浏览器输入地址：

localhost:4000

可以看出我们写出第一篇博客，只不过我下图是我修改过的配置，和你的显示不一样。 

![](https://sen7es.github.io//images/hexoCreate/v2-123e73c0630d299b1c856d99b04b55bb_720w.jpg)



现在来介绍常用的Hexo 命令

npm install hexo -g #安装Hexo
npm update hexo -g #升级
hexo init #初始化博客
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本

命令简写
hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo g == hexo generate #生成
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署

hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令



刚刚的三个命令依次是新建一篇博客文章、生成网页、在本地预览的操作。

#### **推送网站**

上面只是在本地预览，接下来要做的就是就是推送网站，也就是发布网站，让我们的网站可以被更多的人访问。在设置之前，需要解释一个概念，在blog根目录里的_config.yml文件称为**站点**配置文件，如下图 

![](https://sen7es.github.io/images/hexoCreate/v2-cb1fd5e5a2e73f513234e434724c7c55_720w.jpg)

进入根目录里的themes文件夹，里面也有个_config.yml文件，这个称为**主题**配置文件，如下图  

![](https://sen7es.github.io/images/hexoCreate/v2-4252029e5634bf91c7d58916ae2b8ac3_720w.jpg)



下一步将我们的Hexo与GitHub关联起来，打开站点的配置文件_config.yml，翻到最后修改为：

deploy:
type: git
repo: 这里填入你之前在GitHub上创建仓库的完整路径，记得加上 .git
branch: master参考如下：  

![](https://sen7es.github.io/images/hexoCreate/v2-279ac5149b577f04dc099defbb12eaa8_720w.jpg)



保存站点配置文件。

其实就是给hexo d 这个命令做相应的配置，让hexo知道你要把blog部署在哪个位置，很显然，我们部署在我们GitHub的仓库里。最后安装Git部署插件，输入命令：

```basemake
npm install hexo-deployer-git --save
```



这时，我们分别输入三条命令：



```bash
hexo clean 
hexo g 
hexo d
```

其实第三条的 hexo d 就是部署网站命令，d是deploy的缩写。完成后，打开浏览器，在地址栏输入你的放置个人网站的仓库路径，即 [http://xxxx.github.io](https://link.zhihu.com/?target=http%3A//xxxx.github.io) (知乎排版可能会出现"http://"字样，参考下图) 比如我的xxxx就是我的GitHub用户名：



![img](https://sen7es.github.io/images/hexoCreate/v2-d750452f4258bf0967d5629ef23d1b10_720w.jpg)

你就会发现你的博客已经上线了，可以在网络上被访问了。

