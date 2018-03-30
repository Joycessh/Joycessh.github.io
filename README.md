# Joycessh.github.io

## 关于此版本库的介绍

### 创建的远程分支有hexo、master，hexo为默认分支。


- hexo分支用来存放网站的资源文件
- master分支用来存放部署的静态网页


>>> 搭建博客的基本流程

1. 先在机器安装好hexo，`npm install -g hexo-cli `

2. 创建仓库Joycessh.github.io，创建分支hexo（初始已有master分支），设置默认分支为hexo

3. 使用`git clone git@github.com:Joycessh/Joycessh.github.io.git`拷贝仓库，此时为默认分支hexo


4. Joycessh.github.io.git目录一般有.gtik、_comfig.yml和index.md，把.git文件复制出来，删除掉 _comfig.yml和index.md文件。此时Joycessh.github.io.git目录为空，执行`hexo init`（建立博客所需的文件）、`npm install` （安装依赖包），把之前复制出来.git文件黏贴回去进行覆盖


>>到这里，Hexo博客已经搭建好了本地的服务，执行命令`hexo g`和`hexo s --debug`在浏览器中输入localhost:4000就可以看到博客主页了

1. 关联Github Piges，编辑_config.yml文件，修改：

        #Deployment
        ##Docs: https://hexo.io/docs/deployment.html
          deploy:
          type: git
          repository: https://github.com/Joycessh/Joycessh.github.io
          branch: master

2. 为了能够使Hexo部署到GitHub上，需要安装一个插件：

   `npm install hexo-deployer-git --save`

3. 平时工作都是在分支hexo，并不影响部署。执行命令`hexo g -d`在浏览器输入Joycessh.github.io ,即可看到博客首页

4. 推送网站相关的文件

```
    git status #查看本地文件的状态
    git add . #将所有更新的本地文件添加到版本控制系统中
    git commit -m '更新信息说明' #提交
    git push origin hexo #推送到远程仓库

```

> 同步源码到其他电脑

1. 安装hexo`npm install hexo`，使用`git clone git@github.com:Joycessh/Joycessh.github.io.git`拷贝仓库，默认分支为hexo，在Joycessh.github.io.git目录下执行下面代码：

```
   npm install
   npm install hexo-deployer-git --save

```
--------------------------------
