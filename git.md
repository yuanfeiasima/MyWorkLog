[try git](https://try.github.io)
```bash
git 设置log可视化
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%c
r) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

如果没有add 撤销直接用`git checkout -- file。`

如果add但还没有commit，（还添加到了暂存区时），想丢弃修改，分两步，第一步用命令`git reset HEAD file，就回到了场景1，第二步按场景1操作。`

已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)一节，不过前提是没有推送到远程库。

```
不自动转换文件格式 git config --global core.autocrlf false
```