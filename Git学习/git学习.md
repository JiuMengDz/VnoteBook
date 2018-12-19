# 1. git学习
## 1.1. 基础
### 1.1.1. 创建目录
$ mkdir learngit
### 1.1.2. 进入所在目录
$ cd learngit
### 1.1.3. 查看当前目录路径
$ pwd
### 1.1.4. 1.4.把目录添加入git仓库中
$ git init

## 1.2. 版本回退命令
$ git log
查看历史版本信息

$ git reset --hard HEAD^
回退到上一个版本
HEAD^^ 回退到上两个版本
HEAD~100 回退到上100个版本

$ git reset --hard 1094a(版本号前几位)
回退到指定版本号位置

$ git reflog  
查看历史修改记录

## 1.3. 暂存区 工作区
### 1.3.1. 工作区
电脑能看到的目录属于工作区
### 1.3.2. 暂存区
通过git add添加的文件都会暂时存放在暂存区内
通过git commit一次性将所有修改添加到master主文件区内

## 1.4. 删除文件
### 1.4.1. 确认删除
$ git rm [file name]
### 1.4.2. 错误删除，恢复文件
$ git checkout -- [file name]

## 1.5. 远程推送
### 1.5.1. 先创建一个SSH秘钥
### 1.5.2. 添加秘钥到github账户SSH列表中
### 1.5.3. 创建一个新的git仓库
### 1.5.4. 将本地文件推送到远程仓库
$ git remote add origin git@github.com:JiuMengDz/learngit.git
关联远程仓库
$ git push -u origin master
将本地库远程推送到github仓库中

## 1.6. 远程克隆
$ git clone git@github.com:JiuMengDz/gitskills.git
克隆gitskills库到本地文件夹中

## 1.7. 分支开发
### 1.7.1. 创建分支
$ git checkout -b dev
创建并切换到新的分支 , -b 表示创建并切换到当前分支
$ git branch dev      创建dev分支
$ git checkout dev      切换到分支dev

$ git branch
列出当前所有的分支
### 1.7.2. 合并分支并删除分支
$ git checkout master 
切换到master分支
$ git merge dev
合并dev分支到master分支

$ git branch -d dev
删除dev分支

### 1.7.3. 强行删除分支
$ git branch -D feature-vulcan
强行删除，需要使用大写D

## 1.8. 美观
git rebase

## 1.9. 打标签，更易于寻找版本
### 1.9.1. 创建标签
|                    代码                     |                  说明                   |
| :-----------------------------------------: | :-------------------------------------: |
|              git tag [tagname]              |    插入标签tagname到目前最新的commit上    |
|          git tag [tagname] 4c805e2          |      插入标签tagname到4c805e2位置上       |
| git tag -a [tagname] -m "此处写说明" 4c805e2 | 插入标签tagname到4c805e2位置上，并添加说明 |

### 1.9.2. 删除标签
$ git tag -d v0.1
删除指定标签

推送标签到远程
$ git push origin v1.0
推送所有未推送的标签到远程
$ git push origin --tags

### 1.9.3. 删除远程标签
#### 1.9.3.1. 先本地删除
$ git tag -d v0.9
#### 1.9.3.2. 再删除远程标签
$ git push origin :refs/tags/v0.9