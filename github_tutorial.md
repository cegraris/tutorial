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
