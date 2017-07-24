### 基本命令

- `git init`  将当前目录初始化为Git仓库
- `git add <file>`   把名称为`file`的文件添加到Git仓库
- `git commit -m "msg"`  把文件提交到仓库，`msg`为本次提交的说明。

`commit`命令一次可以提交多个文件，因此可以多次`add`不同的文件。



### 版本控制

- `git status`  可以查看仓库当前的状态
- `git diff`  可以查看修改的具体内容
  - `git diff HEAD -- <file>`  可以查看工作区和版本库里面最新版本的区别


- `git log`  查看提交记录
  - `--pretty=oneline`  使用此参数简化输出信息，每次提交记录只显示一行
- `git reset --hard HEAD^`  回退到上个版本
  - `git reset --hard <commit id>`  可以根据`commit id` 来回退版本，版本号不需要写全，Git会根据前几位自动去找
- `git reflog`  查看每一次命令
- `git checkout -- <file>`  可以丢弃工作区的修改，用版本库里的版本替换工作区的版本
- `git reset HEAD <file>`  可以把暂存区的修改回退到工作区。`HEAD`表示最新的版本
- `git rm <file>`  用于删除一个文件

Git中用`HEAD`表示当前版本，上一版本就是`HEAD^` ，上上版本就是`HEAD^^` 。往上一百个版本可以写成`HEAD~100` 



[工作区和暂存区](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013745374151782eb658c5a5ca454eaa451661275886c6000) 



### 远程仓库

- GitHub
  - `git remote add origin <git url>`  在本地库目录下执行，可以将本地仓库与Github中对应仓库相关联。`origin`为远程库的名字，是Git的默认叫法。
  - `git push -u origin master`  把本地库的内容推送到远程，`git push`  将 当前分支`master` 推送到远程。使用`-u` 参数会把本地的`master`分支与远程的`master`分支关联起来。
  - `git clone <git url>` 克隆仓库到本地。



### 分支

- `git checkout -b dev` 创建并切换到`dev`分支
  - 该命令相当于两条命令`git branch dev` 、`git checkout dev` 
- `git brach`  查看当前分支，该命令会列出所有分支，当前分支前面会标一个`*`号。
- `git merge dev` 合并指定分支`dev`到当前分支。
  - 当合并冲突时，手动处理冲突文件后再次`add` 、`commit` 
  - 合并分支时，如果没有冲突，Git会使用`Fast forward`模式。这种模式下，删除分支后，会丢掉分支信息。`git merge --no-ff dev`  将`dev`分支合并到当前分支，禁用`Fast forward`方式。
- `git branch -d dev`  删除`dev`分支。
- `git log --graph`  可以看到分支合并图
  - `git log --graph --pretty=oneline --abbrev-commit`  简化分支合并图信息
- `git stash`  把当前工作现场"储存"起来，后面恢复后继续工作。
- `git stash list`  查看工作现场。
- `git stash apply`  恢复stash内容，但是stash的内容并不删除。
  - `git stash apply stash@{0}`  恢复指定的stash。
- `git stash drop`  删除stash的内容。
- `git stash pop`   恢复并删除stash内容。
  - `git brach -D feature-vulcan`  强行删除`feature-vulcan`分支。分支未合并，删除后会丢失修改。

### 多人协作

- `git remote`  查看远程库的信息
  - `git remote -v`  显示详细信息
- `git push origin master`  把`master`分支上的所有本地提交推送到远程库。
- `git pull`  获取远程库最新的提交。
- `git branch --set-upstream dev origin/dev`  设置`dev`与`origin/dev` 的链接

多人协作，提交到分支到远程库有冲突时，先pull最新提交到本地，然后手动处理冲突后再次提交。如果`git pull` 提示"no tracking information"，则说明本地分支和远程分支未建立连接。使用`git branch --set-upstream <branch-name> origin/<branch-name>` 建立本地分支与远程分支的关联。



### 标签

- `git tag <name>`  为当前分支打一个新标签
  - `git tag`  查看所有标签
  - `git tag <name> <commit id>`  给对应操作记录打标签
  - `git tag -a <name> -m <msg>`  创建有说明的标签
  - `git tag -s <name>` 用私钥签名一个标签。签名使用PGP签名，必须首先安装gpg(GnuPG)。
  - `git tag -d <name>`  删除标签。
- `git show <name>`  查看标签信息
- `git push origin <name>`  推送标签到远程
  - `git push origin --tags`  推送全部尚未推送到远程的本地标签。
  - 删除远程标签，先从本地删除`git tag -d <name>` ，然后从远程删除`git push origin :refs/tags/<name>` 

### 其他

- `git config --global color.ui true`  让Git显示颜色。
- 配置忽略文件`.gitignore` ，可以参考Github中的[gitignore](https://github.com/github/gitignore)。将`.gitignore`提交到Git就完成了。在Win中，在资源管理器里新建一个`.gitignore`文件，系统会提示你输入文件名，可以再文本编辑器中编辑，然后保存为`.gitignore`即可。
- `git add -f <file>`  强制添加到Git
- `git check-ignore -v <file>` 检查`.ignore`文件。 
- 配置别名
  - `git config --global alias.st status`  用`st` 代表`status`。 
  - `git config --global alias.unstage 'reset HEAD'` 简化撤销语句。`git unstage <file>` 
  - `git config --global alias.last 'log -1'`   配置`git last` ，让其显示最后一次提交信息。
  - `--global`是全局参数，针对当前用户起作用，如果不加就只针对当前仓库起作用。每个仓库的配置文件都放在`.git/config`文件中。当前用户的Git配置文件放在用户主目录下的隐藏文件`.gitconfig`中。

#### Issue

- [`Detached HEAD`状态](http://www.jianshu.com/p/ae4857d2f868)



### Thanks

- [廖雪峰Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)