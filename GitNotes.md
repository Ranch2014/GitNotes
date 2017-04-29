# GitNotes
Git 学习笔记及常用命令小结。



### 常用本地操作

- 初始化仓库

```basic
git init : 初始化 git 仓库
```

- 配置用户名和邮箱

设置自己的用户名与邮箱。执行以下代码：

```basic
git config --global user.name "***"
git config --global user.email "***@**.com"
```

- 添加及提交文件

```basic
git add <name> : 添加指定的文件
git add . : 添加所有文件

git commit -m "first commit" : 提交信息
```

- 日志

```basic
git log : 查看日志(较详细)
git log --pretty=oneline : 日志简化(只有 commit id 和提交信息)
git log --pretty=oneline --abbrev-commit : 日志简化(commit id 也简化了)

此外，有一个比较酷的查看历史记录的命令如下：
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative  
```

- 取别名

```basic
git config --global alias.ci commit : 给 commit 取别名 ci, 之后可以用 git ci 提交
```

- stash

```basic
git stash: 把当前分支没有 commit 的代码先暂存起来（保护现场）。
git stash list: 查看记录

git stash apply: 返回暂存前的状态 
git stash drop: 删除 stash 记录
	上面两句可以合并为下面一行代码：
git stash pop

git stash clear: 清空暂存区的记录
```

- 回退

```basic
git reset --hard HEAD^ : 回退到上个版本
git reset --hard HEAD^^ : 回退到上个版本
git reset --hard HEAD-10 : 向前回退 10 个版本
git reset --hard a25ffbd: 返回到回退之前的状态（注意要知道之前的 commit id, 不必写全，前几位即可）

git reflog: 查看命令历史记录（以便确定将操作回退到哪一个记录）。

git checkout -- readme.txt : 将 readme.txt 撤销到上一次操作（未提交到暂存区，即没有用 add 命令）
```

- 其他

```basic
git status : 查看状态

git rm —cached : 移除缓存（add 过，还没 commit 的操作）
```



### 分支

- 创建 & 切换分支

```basic
git branch : 查看分支
git branch -r : 查看远程分支

git branch <name> : 新建分支
git checkout <name> : 切换分支

git checkout -b <name> : 新建并切换到 name 分支 
```

- 合并分支

```basic
git merge <name> : 合并分支

这里有两个步骤：
1）切换到要合并的分支（例如 master 分支）；
2）执行 git merge <name> 意为将 name 分支合并到 master 分支。

合并分支时，加上 --no-ff 参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
例如：git merge --no--off -m “merge with no-ff” -dev
```

- 删除分支

```basic
git branch -d <name> : 删除分支
git branch -D <name> : 强制删除分支

PS: 有些时候可能会删除失败，比如 a 分支的代码还没有合并到 master，此时执行 git branch -d a 是删除不掉的，它会智能的提示你 a 分支还有未合并的代码，但是如果你非要删除，那就执行 git branch -D a 就可以强制删除 a 分支。
```

- 推送分支

```basic
git push origin <name>

git push origin master: 推送到远程 master 分支
git push origin develop : 推送到远程 develop 分支
```

- 克隆远程分支

```basic
git checkout -b dev origin/develop: 把远程 develop 分支克隆到本地
```



### 标签

- 创建 & 切换标签

```basic
git tag : 查看标签

git tag <tagname> : 新建标签(默认在最新提交的 commit)
git tag <tagname> 3302252: 给某个历史 commit 打 tag

还可以创建带有说明的标签，用 -a 指定标签名，-m 指定说明文字：
git tag -a <tagname> -m "version 0.1 released" 3628164

git checkout <tagname> : 切换标签
```

- 查看标签

```basic
git show <tagname> : 查看标签信息
```

- 推送到远程

```basic
git push origin <tagname> : 推送某个标签到远程
git push origin —tags : 一次推送全部尚未推送到远程的本地标签 
```

- 删除本地和远程标签

```basic
git tag -d <tagname>: 删除标签
git push origin :refs/tags/<tagname>
```



### 常用远程操作

- SSH

生成 SSH key：

终端输入 `ssh-keygen -t rsa`, 指定 rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），然后就会生成两个文件 id_rsa 和 id_rsa.pub ，id_rsa 是密钥，id_rsa.pub 就是公钥。这两文件默认在目录：`~/.ssh`



### 其他

- 忽略特殊文件

[忽略特殊文件](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013758404317281e54b6f5375640abbb11e67be4cd49e0000)

- 搭建 Git 服务器

[搭建 Git 服务器](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137583770360579bc4b458f044ce7afed3df579123eca000)





主要参考教程：

1. [从0开始学习 GitHub 系列](http://stormzhang.com/github/2016/05/25/learn-github-from-zero1/)
2. [廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

