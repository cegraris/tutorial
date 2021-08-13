# git安装设置
安装方法可以google
安装完后设立全局名称和邮箱，用以后面commit
```bash
git config --global user.name "XXX"
git config --global user.email "XXX@XXX"
```

# 建立SSH Key
```
ssh-keygen -t rsa -C "XXX@xxx"
```

# 初始化git库
在需要建立git库的文件夹目录下
```bash
git init
```
# 保存版本快照
查看版本控制情况
```bash
git status
```
查看文件变化情况
```bash
git diff XXX.xxx
```
添加到暂存区
```bash
git add XXX.xxx
git add YYY.yyy
git add .
```
从暂存区删除
```bash
git rm --cachted XXX.xxx
```
提交到本地库
```bash
git commit -m "xxxxx" XXX.xxx
git commit -m "xxxxx"
```


# 查看历史快照
产看完整日志
```
git log
```
简短单行说明
```
git log --pretty=oneline
```
查看简短日志
```
git reflog
```

# 退回历史版本
```
git reset --hard HEAD^
```
HEAD^ -> 回退上一版本 </br>
HEAD^ -> 回退上上版本 </br>
HEAD~100 -> 回退前一百个版本 </br>
d404070e3a76c058066cb62c30b3bcfdaf9095d9 -> 回退到该版本 </br>
d4040 -> 回退到该版本（简写也是可以的） </br>

# 撤销修改
放弃工作区的修改，将文档返回到最近一次git commit或git add时的状态 <br/>
当add到暂存区，然后修改（没commit），就会撤回到add的时候的状态<br/>
当commit过了，然后修改（没有add)，就会撤回到commit时的状态<br/>
```
git checkout -- <file>
```
add后，可以用reset把暂存区的修改撤销掉，重新放回工作区
```
git reset HEAD <file>
```

# 删除文件
文件管理器中将文件删了<br/>
当这个文件时确实要删除的:<br/>
```
git rm <file>
git commit -m "xxxxx"
```
当这个文件是误删，可以通过以下指令恢复文件:<br/>
```
git checkout -- <file>
```
checkout其实使用版本库里的版本替换工作区的版本

# 远程仓库GitHub
在GitHub 建一个新的repo，然后将其clone到本地，或将一个本地仓库与之关联 <br/>
clone到本地的方法：<br/>
```
git clone git@github.com:cegraris/tutorial.git
```
创建远程库别名： <br/>
```
git remote add origin git@github.com:cegraris/tutorial.git
```
origin是远程库的默认习惯名字，后面一串是GitHub提供的SSH地址<br/>
可以用下列指令查看远程仓库信息（简单/详细）<br/>
```
git remote
git remote -v
```
绑定后就可以将本地库的内容推送到远程的某个分支了
```
git push -u origin master
```
-u参数可以将远程和本地库的master分支绑定，以后就可以直接用git push origin master了<br/>

若要删除远程和本地库的绑定可以先查看远程库信息
```
git remote -v
```
然后根据名字（比如origin）删除
```
git remote rm origin
```

# 分支管理
一般情况下：<br/>
HEAD -> master -> 最新的commit <br/>
查看分支
```bash
git branch -v
```
当我们创建了一个新的分支（dev）时：<br/>
```bash
git checkout -b dev
```
等价于
```bash
git brach dev
git checkout dev
```
或
```
git switch -c dev
```
HEAD -> dev -> 最新的commit <br/>
此后对工作区的修改和提交就是在dev分支上了，master的指针不会再改变<br/>
可以用以下指令查看当前分支
```
git branch
```
等dev工作完成了，就可以进行合并<br/>
```
git checkout master
git merge dev
```
或
```
git switch master
git merge dev
```
merge指令可将制定分支合并到当前分支<br/>
merge会默认尽量采用Fast forward模式，即把master指向dev指向的那个commit，但这种模式下，删除分支后会丢掉分支信息。<br/>
当冲突发生时会merge失败，然后需要手动修改文件，然后再add,commit修改后的文件<br/>
在非冲突情况下也可以禁用Fast forward来强制在merge时产生一个新commit来进行合并<br/>
```
git merge --no-ff -m "merge with no-ff" dev
```
合并完成后也可以删除dev分支，即将dev指针删除<br/>
```
git branch -d dev
```
用以下指令可以查看分支的合并图
```
git log --graph
```
一般情况下小组成员各自开一个分支（一般在本地维护），这几个分支共同维护一个dev分支（远程），然后偶尔将dev分支合并到master（远程）上，成为比较正式的版本

## bug分支
将当前工作区存起来,这种情况下git status会显示是干净的
```
git stash
```
然后切换到要修复bug的分支A，建立并跳到修复bug的分支B，修复，add，commit，跳回要修复bug的分支A，merge B<br/>
bug修复好，现在要恢复之前的工作区<br/>
查看暂存工作区
```
git stash list
```
恢复并删除stash内容
```
git stash apply
git stash drop
```
等价于
```
git stash pop
```
也可以恢复制定的stash
```
git stash apply stash@{0}
```
若想要当前分支上也修复以下刚刚修复过的bug，则可以使用以下指令仅将bug修复commit中修改的部分复制过来
```
git cherry-pick 4c805e2
```

## feature分支
一般用来创建一个新的功能
若该功能最终弃用，没有合并，则可以通过以下指令强行删除
```
git branch -D <name>
```

## 多人协作可能产生的冲突
先试图用push推送自己的修改
```
git push origin <branch-name>
```
如果推送失败，则因远程分支比你本地的更新，需要先用pull试图合并
```
git pull
```
若提示no tracking information,则说明本地分支和远程分支的链接关系没有建立，使用如下指令解决问题
```
git branch --set-upstream-to <branch-name> origin/<branch-name>
```
如果合并有冲突，则解决冲突，并在本地提交<br/>
没有冲突或者解决掉冲突后，再用push推送就能成功<br/>

## Rebase
可以将提交历史转化成一条直线
```
git rebase
```

# 标签
可以为commit打上标签,切换到branch，然后用如下命令，会自动给最新的commit打上标签
```
git tag v1.0
```
也可以为指定的commit打标签
```
git tag v0.9 f42c633
```
或采用带说明标签
```
git tag -a v0.1 -m "version 0.1 released" 1094adb
```
用如下指令查看标签<br/>
按字母顺序排列：
```
git tag
```
查看标签信息
```
git show <tagname>
```

推送某个标签到远程
```
git push origin <tagname>
```
推送全部尚未推送到远程的本地标签
```
git push origin --tags
```
删除本地标签
```
git tag -d <tagname>
```
删除远程标签，先要删除本地，然后执行如下指令
```
git push origin :refs/tags/<tagname>
```

# 忽略特殊文件
有些文件必须在工作目录中但不想提交，则可以在Git工作区的根目录下创建.gitignore文件，然后把想要忽略的文件填进去，Git会自动忽略这些文件，不需要从头写.gitignore文件。可以在https://github.com/github.gitignore 查看预备的配置文件模板。<br/>
强制添加被忽略的文件到git
```
git add -f <file>
```