---
title: 我是如何使用hexo+github pages搭建个人博客
tags:
  - Hexo
comments: true
date: 2018-04-01 11:30:40
categories:
password:
---
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

<!--more-->


## 搭建博客的基本流程

> 我所用的系统环境为deepin15.5，已经安装好Git。先检查电脑是否已经安装SSH：`ls -al ~/.ssh` ， 如果有id_rsa（私钥），id_rsa_pub（公钥）文件就表示安装好了。测试一下： `ssh -T git@github.com`


### 进入github主页新建一个仓库，格式：USERNAME.github.io
- 我们要设置主题，点击-setting，change theme 选择一个主题，发布
- 在浏览器输入USERNAME.github.io，你会看到博客主页

### 创建的远程分支有hexo、master，设置hexo为默认分支。
- hexo分支 #用来存放网站的资源文件
- master分支 #用来存放部署的静态网页


### 安装Hexo的流程
- 装Hexo需要安装Node.js、Git ，安装Node.js，下面是使用nvm安装的方法：
 `wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh `
  安装完成后，重启终端并执行命令`npm instal stable`即可安装 Node.js。

- 使用`npm install -g hexo-cli `安装Hexo

- 使用`git clone git@github.com:USERNAME/USERNAME.github.io.git`拷贝仓库，此时为默认分支hexo


- USERNAME.github.io.git目录一般有.git、_comfig.yml和index.md，把.git文件复制出来，删除掉 _comfig.yml和index.md文件。此时USERNAME.github.io.git目录为空，执行`hexo init`（建立博客所需的文件）、`npm install` （安装依赖包），把之前复制出来.git文件黏贴回去进行覆盖


>>到这里，Hexo博客已经搭建好了本地的服务，执行命令`hexo g`和`hexo s --debug`在浏览器中输入localhost:4000就可以看到博客主页了

### 关联Github Piges，编辑_config.yml文件，修改：

        #Deployment
        ##Docs: https://hexo.io/docs/deployment.html
          deploy:
          type: git
          repository: https://github.com/USERNAME/USERNAME.github.io
          branch: master

- 为了能够使Hexo部署到GitHub上，需要安装一个插件：

   `npm install hexo-deployer-git --save`

- 平时工作都是在分支hexo，并不影响部署。执行命令`hexo g -d`在浏览器输入USERNAME.github.io ,即可看到博客首页

### 推送网站相关的文件

```
    git status #查看本地文件的状态
    git add . #将所有更新的本地文件添加到版本控制系统中
    git commit -m '更新信息说明' #提交
    git push origin hexo #推送到远程仓库

```

> 同步源码到其他电脑

### 安装hexo`npm install hexo`，使用`git clone git@github.com:USERNAME/USERNAME.github.io.git`拷贝仓库，默认分支为hexo，在USERNAME.github.io.git目录下执行下面代码：

```
   npm install
   npm install hexo-deployer-git --save

```
> 使用其他主题的方法：
- 使用git clone拷贝到USERNAME.github.io/themes下,例如：
```
$ cd USERNAME.github.io #你的根目录
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```
- 再将站点配置文件_config.yml中的theme: landscape改为对应的主题名字。

```
## Themes: https://hexo.io/themes/

theme: next

```
- 主题的配置是在/themes/next/_config.yml文件里面

### Hexo常用命令：

 - hexo n "title" == hexo new "title" #新建文章,在source/_posts生成.md文件
 - hexo new page "pageName" #新建页面
 - hexo clean #清除缓存文件
 - hexo generate == hexo g #生成静态网页
 - hexo server == hexo s #开启服务，默认localhost：4000
 - hexo s --debug #启动本地站点，并开启调试模式
 - hexo deploy == hexo d #部署到Github Pages

### 发布文章的流程：
 - hexo new "title" #新建文章，使用markdown编辑器编写，如atom。或者直接把写好md文件放到source/_posts下
 - hexo generate #生成静态页面
 - hexo server #预览，localhost:4000
 - hexo deploy #部署到github（博文发布）

### 绑定阿里云域名
 - 先到阿里云注册一个域名，按提示来走就行，很简单。
 - 在source目录创建一个CNAME文件，内容是你的域名xxx.xyz。github会读取CNAME文件，将USERNAME.github.io重定向到xxx.xyz。当我们提交CNAME文件时，github就会帮我们自动部署了。
 - 进入阿里云管理控制台，云解析DNS，添加两条解析


记录类型|主机记录|解析线路|记录值
-|-|-|-
CNAME | www | 默认 | USERNAME.github.io
CNAME | @ | 默认  |  USERNAME.github.io

 - 这样配的好处是有无www都能访问你的网站
 - 等一会，刷新网页，神奇的事情就发生了：）


参考资料：

<http://theme-next.iissnan.com/getting-started.html>
<http://codepub.cn/2016/03/20/Hexo-blog-theme-switching-from-Jacman-to-NexT-Mist/>
<https://blog.csdn.net/MasterAnt_D/article/details/56839222>
<https://segmentfault.com/a/1190000002632530>
<http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html>

---------------------------------------------------
