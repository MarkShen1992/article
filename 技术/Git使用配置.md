# Git使用配置

## 配置全局用户名和邮箱

```
git config --global user.name "userName"
git config --global user.email "email address"
```

## 重置用户名和密码

```
git config --system --unset credential.helper
```

## git永久保存账号密码

```
git config --global credential.helper store
```

未完待续... ...