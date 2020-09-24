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
  - Github
  - Gitlab（CI特性）
  - 码云

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

- **工作目录 =》暂存区 =》 版本历史**

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

