# git命令



#### 常用的基础操作

```bash
//最常用操作
git add .
git commit -m 'description'
git push
```

合并到主分支

```bash
git checkout master
git merge origin/index-swiper
git push
```

```bash
// 拉取
git pull
// 切换分支
git checkout index-swiper
// 可选 查看目前分支文件
git status
//运行
npm run start

```



#### 操作具体说明

查询当前远程的版本

```bash
git remote -v
```

将新建的文件或修改过的文件添加到索引库

```bash
git add .
```

本地分支代码保存到本地仓库

```
git commit -m "注释"
```

直接拉取并合并最新代码

```bash
git pull origin master  #拉取远端origin/master分支并合并到当前分支

git pull origin dev #拉取远端origin/dev分支并合并到当前分支
```

从本地提交代码到服务器

```bash
git push origin master #将当前分支提交到远端origin/master分支 push到GitHub的文件要求小于100M
```


撤销本地修改
```bash
#撤销对所有已修改但未提交的文件，不包括新增的文件
git checkout 
#撤销对指定文件的修改，<file> 为文件名
git checkout <file>

```

任何时候查看文件git文件流转当前状态

```shell
git status
```

添加文件到暂存区

```shell
git add <file>
git add . #添加所有文件（改动文件）
```

从暂存区删除文件（添加了无用文件）

```shell
git restore --staged  <file>
git reset <file>  #效果一样
复制代码
```

删除或移动、重命名文件，并自动提交到暂存区。用于处理已提交到仓库的文件

```shell
git rm|mv <file>
```

提交修改到本地仓库

```shell
git commit -m "change to..."
git commit -am "change to ..." #用于直接提交修改文件，无法提交新增文件
```

撤销某次提交（会在分支上长生一次commit记录）

```shell
git revert <commit>
```

查看提交记录

```shell
git log
git log --graph #图形化查看
git blame <file> #列表的方式查看指定文件修改历史
```

查看文件修改或区别

```shell
git diff #暂存和工作区所有差别  
git diff <file>  #查看指定文件
git diff HEAD -- <file>  #查看工作区和版本库里面最新版本的区别
```

使用`git reset` 回退项目版本

```shell
git reset <commitid> #我们使用git log查询到需要回退版本的commitid
git reset HEAD~1 #回退到上一个版本
git rest HEAD~n #回退到前n个版本
```

提交修改到远程仓库

```shell
git push  #提交有冲突时需要拉取远程最新版本
git push orgin master #将本地master分支提交到远程master分支
git push -u orgin master #提交并关联（适用于从本地创建的仓库）
```

拉取远程仓库最新版本

```shell
git pull  #拉取合并

git fetch #拉取不合并

git pull --rebase  #不会产生merge记录，保持分支干净卫生
git add <conflict-file>  #添加解决的冲突的文件
git rebase --continue  #解决冲突后继续rebase
```

git如何在不提交本地修改的前提下，拉取远程最新代码

```bash
git stash list #查看本地的暂存区栈

git stash #暂存本地修改

git pull #拉取最新代码

git stash pop #或者可以使用：git stash apply stash@{0}  :回到拉取之前的本地状态；此时若出现文件冲突，酌情解决即可；至于是git stash apply stash@{0} 还是git stash apply stash@{1} ，可以通过 git stash list 查看去确定。
git stash clear #可选 清空本地暂存栈信息
```



初始化一个仓库

```shell
git init myrepo
```

克隆一个仓库到本地myrepo目录

```shell
git clone git://github.com/linux/linux.git myrepo
git remote add origin git://github.com/linux/linux.git #指定（关联）远程仓库地址，适用于从本地创建的仓库
```

