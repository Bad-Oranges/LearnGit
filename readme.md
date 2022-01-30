## 基本配置

```bash
git init  # 初始化
git config --global user.name "xxx"   # 配置用户名
git config --global user.email "xxx"  # 配置邮箱
git config --global core.ignorecase false  # 配置大小写敏感
git config --list  # 查看配置信息

```

### 创建ssh

```bash
ssh-keygen -t rsa -C "youremail@exaple.com" 
```

ssh文件默认路径`C:\Users\<User Name>\.ssh`

创建本机ssh之后可以在GitHub的settings里面添加,然后就可以连接GitHub仓库了

```bash
git remote add origin git@github.com:Bad-Oranges/LearnGit.git  #添加远程仓库
git branch -M main  # 创建主分支
git push -u origin main  # Origin表示远程仓库，main表示本地仓库
```



## 基本操作

```bash
ll -ah  # 查看文件列表，包括隐藏文件夹
git status  # 查看本地文件状态
git log  # 查看提交日志
git reflog  # 查看命令历史

git restore <file_name>  # 丢弃工作区的修改
git restore  # 丢弃工作区所有文件的修改
git restore --staged <file_name>  # 撤销暂存区的修改
git restore --source=HEAD~1  # 将工作区回滚至上n个版本
git restore --source=<commit> # 将工作区回滚至指定版本
```

## 文件状态

![image-20220130233742518](readme.assets/image-20220130233742518.png)

```bash
# 一般提交流程
git rm <file-name>  # 删除文件
git add <file-name>  # 将文件放入暂存区(此时文件状态为staged）
git add .  # 将所有放入暂存区(此时文件状态为staged）
git commit <file-name> -m "some messages"  # 将文件提交至本地仓库并备注信息
git commit <file-name> -am "some messages"  # 等同于git add . && git commit -m
## git commit --amend  # 修改上次提交的备注信息
git push  # 将文件从本地仓库提交到远程仓库

# 从远程仓库获取文件
git fetch <远程主机名> <分支名>  # 获取远程仓库特定分支的更新
git fetch --all  # 获取远程仓库所有分支的更新
git pull <远程主机名> <远程分支名>:<本地分支名>  # 等同于 git fetch && git merge
git pull --rebase <远程主机名> <远程分支名>:<本地分支名>  # 使用rebase的模式进行合并

# 远程仓库
git remote -v  # 查看远程仓库
git remote add 仓库名 地址  # 添加远程仓库
```





## 分支与标签管理

```bash
git branch  # 查看本地分支
git branch -r  # 查看远程分支
git branch -a  # 查看本地和远程分支


git switch -c <branch-name>  # 创建分支
git switch <branch-name>  # 切换分支
git branch -d <branch-nane>  # 删除本地分支
git branch -m <old-branch-name> <new-branch-name>  # 重新命名分支

git commit -am "some message"  # 分支内容提交和正常没有区别
git push --set-upstream origin <branch-name>  # 第一次提交时需要设置远程分支

git merge <branch-name>  # 以当前分支为主分支合并目标分支
```

![image-20220130231917886](readme.assets/image-20220130231917886.png)

### 分支策略

主分支仅用来发布新版本

dev分支负责开发工作

dev分支可以继续细分（按工作类型、人员）

### 标签管理

```bash
git tag  # 查看所有标签
git tag v1.0 (commmit ID)  # 创建标签(对指定Commit ID添加标签，SHA可以通过log查找)
git tag -a v0.1 -m (Commit ID)"version 0.1 released"   # 创建带有描述信息的标签
git show <tagname>  # 查看标签说明文字
git tag –d v0.1  # 删除指定标签

# 将本地标签发布到远程仓库
git push origin --tags  # 发送所有
git push origin 1.0.0  # 指定标签发送

# 删除远程仓库对应标签 （删除远程标签需要先删除本地标签！）
git tag -d v0.9
git push origin --delete v0.9  # Git版本 > V1.7.0
git push origin :refs/tags/v0.9  # 旧版本Git
```

## 其他

### commit message规范

[Git Commit 标准化 - 吴佰清 - 博客园](https://www.cnblogs.com/wubaiqing/p/10307605.html)

## 用什么规范？

现在市面上比较流行的方案是`约定式提交规范`（`Conventional Commits`），它受到了`Angular提交准则`的启发，并在很大程度上以其为依据。`约定式提交规范`是一种基于提交消息的轻量级约定。 它提供了一组用于创建清晰的提交历史的简单规则；这使得编写基于规范的自动化工具变得更容易。这个约定与`SemVer`相吻合，在提交信息中描述新特性、bug 修复和破坏性变更。它的 message 格式如下:

```text
<类型>[可选的作用域]: <描述>

[可选的正文]

[可选的脚注]
```
