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
快照
```
git add XXX.xxx
git add YYY.yyy
git commit -m "xxxxx" -m "xxxxx"
```
也可以直接用批量快照
```
git add .
git commit -m "xxxxx" -m "xxxxx"
```

# 查看历史快照
```
git log
```
简短单行说明
```
git log --pretty=oneline
```
产看完整日志
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
checkout其实使用版本苦力的版本替换工作区的版本

# 远程仓库GitHub
在GitHub 建一个新的repo，然后将其clone到本地，或将一个本地仓库与之关联 <br/>
clone到本地的方法：<br/>
```
git clone git@github.com:cegraris/tutorial.git
```
本地仓库与之关联的方法： <br/>
```
git remote add origin git@github.com:cegraris/tutorial.git
```
origin是远程库的默认习惯名字，后面一串是GitHub提供的SSH地址<br/>
绑定后就可以将本地库的内容推送到远程了
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
当我们创建了一个新的分支（dev）时：<br/>
```
git checkout -b dev
```
等价于
```
git brach dev
git checkout dev
```
HEAD -> dev -> 最新的commit <br/>
此后对工作区的修改和提交就是在dev分支上了，master的指针不会再改变<br/>
可以用以下指令查看当前分支
```
git branch
```
等dev工作完成了，可以把master指向dev指向的那个commit，那就完成了合并<br/>
合并完成后也可以删除dev分支，即将dev指针删除<br/>