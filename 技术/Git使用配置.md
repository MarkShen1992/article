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

把已有的项目代码纳入Git管理

```
git init demo
cd demo

cp ../readme .
git add readme
git status
git commit -m "Add readme"
git log
```

