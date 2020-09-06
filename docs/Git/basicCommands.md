# 基本命令

## git add
> 作用：将改动添加到暂存区
```
# 常用命令
1. git add readme.txt：添加某一个文件到暂存区
2. git add --all：添加所有改动到暂存区
```

## git branch
> 作用：查看当前所在分支

## git checkout
> 作用：在分支间切换
```
# 常用命令
1. git checkout dev
2. git checkout master
```

## git checkout -b dev
> 作用：创建dev分支并切换到dev分支，相当于（git branch dev，git checkout dev 这两条命令）

## git checkout -- filename
> 作用：当你改乱了工作区某个文件内容，想直接丢弃工作区的修改（其实是用版本库里的替换工作区的）如果你还将其添加到了暂存区，那不好意思，该条命令不起作用。

## git clone 
> 作用：克隆仓库
```
# 常用命令
1. git clone https://...
2. git clone --recurse-submodules https://...
3. git clone -b branch https://...

# https://github.com 和 git@github.com 的区别
# 前者是 https 格式，后者是 ssh 格式。
# 用 https 格式的时候，每当要 git pull 还是 git push 都会要求你输入用户名密码。
# 而用 ssh 格式就不需要，因为有公用私用密码机制。
**解决：**
git remote remove origin
git remote add origin git@github.com:USERNAME/REPOSITORY.git
**还要重新追踪分支：**
git branch --set-upstream-to=origin/master master
git branch --set-upstream-to=origin/dev dev
```

## git commit
> 作用：将暂存区的内容提交到分支
```
# 常用命令
1. git commit -m 'describe'：将暂存区的内容提交到分支并对该改动进行描述。
```

## git diff
> 作用：查看修改内容
```
# 常用命令：
1. git diff filename
```

## git init
> 作用：初始化一个仓库

## git log
> 作用：查看提交日志
```
# 常用命令
1. git log --pretty=oneline --abbrev-commit --graph：查看提交日志，显示方式一行、简略信息、图形结构
```

## git merge
> 作用：合并分支。
```
# 常用命令
1. git merge dev：首先你要处在某一分支，比如你要将dev合并到master，你首先要呆在master分支上，然后执行上述命令。
2. git merge --no-ff dev：<font color=red >--no-ff</font> 的意思就是不使用 <font color=red>fast forward</font> 合并。普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而 <font color=red>fast forward</font> 模式合并就看不出曾经做过合并。
```

## git reflog
> 作用：当你回退到以前的版本后，git log 中就没有你当前版本后的版本信息，此时你又想返回未来，就需要未来的版本号，你可以查看命令历史，并确定回到未来的哪个版本

## git reset
> 作用：版本回退
```
# 常用命令
1. git reset --hard HEAD：回退到上一个版本
2. git reset --hard 版本号：回退到指定版本
```

## git reset HEAD filename
> 作用：当你不但改乱了工作区某个文件的内容，还添加到了暂存区，可以用此条命令丢弃暂存区中的修改。然后再用上 git checkout -- filename 将工作区的修改丢弃。

## git rm filename
> 作用：删除一个文件

## git status
> 作用：随时掌握工作区的状态
