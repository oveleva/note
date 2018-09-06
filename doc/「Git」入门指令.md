# git入门

## Git 创建仓库
```git
#repo:Git 仓库。
directory:本地目录。
# 当前目录
git init
# 指定目录
git init newrepo
# 从现有仓库拷贝
git clone <repo>
# 拷贝到指定目录
git clone <repo> <directory>
```

**参数说明：**
* repo:Git 仓库。
* directory:本地目录。


## 查看状态
```git
# -s 简短的结果
# --cached 尚已缓存的改动
# HEAD 查看已缓存的与未缓存的所有改动
# --stat 显示摘要
git diff 
```

## 添加到快照
```git
# 添加所有文件到缓存（可把.换为具体文件名，多个文件名用空格分割）
git add  .
```

## 添加到仓库
```git
# -a 自动添加快照再添加到仓库
# -m [备注]
git commit 
```