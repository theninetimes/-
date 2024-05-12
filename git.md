**配置**

```bash
git config --global user.name 'songsonglin'//配置姓名
git config --global user.email 'swussl@163.com'//配置邮箱
```

**查看配置**

```bash
git config user.name#查看姓名
git config user.email#查看邮箱
```

**使用git**

在git中的文件有四种状态：

1.未跟踪 2.未修改 3.暂存 4.已修改

```bash
git init #初始化仓库
git status#查看当前仓库的状态
```

新添加的文件处于未跟踪状态

```bash
git add <file name>#未跟踪-->暂存
git add *#将所有已修改文件或者未跟踪文件添加到暂存区
git commit -m '....'#将暂存区的文件提交到git仓库，附带有提交信息  暂存-->未修改
git commit -a -m '....'#将所有已修改文件提交到仓库，未跟踪文件不会提交
```

**常用命令**

1.重置文件

```bash
git restore <filename>#将文件恢复到仓库中的状态
git restore --staged <filename>#取消暂存状态，只是将该文件从暂存区移除，并不做其他修改
```

2.删除文件

```bash
git rm <filename>
git rm <filename> -f#强制删除
```

3.移动 重命名文件

```bash
git mv from to  
```

**分支**

git在存储文件时，每一次代码提交都会创建一个节点，git通过一个一个节点来管理文件的状态。在git中，可以创建多个分支，分支与分支之间相互独立。默认情况下只有一个分支叫做master

```bash
git branch#查看当前分支
git branch <branch name>#创建新的分支
git branch -d <branch name>#删除分支
git switch <branch name>#切换分支
git switch -c <branch name>#创建并切换分支
git merge <branch name>#合并分支
```

**变基**

除了可以使用merge来合并还可以使用变基来合并

变基时发生了什么：

1.git会首先找到两条分支的公共祖先

2.对比当前分支相对于祖先的提交，并保存在一个临时文件中

3.将当前部分指向目标基底

4.以当前基底开始，执行历史提交

变基相对于合并的**优势**：是保持提交历史的整洁和线性，并且可以提高代码审查的质量。

```bash
#将feature分支合并到main分支上
git switch feature
git rebase main
```

**远程仓库**

```bash
git branch -M main#重命名当前分支
git remote add origin https://github.com/Wang-Phil/test.git#关联远程仓库，别名为origin
git push -u origin main#设置远程仓库的main分支为本地仓库main分支的上游分支，在提交时不需指定
```

远程仓库操作命令

```bash
git remote#查看关联的远程库
git remote add <仓库名> <url>#添加远程仓库
git remote remove <仓库名>#删除远程库
git push -u <远程仓库名> <本地分支名>#将本地分支和远程仓库的分支进行关联
git clone <url>#从远程仓库下载代码

git push #向远程仓库推送代码
git fetch #从远程仓库拉取最新代码，但是不会自动合并，需要调用merge合并代码
git pull #从远程仓库拉去最新代码，并且自动合并
```

**注**推送代码之前必须获取最新的代码

**tag标签**

当head指针没有指向某个分支的头部时，为分离头指针（head detached），这种情况下任何修改都不会出现在分支上，所以不应在分离头指针的情况下修改代码

如果要回到某个版本修改代码，可以分离头指针然后在头指针的位置创建新的分支

```bash
git switch -c test <版本id>
```

在这种情况下，版本id辨识度不高，所以可以为版本打上tag方便回到以前的版本

```bash
git tag#获取所有tag
git tag 版本#打标签
git tag 版本 提交id#给某个版本打上标签
git tag -d 标签名
git push <仓库名> tag
git push <仓库名> --tags#提交所有标签
git push <仓库名> -delete 标签名
```

在有标签的情况下，回到某个版本就很方便

```bash
git switch -c test <标签名>
```

**gitignore**

默认情况下git会跟踪所有的文件，但是类似node_modules的文件不希望被管理，所以我们需要配置gitignore来忽略类似的文件

.gitignore

```bash
node_modules#忽略node_modules文件夹
*.log#忽略所有的log文件
```

**github的静态网页**

我们可以将静态网页放到github上，GitHub会为我们的网页分配域名，这样可以供所有人访问

注：静态网页的分支必须为：gh-pages，如果希望通过xxx.github.io访问，则要将GitHub上的仓库名命名为xxx.github.io