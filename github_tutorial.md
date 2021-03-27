# 安装设置
安装方法可以google
安装完后设立全局名称和邮箱，用以后面commit
```bash
git config --global user.name "XXX"
git config --global user.email "XXX@XXX"
```
# 初始化github库
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