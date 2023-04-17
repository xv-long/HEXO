---
title: Git命令大全
date: 2023-04-17 14:11:35
tags:
---
### git配置项查看

#### 1.检查Git版本

```bash
git -v  
```

#### 2.查看git配置信息

```bash
git config -list
```

#### 3.查询Git 用户名 邮箱   

```bash
git config --global user.name
git config --global user.email
注 :在config后加   --global 表示全局，

```

```bash
git config --global user.name
git config --global user.email
#没有--global表示只查询在当前项目
```

#### 4.配置全局用户名

```bash
git config --global user.name "你的用户名"

```

#### 5.配置全局邮箱

```bash
git config --global user.email "eamil@qq.com"

```

---

---

### 管理代码

#### 1.初始化 Git 储存

```bash
git init

```

#### 2.将工作区所有修改放入到暂存区

```bash
git add .
```

```bash
git add <文件名>  #将指定文件添加到暂存区
git add *.vue  # 提交所有 .vue 格式文件
git add -f <文件名>  # 强制添加 指定文件添加到暂存区

```

#### 3.将暂存区文件恢复到工作区

```bash
git reset -- .          # 从暂存区恢复所有文件到工作区
git reset <文件名>   # 从暂存区恢复指定到工作区
git reset --hard        # 把暂存区的修改退回到工作区

```

#### 4.查看工作区 & 暂存区的状态

```bash
git status

```

#### 5.撤销暂存区的修改

```bash
git rm --cached <file-name>  # 将本地暂存区的内容移除暂存区

```

#### 6.暂存区文件提交到本地仓库

```bash
git commit -m "备注"       # 将缓存区的所有文件提交到本地仓库
```

```bash
git commit <file-name> ... "备注"   # 将缓存区的指定文件提交到本地仓库
git commit -am '备注'      # 跳过暂存区域直接提交更新并且添加备注的记录信息
git commit --amend '备注'  # 使用一次新的commit，替代上一次提交，如果代码没有任何新变化，则用来修改上一次commit的提交记录信息

```

#### 7.撤销 commit 提交

```bash
git revert HEAD    # 撤销最近的一个提交(创建了一个撤销上次提交(HEAD)的新提交)

```

```bash
git revert HEAD^   # 撤销上上次的提交
```

### 查看日志

#### 1.查看历史提交记录   # 注：空格向下翻页，B向上翻页，Q退出

```bash
git log    # 查看历史commit记录

```

```bash
git log --oneline  # 以简洁的一行显示，包含简洁哈希索引值
git log --pretty=oneline # 查看日志且并且显示版本
git log --stat     # 显示每个commit中哪些文件被修改,分别添加或删除了多少行
```

#### 2.查看 分支合并图

```bash
git log --graph
```

#### 3.查看版本线图

```bash
git log --oneline --graph

```

### Git 提交回滚

#### 1.回滚到指定版本

```bash
git reset --hard 版本号 ## 回退到指定版本，不保留原更改代码
 
git revert 版本号  # 回退到指定版本，保留原更改代码，且生成新的提交

```

#### 2.回滚到上一个版本

```bash
git reset --hard HEAD~1  # 后退一个版本
# 注：~ 后面的数字表示回退多少个版本

```

### 分支管理

#### 1.查看分支

```bash
git branch            # 查看所有本地分支
git branch -r         # 查看所有远程分支
git branch -a         # 查看所有远程分支和本地分支
git branch --merged   # 查看已经合并的分支

```

#### 2.创建新分支

```bash
git branch <分支名称>  # 创建分支，依然停留在当前的分支

```

#### 3.切换分支

```bash
git checkout <分支名称>   # 切换到指定分支，并更新工作区

```

#### 4.创建分支并切换到该分支

```bash
git chechout -b <分支名称>  # 创建一个新的分支，并切换到这个新建的分支上

```

#### 5.合并分支

```bash
git merge <分支名称>  # 合并<指定分支>到当前分支

```

#### 6.删除分支

```bash
git branch -d <branch-name>    # 只能删除已经被当前分支合并的分支
git branch -D <branch-name>    # 强制删除分支

```

#### 7.删除远程分支

```bash
git push origin --delete  <远程分支名>  

```

### 远程仓库(多人协作)

#### 1.克隆远程仓库到本地(本地没有仓库时)

```bash
git clone 远程仓库地址

```

#### 2.本地仓库与远程仓库关联(本地有仓库)

```bash
git remote add origin 远程仓库地址

```

#### 3.查看远程仓库别名

```bash
git remote -v
```

#### 4.新建远程仓库别名

```bash
git remote add <origin> 远程仓库地址 

```

#### 5.删除本地仓库中的远程仓库别名

```bash
git remote rm <别名>

```

#### 6.重命名 远程仓库地址别名

```bash
git remote rename <旧别名> <新别名>

```

#### 7.把远程仓库代码拉取到本地

```bash
git pull # 已关联的本地仓库与远程仓库可以直接  拉取代码
```

```bash
git fetch <origin/url> <远程分支名称>   # 抓取远程仓库的指定分支到本地，但没有合并
git pull <origin/url> <远程分支名称>    # 拉取到本地，并且与当前所在的分支进行合并
# 注: <origin/url> 远程仓库的别名 或者是 远程仓库地址

```

#### 8.把本地代码上传到远程仓库

在推送前 要先拉去代码避免覆盖

```bash
git push # 已关联的本地仓库与远程仓库可以直接上传代码
```

```bash
git push <origin/url> <本地分支名>   # 将本地的每个分支推送到远程仓库
git push <origin/url> --force         # 强行推送 当前分支到远程仓库，即使有冲突
git push <origin/url> --all           # 推送所有本地分支到远程仓库
# 注: <origin/url> 远程仓库的别名 或者是 远程仓库地址

```

