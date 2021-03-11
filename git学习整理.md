 # windows下git使用

本文只专注于git使用，不包含其他诸如mkdir、cd、cat等操作命令
现在github默认主分支由之前的master更改为main，本文将使用main
- [windows下git使用](#windows下git使用)
  - [1. git初始化设置](#1-git初始化设置)
  - [2. SSH](#2-ssh)
    - [2.1. 生成SSH](#21-生成ssh)
    - [2.2. SSH警告](#22-ssh警告)
  - [3. 本地与远程连接](#3-本地与远程连接)
    - [3.1. 将本地仓库添加到远程库](#31-将本地仓库添加到远程库)
    - [3.2. 从远程库clone到本地](#32-从远程库clone到本地)
  - [4. 本地修改推送到远程](#4-本地修改推送到远程)
  - [5. 分支管理](#5-分支管理)
  - [6. 参考文章](#6-参考文章)
## 1. git初始化设置
定义本地名字与邮箱
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
--global参数：这台机器上所有git仓库都会使用这个配置
## 2. SSH
进行本地仓库和远程仓库的同步管理，需要使用SSH。SSH保存在~/.ssh目录下，为`id_dsa`或`id_rsa`,带有`.pub`拓展名的是公钥，不带的是私钥
### 2.1. 生成SSH
1. 生成单个SSH key
   输入生成代码
   ```
   例子
   $ ssh-keygen -C "youremail@example.com"
   # 参数解释
   -t 加密方式，包含rsa与dsa,默认rsa
   -C 设置注释文字，比如邮箱
   -f 指定密钥文件存储文件名，推荐不设置，会生成默认名id_rsa和id_rsa.pub
   ```
   运行后提示设置之后push时需要输入的密码，可留空直接回车，之后push时可直接提交
   ```
   Your identification has been saved in /c/Users/you/.ssh/id_rsa.
   # Your public key has been saved in /c/Users/   you/.ssh/id_rsa.pub.
   # The key fingerprint is:
   #    01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:d   b your_email@example.com
   ```
   出现上述代码提示则表示创建成功
   之后登陆GitHub，打开“Account settings”，“SSH Keys”页面。然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容,点“Add Key”，可看到已经添加的Key
2. 生成多个ssh
   待整理学习

   解决同一台电脑生成两份或多份ssh密钥、公钥映射两个或多个GitHub账号  
   https://blog.csdn.net/myNameIssls/article/details/80516577

   git中ssh-agent多密钥配置详解  
   https://blog.csdn.net/u011679955/article/details/86634246
### 2.2. SSH警告
第一次使用git的clone和push命令时，会有一个警告
```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```
输入yes即可

## 3. 本地与远程连接

本地与远程连接有两种模式，
1.将本地仓库添加到远程库；
2.从远程库clone到本地

### 3.1. 将本地仓库添加到远程库

1. 建立本地仓库
   ```
   $ git init
   ```
   在本地仓库目录下运行Git Bash Here,输入此代码，会出现一个".git"文件夹
2. 关联远程库
   获取一个github空仓库地址（可以新建一个），运行命令
   ```
   $ git remote add <shortname> <url>
   # <shortname>对url的命名，之后可以用此命名来代替url，通常为origin(远程库)

   # 例子
   $ git remote add origin git@github.com:githubid/repo.git
   $ git remote add origin https://github.com/githubid/repo.git
   ```
3. 同步(push)
   ```
   $ git push <local_branch>:<remote_branch>

   # 例子
   $ git push -u origin main
   # 第一次推送时加上-u参数，推送并关联本地与远程分支
   $ git push origin main 
   # 之后推送可以不用加-u参数
   ```
### 3.2. 从远程库clone到本地
已经有远程库的情况下，在工作目录运行Git Bash Here，输入命令
```
$ git clone <url>

#例子
$ git clone git@github.com:githubid/repo.git
$ git clone https://github.com/githubid/repo.git
```

## 4. 本地修改推送到远程
1. 添加修改到咱暂存区
   ```
   # 添加单个文件
   $ git add <filePath>
   # 添加所有文件
   $ git add .
   ```
   此命令会把工作时的变化提交到暂存区，包括文件内容修改(modified)以及新文件(new)，但不包括被删除的文件。
2. 提交修改到本地仓库
   ```
   # 提交暂存区修改到仓库
   $ git commit -m "commit msg"

   # 跳过add步骤，直接将所有本地修改的文件提交到本地仓库，不包括新文件
   $ git commit -a -m "Changed some files"
   ```
3. 同步本地库到远程库
   ```
   $ git push <remote> <local_branch>:<remote_branch>

   # 例子
   $ git push origin main:main
   # 简写：添加到远程同名分支，如没有则新建
   $ git push origin main
   # 简写：添加当前分支到远程同名分支
   $ git push origin
   ```
## 5. 分支管理
1. 创建分支
   ```
   # 本地创建一个名叫test的分支
   $ git branch test
   # 创建并切换到新建分支
   $ git checkout -b test
   ```
2. 查看分支
   ```
   # 本地分支
   $ git branch 
   # 所有分支（包括远程）
   $ git branch -a
   ```
3. 切换分支
   ```
   # 表示从当前分支切换到name分支
   $ git checkout name 
   ```
4. 本地分支与远程分支关联
   ```
   git branch –set-upstream local_branch origin/remote_branch
   ```
5. 合并分支
   ```
   # 将name分支合并到当前分支
   $ git merge name
   ```
6. 重命名分支
   ```
   git branch -m old-branch-name new-branch-name
   ```
7. 删除分支
   ```
   # 删除本地分支
   $ git branch -d test
   # 删除远程分支。local_branch留空则表示删除远程remote_branch分支。
   $ git push origin :remote_branch
   ```

## 6. 参考文章
https://yangjiantao.github.io/2018/03/10/git%E5%AE%9E%E7%94%A8%E6%8A%80%E5%B7%A7/
