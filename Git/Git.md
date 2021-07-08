# Git

### Git概述

Git本质上是一个版本控制工具

### Git基本操作

通过`git clone url`同步本地仓库

 ![image-20210708101142006](C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20210708101142006.png)

本地仓库同步到远程仓库步骤

1. 工作区为红色文件，通过`git status`查看状态
2. `git add`把工作区文件更新到缓存区，绿色文件
3. `git commit -m "注释"` 把缓存区文件加入到分支
4. `git push origin master` 把分支文件push到远程仓库的master分支上

* 第一次同步仓库时需要config一下用户名密码

```
git config --global user.email "@"
git config --global user.name "name"
```

远程仓库同步到本地仓库

`git pull origin master`

#### 常见问题-无法正常推送

如果远程仓库的代码高于本地仓库，则无法正常推送，需要先pull一下获取最新版本再推送。

### Git版本追溯

`git reset --hard 版本号`

所以在开发过程中，每次提交的备注commit应写明，而且每次开发完成后记得及时提交，或者每日提交。

### Git分支管理

不应在master分支上直接开发

最终发布版本在master分支，开发版本可以在develop分支。这样开发过程中不会给正式项目引入BUG。

* `git branch`查看分支
* `git branch develop`创建develop分支
* `git checkout develop`切换当前分支到develop分支
* `git push origin develop:develop`把本地develop分支提交到远程仓库develop分支，如果远程仓库没有develop分支会自动创建
* 合并分支，在当前master分支`git merge develop`合并develop分支，然后push到远端

### 配置公钥

C:\Users\Administrator\.ssh（Administrator是当前用户名）目录下

先配置用户名邮箱

```
$ git config --global user.name "your_name"
$ git config --global user.email "your_email@example.com"
```

生成密钥对

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

id_rsa.pub文件即为公钥

