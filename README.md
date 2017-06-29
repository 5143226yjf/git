# git命令大全

## git常用命令1

#### 1.查看、添加、提交、删除、找回，重置修改文件

git help <command> # 显示command的help

git show # 显示某次提交的内容 git show $id

git co -- <file> # 抛弃工作区修改

git co . # 抛弃工作区修改

git add <file> # 将工作文件修改提交到本地暂存区

git add . # 将所有修改过的工作文件提交暂存区

git rm <file> # 从版本库中删除文件

git rm <file> --cached # 从版本库中删除文件，但不删除文件

git reset <file> # 从暂存区恢复到工作文件

git reset -- . # 从暂存区恢复到工作文件

git reset --hard # 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改

git ci <file> git ci . git ci -a # 将git add, git rm和git ci等操作都合并在一起做　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　git ci -am "some comments"

git ci --amend # 修改最后一次提交记录

git revert <$id> # 恢复某次提交的状态，恢复动作本身也创建次提交对象

git revert HEAD # 恢复最后一次提交的状态

#### 2.查看文件diff

git diff <file> # 比较当前文件和暂存区文件差异 git diff

git diff <id1><id1><id2> # 比较两次提交之间的差异

git diff <branch1>..<branch2> # 在两个分支之间比较

git diff --staged # 比较暂存区和版本库差异

git diff --cached # 比较暂存区和版本库差异

git diff --stat # 仅仅比较统计信息

#### 3.查看提交记录

git log git log <file> # 查看该文件每次提交记录

git log -p <file> # 查看每次详细修改内容的diff

git log -p -2 # 查看最近两次详细修改内容的diff

git log --stat #查看提交统计信息

tig

Mac上可以使用tig代替diff和log，brew install tig

Git 本地分支管理

#### 4.查看、切换、创建和删除分支

git br -r # 查看远程分支

git br <new_branch> # 创建新的分支

git br -v # 查看各个分支最后提交信息

git br --merged # 查看已经被合并到当前分支的分支

git br --no-merged # 查看尚未被合并到当前分支的分支

git co <branch> # 切换到某个分支

git co -b <new_branch> # 创建新的分支，并且切换过去

git co -b <new_branch> <branch> # 基于branch创建新的new_branch

git co $id # 把某次历史提交记录checkout出来，但无分支信息，切换到其他分支会自动删除

git co $id -b <new_branch> # 把某次历史提交记录checkout出来，创建成一个分支

git br -d <branch> # 删除某个分支

git br -D <branch> # 强制删除某个分支 (未被合并的分支被删除的时候需要强制)

#### 5. 分支合并和rebase

git merge <branch> # 将branch分支合并到当前分支

git merge origin/master --no-ff # 不要Fast-Foward合并，这样可以生成merge提交

git rebase master <branch> # 将master rebase到branch，相当于： git co <branch> && git rebase master && git co master && git merge <branch>

 Git补丁管理(方便在多台机器上开发同步时用)

git diff > ../sync.patch # 生成补丁

git apply ../sync.patch # 打补丁

git apply --check ../sync.patch #测试补丁能否成功

#### 6. Git暂存管理

git stash # 暂存

git stash list # 列所有stash

git stash apply # 恢复暂存的内容

git stash drop # 删除暂存区

#### 7.Git远程分支管理

git pull # 抓取远程仓库所有分支更新并合并到本地

git pull --no-ff # 抓取远程仓库所有分支更新并合并到本地，不要快进合并

git fetch origin # 抓取远程仓库更新

git merge origin/master # 将远程主分支合并到本地当前分支

git co --track origin/branch # 跟踪某个远程分支创建相应的本地分支

git co -b <local_branch> origin/<remote_branch> # 基于远程分支创建本地分支，功能同上

git push # push所有分支

git push origin master # 将本地主分支推到远程主分支

git push -u origin master # 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)

git push origin <local_branch> # 创建远程分支， origin是远程仓库名

git push origin <local_branch>:<remote_branch> # 创建远程分支

git push origin :<remote_branch> #先删除本地分支(git br -d <branch>)，然后再push删除远程分支

#### 9.Git远程仓库管理

##### GitHub
git remote -v # 查看远程服务器地址和仓库名称

git remote show origin # 查看远程服务器仓库状态

git remote add origin git@ github:robbin/robbin_site.git # 添加远程仓库地址

git remote set-url origin git@ github.com:robbin/robbin_site.git # 设置远程仓库地址(用于修改远程仓库地址) git remote rm <repository> # 删除远程仓库

##### 创建远程仓库

git clone --bare robbin_site robbin_site.git # 用带版本的项目创建纯版本仓库

scp -r my_project.git git@ git.csdn.net:~ # 将纯仓库上传到服务器上

mkdir robbin_site.git && cd robbin_site.git && git --bare init # 在服务器创建纯仓库

git remote add origin git@ github.com:robbin/robbin_site.git # 设置远程仓库地址

git push -u origin master # 客户端首次提交

git push -u origin develop # 首次将本地develop分支提交到远程develop分支，并且track

git remote set-head origin master # 设置远程仓库的HEAD指向master分支

##### 也可以命令设置跟踪远程库和本地库

git branch --set-upstream master origin/master

git branch --set-upstream develop origin/develop

## git常用命令2
```bash
  克隆项目：git clone ...
  创建自己分支  git checkout -b branchName
  切换分支 git checkout branchName
  查看本地分支状态 git branch
  查看当前状态 git status
  删除本地分支 git branch -d branchName  (此时不能处在branchName分支上)
  若无法删除, 在确保代码已经和合并此分支没有用的情况可以强制删除 git branch -D branchName
  查看远程分支 git branch -r
  删除远程分支 git push origin :branchName
  从远程分支拉取对应的分支（例如risk分支）到本地一个新的分支上（例如risk2）  git checkout -b risk2 origin risk
  如果失败，可以这样 git fetch origin risk:risk2 但是需要手动切换  git checkout risk2

  在合作开发时，应该每次写代码时都先到dev分支   git checkout dev
  从远程更新最新代码  git pull
  从dev分支出发，创建并切换到一个新的分支，如test      git checkout -b test
  从此在这个分支上进行开发，开发结束，提交  git add text.jx(提交单个文件)    
                                                                提交全部内容  git add -A
  然后commit一下   git commit -a -m"这里是提交信息"
  最好提交之前先 git pull一下，养成习惯。但是如果远程分支上都没有这个分支的话，也啥都没有
  最后提交   git push (如果远程有这个分支)  git push origin test (远程没有这个分支，创建远程test分支并提交)
  ```

--------------------------------下面这个超级重要------------------------
目前知道两种情况要用
1. 当你完成一个任务发现忘记重新创建一个分支，而是在一个很旧的分支上写的时候，先将当前修改保存到缓存中 git stash
    切换到dev分支 
     ```bash
     git checkout dev 
     ```
    拉取最新代码
     ```bash 
    git pull
    ``` 
    创建新的分支并切换    git checkout -b test
    将缓存中的代码取出并放在当前分支中   git stash pop
    可以多次进行缓存，当想要回复时先查看当前缓存中的代码  git stash list
    然后指定想要恢复的那一个   git stash apply stash@{0}
当正在完成当前任务，突然需要修复一个bug时，做法与上述类似，先将正在完成的代码放在缓存中，等bug修复结束再取出继续操作

当修改了东西git stash的时候出现 needs merge的情况，pull不了，stash不了，解决办法使用
   ```bash
     git reset --mixed
     git merge又想撤销，撤销revert的方法
     git revert HEAD                  撤销前一次 commit
     git revert HEAD^               撤销前前一次 commit
     git revert commit （比如：fa042ce57ebbe5bb9c8db709f719cec2c58ee7ff）撤销指定的版本，撤销也会作为一次提交进行保存。
  ```

## git常用命令3
```bash
             git add .   —将代码添加到暂存区
             git commit -am “注释”    —将代码提交到本地仓库
             git pull        — 更新所有代码
             git push      —将当前分支的代码放到远端对应服务器
             git stash     —方便临时处理bug时随时切换分支而不丢失修改
             git stash pop — 从Git栈中读取最近一次保存的内容，恢复工作区的相关内容。  　　　　　　　　　　  
                             由于可能存在多个Stash的内容，所以用栈来管理，pop会从最近的一个stash中读取内容并恢复。
  　　        git stash list — 显示Git栈内的所有备份，可以利用这个列表来决定从那个地方恢复。
             git stash clear — 清空Git栈。此时使用gitg等图形化工具会发现，原来stash的哪些节点都消失了。
  　　　      git diff  —  查看本地修改内容 （一般用于git add .前检查代码）
             git branch newBranch  —创建一个新的分支
             git checkout -b newBranch  —创建并切换到新创建的分支
             git checkout master — 切换回主分支
             git branch -d  newBranch   — 删除本地的新建分支
             git branch -r        — 查看远端所有分支
    　　　    git branch -a        — 查看所有分支（本地+远程分支）
             git push origin : jim   — 删除远端 新建的分支
             git status        —查看当前状态
             git merge       — 将分支合并到本地
             git push origin jim — 将本地分支推送到远程
             git  push - - set-upstream origin jim   — 将新建的分支与远端相关联
             git checkout —filename   — 回滚改动错误的代码
             git log    — 查看日志
             git reset  --hard 版本号    — 本地回滚错误的代码
             git rebase — 慎用！若当成一种在推送之前清理提交历史的手段，而且仅仅衍合那些尚未公开的提交对（如果衍合那些已经公开的提交对象，并且已经有人基于这些提交对象开展了后续开发工作的话，就会出现麻烦）。
 ```