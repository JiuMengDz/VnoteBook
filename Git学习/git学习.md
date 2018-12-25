# 1. 基础
git是分布式版本控制系统
![](_v_images/20181225115718928_27010.png =400x)

## 1.1. 配置用户的个人信息
$ git config --global user.name "John Doe"

$ git config --global user.email johndoe@example.com

如果使用了 --global 选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事情， Git 都会使用那些信息。 当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有 --global 选项的命令来配置。

检查用户配置目录: git config --list

## 1.2. 查询帮助
```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```
如

```
$ git help config
```

# 2. 实际操作
## 2.1. 查看当前目录路径
$ pwd
## 2.2. 将当前目录初始化为GIT仓库
$ git init

![文件的状态变化周期](_v_images/20181225152137429_30579.png =720x)


## 2.3. 查看当前git状态
$ git status

```
$ echo 'My Project' > README
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README

nothing added to commit but untracked files present (use "git add" to track)
```
可以看到新建的README文件处于未跟踪状态

**简短的status输出**
使用git status -s 或者--short
得到类似如下结果

```
$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```

其中  M在右边  被修改/未被放入暂存区
M在左边   被修改/已放入暂存区
A  新添加到暂存区文件
??  未被跟踪

## 2.4. 丢弃之前的更改

```
$ git checkout <filename>
```

## 2.5. 忽略文件
创建 .gitignore文件即可
**语法规范如下:**

- 所有空行或者以 ＃ 开头的行都会被 Git 忽略。
- 可以使用标准的 glob 模式匹配。
- 匹配模式可以以（/）开头防止递归。
- 匹配模式可以以（/）结尾指定目录。
- 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。


例子如下：  

```
# 忽略.a文件
*.a

# 只跟踪lib.a文件，即使前面已经忽略了.a文件
!lib.a

# 忽略当前目录下的TODO文件，而不是下一级目录的TODO文件
/TODO

# 忽略build目录下的全部内容
build/

# 忽略doc/*.txt  而不忽略doc/sever/*.txt
doc/*.txt

# 忽略doc目录下的所有.pdf文件
doc/**/*.pdf
```

## 2.6. 删除文件
删除文件后，会在status状态下看到文件的更改未提交状态
此时继续执行
git rm filename

可以移除git目录下的跟踪状态

在下一次提交的时候则不再继续纳入版本管理了

如果在删除之前已经将修改提交到了暂存区内，则需要使用强制删除选项 -f 或 --force 

这样的数据不能被Git恢复

如果希望把文件从git仓库中移除并必须保留在工作区而不被git继续跟踪，而这个文件又被放到了暂存区内
则需要使用

git rm --cached README


## 2.7. 提交文件文本信息

在打开的vim编辑器中，会默认第一行开始输入信息，也可以删除不写
退出编辑模式后会自动commit携带这部分的信息
也可以使用git commit -m "在这里输入你本次提交的具体说明"

**提交的内容是暂存区的内容，如果文件不在暂存区内，则仍然会继续保持其已修改状态**

## 2.8. 跳过暂存全部提交
使用 git commit -a 命令，则会将所有的跟踪文件一并提交，跳过git add步骤

# 3. 提交历史
```
$ git log
```
返回所有提交历史信息，最新的排列在最上面

[git log --pretty = format 常用选项](https://git-scm.com/book/zh/v2/ch00/rpretty_format)

[git log 常用选项](https://git-scm.com/book/zh/v2/ch00/rlog_options)

# 4. 撤销操作
## 4.1. 可逆的撤销操作
### 4.1.1. 漏掉文件、提交信息错误
```
$ git commit --amend
```
这个操作会覆盖之前的提交操作，修改其提交信息和结果   最终你只会有一个提交，第二次提交将代替第一次提交的结果
### 4.1.2. 取消暂存区的文件



## 4.2. 不可逆的撤销操作




# 5. 版本回退命令
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

# 6. 暂存区 工作区
## 6.1. 工作区
电脑能看到的目录属于工作区
## 6.2. 暂存区
通过git add添加的文件都会暂时存放在暂存区内
通过git commit一次性将所有修改添加到master主文件区内

# 7. 删除文件
## 7.1. 确认删除
$ git rm [file name]
## 7.2. 错误删除，恢复文件
$ git checkout -- [file name]

# 8. 远程推送
## 8.1. 先创建一个SSH秘钥
## 8.2. 添加秘钥到github账户SSH列表中
## 8.3. 创建一个新的git仓库
## 8.4. 将本地文件推送到远程仓库
$ git remote add origin git@github.com:JiuMengDz/learngit.git
关联远程仓库

$ git push -u origin master
将本地库远程推送到github仓库中

# 9. 远程克隆
$ git clone git@github.com:JiuMengDz/gitskills.git
克隆gitskills库到本地文件夹中

# 10. 分支开发
## 10.1. 创建分支
$ git checkout -b dev
创建并切换到新的分支 , -b 表示创建并切换到当前分支
$ git branch dev      创建dev分支
$ git checkout dev      切换到分支dev

$ git branch
列出当前所有的分支
## 10.2. 合并分支并删除分支
$ git checkout master 
切换到master分支
$ git merge dev
合并dev分支到master分支

$ git branch -d dev
删除dev分支

## 10.3. 强行删除分支
$ git branch -D feature-vulcan
强行删除，需要使用大写D

# 11. 美观
git rebase

# 12. 打标签，更易于寻找版本
## 12.1. 创建标签
|                    代码                     |                  说明                   |
| :-----------------------------------------: | :-------------------------------------: |
|              git tag [tagname]              |    插入标签tagname到目前最新的commit上    |
|          git tag [tagname] 4c805e2          |      插入标签tagname到4c805e2位置上       |
| git tag -a [tagname] -m "此处写说明" 4c805e2 | 插入标签tagname到4c805e2位置上，并添加说明 |

## 12.2. 删除标签
$ git tag -d v0.1
删除指定标签

推送标签到远程
$ git push origin v1.0
推送所有未推送的标签到远程
$ git push origin --tags

## 12.3. 删除远程标签
### 12.3.1. 先本地删除
$ git tag -d v0.9
### 12.3.2. 再删除远程标签
$ git push origin :refs/tags/v0.9