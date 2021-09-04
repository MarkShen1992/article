# Git学习笔记

## Git的下载和安装

- [Git官网](https://git-scm.com/)
- 用户可以根据自己的需求，选择不同操作系统的Git下载使用
- 特点
  - 最优的存储能力
  - 高性能
  - 开源
  - 备份容易
  - 支持离线操作（本地仓库，远程仓库）
  - 很容易制作工作流程
- 与之相关的远程仓库
  - [Github](https://www.github.com)
  - [Gitlab（CI特性）](https://about.gitlab.com/)
  - [码云](https://gitee.com/)
  - [coding.net](https://coding.net)

## Git使用配置

- 配置全局用户名和邮箱

```
git config --global user.name "userName"
git config --global user.email "email address"

# config 的三个作用域
-- local
-- global
-- system

优先级：local > global

# 显示config 的配置，加 --list
git config --list --local|global|system
```

- 重置用户名和密码

```
git config --system --unset credential.helper
```

- Git永久保存账号密码

```
git config --global credential.helper store
```

## 建Git仓库

- 把已有的项目代码纳入Git管理

```
git init demo
cd demo

cp ../readme .
git add readme
git status
git commit -m "Add readme"
git log
```

## 往仓库里添加文件

- **工作区 =》暂存区 =》 版本历史**

​             git add files    git commit

- 4次提交，一个像模像样的静态页面生成了

```
# 暂存区状态查看
git status

# 添加文件到暂存区
git add file
git add -u

# 把暂存区中的文件提交到 历史版本
git commit -m'add files'

# 查看历史记录
git log
```

## 文件重命名

- Git 重命名文件

```
mv a a.txt
git add a.txt
git rm a
git status

# 可怕的命令
git reset --hard

# 重命名
git mv a a.txt
git commit -m'move a to a.txt'
```

## Git的版本历史如何看

```
git log --oneline
git log -n4 --oneline

# 查看本地有多少分支
git branch -v

# 创建分支
git checkout -b temp 415c5c8086e16399

# 工作区直接到版本历史库中
git commit -am'add temp'

# 查看有多少个分支
git branch -av

# 查看当前分支历史
git log

# 所有分支日志
git log --all --graph
```

## 图形界面查看版本历史

Patch/Tree

作者/提交人/Parent

## 探秘 `.git`

```
cat HEAD

# 切换分支
git checkout master

cat config
cat refs

# 类型
git cat-file -t aceled38a92b
# 内容
git cat-file -p aceled38a92b
```

## commit, tree和blob

- [commit, tree and blob](https://blog.csdn.net/liyazhen2011/article/details/89428602)
- 一个commit对应一棵树，文件内容相同就是一个东西

## 分离头指针情况下的注意事项

- 使用场景：想做些变更，但是不一定是正是变更
- HEAD 指向某个具体的commit的时候，产生分离头指针的情况

## 进一步理解HEAD和branch

```
git checkout -b newbranch # 创建新分支并直接切换过去
git diff asjfdlsajl askdjflska
git diff HEAD HEAD^^
git diff HEAD HEAD~2
```

## 如何删除不需要的分支

```
git branch -d jasdjfsa
git branch -D sdadjfsa
git branch -av
```

## 如何修改最近commit的message

```
git commit --amend
```

## 如何修改之前commit的message

```
git rebase -i 被变更的上一个commit
```

## 如何将多个commit合成一个

```
git rebase -i 所有需要变更的 commit 的前一个commit
```

## 如何把间隔的几个commit合成一个

```
git rebase -i saflsa
```

## 如何比较暂存区和HEAD所含文件的差异

```
vi index.html
git status
git diff --cached
```

## 怎么比较工作区和暂存区所含文件的差异

```
git diff
git diff -- readme.md # 指定某个具体文件
```

## 如何让暂存区恢复成和HEAD的一样

```
git reset HEAD  # 暂存区 => 工作区
```

## 如何让工作区的文件恢复成和暂存区一样

```
git checkout -- index.html
```

## 如何取消暂存区部分文件的更改

```
git reset HEAD -- index.html
```

## 消除最近几次提交(工作区、暂存区)

```
git reset --hard sfalsajflsajdl  # 慎用
git reset --hard HEAD
```

## 看看不同提交的指定文件的差异

```
# 分支比较
git diff master temp # 所有文件
git diff master temp -- index.html # index.html 文件
git diff sajfdsladjf safjsfjasdl -- index.html 文件
```

## 正确删除文件的方法

```
git rm readme
```

## 开发中临时加塞了紧急任务怎么处理

```
git stash
git stash list
git status

git stash apply # 把 stash 命令操作后的内容弹出来，继续修改；同时，stash 堆栈内的内容还在，不会被删除
git stash pop # 把 stash 命令操作后的内容弹出来，继续修改；同时，stash 堆栈内的内容不存在，会被删除
```

## 如何指定不需要Git管理的文件

`.gitignore` 文件

[gitignore official configuration](https://github.com/github/gitignore)

## 如何将 Git 仓库备份到本地

| 常用协议      | 语法格式                                       | 说明                   |
| :------------ | ---------------------------------------------- | ---------------------- |
| 本地协议（1） | /path/to/repo.git                              | 哑协议                 |
| 本地协议（2） | file:///path/to/repo.git                       | 智能协议               |
| http/https    | http(s)://git-server.com:port/path/to/repo.git | 平时接触到都是只能协议 |
| ssh           | user@git-server.com:path/to/repo.git           | 工作中最常用的只能协议 |

哑协议传输进度不可见，智能可见；且只能协议传输速度大于哑协议；工作中使用智能协议

Git是一个分布式代码版本控制系统。

```
git clone --bare [绝对路径]/.git backup.git
git clone --bare file:///[绝对路径]/.git backup.git

# 与远程仓库关联
git remote add ai file:///[绝对路径]/backup.git
git push ai
git push --set-upstream ai backup
```

## Github 注册

www.github.com

## 配置好公钥私钥

https://docs.github.com/en

## 在Github中创建一个仓库

https://docs.github.com/en

## 本地仓库同步到远端仓库

```
git remote add github https://github.com/git201901/git_learning.git
git pull
git push
git fetch github master
```

### 如何切换 https 方式 to ssh 方式

```
# 需求：由于 Github 最近添加了不同的认证方式，Two-factor authentication. 所以，我也想把 git 推代码的方式由 https 的方式编程ssh的方式。步骤如下：

# step 01: 首先同步代码，使得远程仓库的代码和本地仓库一致
git pull

# step 02: 移除当前远程仓库
git remote remove origin

# step 03: 重新设置远程仓库
git remote add origin git@github.com:MarkShen1992/article.git

# step 04: 指定远程仓库的分支
git branch --set-upstream-to=origin/master

# 这四步都执行完后就算完成了切换。当然，变成 ssh 的方式的前提是已经设置了 key. 这时很重要的，如有代理，需确认端口号是否一致。
```

## 不同人修改了不同文件如何处理

```
在两个人协同工作的时候首先要做的是：
git pull
修改文件 commit
git push
git pull

# fetch 与 pull 的区别
fetch 不自动合并，需要使用 git merge 命令
pull 自动合并（推荐使用）
```

## 不同人修改了同一个文件不同区域

```
在两个人协同工作的时候首先要做的是：
git pull
修改文件 commit
git push
git pull

# fetch 与 pull 的区别
fetch 不自动合并，需要使用 git merge 命令
pull 自动合并（推荐使用）
```

## 不同人修改了同一文件的同一区域

```
# 冲突解决
在两个人协同工作的时候首先要做的是：
git pull
修改文件 commit
git push
git pull

# fetch 与 pull 的区别
fetch 不自动合并，需要使用 git merge 命令
pull 自动合并（推荐使用）

# 编辑冲突文件
git commit -m'resolved conflicts'
```

## 同时变更了文件名和文件内容如何处理

```
git mv index.html index.htm
git pull
```

## 把同一文件改成了不同的文件名如何处理

```
做好沟通，逐个文件处理
```

## 禁止向集成分支执行 `push -f` 操作

```
git reset --hard asjfdasj
```

## 禁止向集成分支执行变更历史的操作

```
不要对应集成分支有 rebase 的行为
```

## Github 的核心功能

https://github.com/features

https://github.com/marketplace

## 找感兴趣的开源项目

- 一般搜索

- 高级搜索 https://github.com/search/advanced?q=java&type=Repositorie
- 搭建个人博客
- in:readme
- stars:>1000
- https://docs.github.com/en/free-pro-team@latest/github/searching-for-information-on-github

## 开源项目如何保存代码质量

https://www.jianshu.com/p/d9f217e1b09b

## 为何需要组织类型的仓库

`New Organization`

一个组织多个 `repositories`

团队加人，不同人不同权限

## 如何选择适合自己团队的工作流

- 考虑因素
  - 团队人员组成
  - 研发设计能力
  - 输出产品特征
  - 项目难以程度
- 主干开发
- CI/CD  /  DevOps
- Git Flow
  - https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
  - https://www.git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/git-flow/
  - http://www.ruanyifeng.com/blog/2015/12/git-workflow.html
  - https://datasift.github.io/gitflow/IntroducingGitFlow.html
  - https://nvie.com/posts/a-successful-git-branching-model/
  - https://jeffkreeftmeijer.com/git-flow/

## 如何挑选合适的分支集成策略

- `Insights` -> `Network` 
- `Settings` -> Merge button
  - merge commits
  - squash merging
  - rebase merging

## 启用issue跟踪需求和任务

- issues
  - CRUD

## 如何用project管理 issue

- project
  - new project
- kanban (敏捷团队)
  - https://trello.com/
  - `github` 自带的看板

## 项目内部如何做 `code review`

- `settings` -> `branches` 

## 团队协作时如何做多分支集成

- PR -> Merge

## 如何保证集成质量

- https://github.com/marketplace
- 提`PR`后，在合并确认的时候github会再跑下代码

## Github 发布产品包

- github release
- https://travis-ci.org

## 给项目增加文档

- wiki document