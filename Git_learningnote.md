# Git使用笔记 #

## 一. Git和SVN的区别 ##

|   |类型|描述|
| -| - | - |
Git|分布式版本控制系统|本地有镜像,无网络时也可以提交到本地镜像,等到有网络时再push到服务器
SVN|集中式版本控制系统|无网络不可以提交, 和 Git 的主要区别是历史版本维护的位置

## 二. 安装Git ##

本文的git安装在ubuntu系统下

## 三. 创建版本库 ##

**版本库又名仓库，英文名repository，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原"。**

### 1.相关命令 ###

```C

(所有命令都在 Git Bash 中运行)
$ git                           查看 git 的相关命令 (git --help)
$ git --version                 查看 git 的版本
$ git config                    查看 git config 的相关命令
$ git pull origin develop       从远程(origin) 的 develop 分支拉取代码
```

### 2.初始化本地仓库 ###

```c

$ mkdir learn_git
$ cd learn_git
$ pwd

# cd: change directory 改变目录
# mkdir  创建目录
# pwd    用于显示当前目录
```

```c

# 不想要 git 管理跟踪的文件,可以在仓库根目录添加 .gitignore 文件,在里面写对应的规则
$ git init              把当前目录初始化为 git 仓库
$ ls -ah                查看当前目录下的文件,包含隐藏文件 (不带 -ah 看不了隐藏文件)
```

### 3.添加文件到仓库 ###

随便写一个文件放到 ***git_learing*** 目录下，因为这是一个Git仓库，放到其他地方Git找不到这个文件.
这里我们写了一个 ***readme.txt*** 文件，把一个文件放到Git仓库需要两步：

第一步：用命令 git add 告诉Git，把文件添到仓库  

```C

git add readme.txt
```

第二步，用命令git commit告诉Git，把文件提交到仓库：

```C

$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
1 file changed, 2 insertions(+)
create mode 100644 readme.txt
```

**注意**:

1. -m 后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的,这样你就能从历史记录里方便地找到改动记录。

2. git commit命令执行成功后会告诉你， ***1 file changed***  1个文件被改动（我们新添加的readme.txt文件）； ***2 insertions*** 插入了两行内容（readme.txt有两行内容）。

3. 为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：

```C
git add file1.txt
git add file2.txt file3.txt
git commit -m "add 3 files."
```

### 4.查看仓库当前状态(项目是否有修改，添加，未追踪文件等) ###

```C
git status 
```

### 5.查看修改内容，查看文件不同 ###

```C
$ git diff 
$ git diff <file>                
$ git diff --cached
$ git diff HEAD -- <file>
# git diff 查看工作区(work dict)和暂存区(stage)的区别
# git diff --cached 查看暂存区(stage)和分支(master)的区别
# git diff HEAD -- <file> 查看工作区和版本库里面最新版本的区别
如: git diff readme.txt  表示查看 readme.txt 修改了什么,有什么不同
```

### 6.查看提交日志 ###

每修改一次算一个版本，如何查看版本？用日志命令！

```C
$ git log
$ git log --oneline     #美化输出信息,每个记录显示为一行,显示 commit_id 前几位数
$ git log --pretty=oneline     #美化输出信息,每个记录显示为一行,显示完整的 commit_id
$ git log --graph --pretty=format:'%h -%d %s (%cr)' --abbrev-commit --
$ git log --graph --pretty=oneline --abbrev-commit

# 显示从最近到最远的提交日志
# 日志输出一大串类似 3628164...882e1e0 的是commit_id (版本号),和 SVN 不一样，Git 的commit_id 不是 1，2，3…… 递增的数字，而是一个 SHA1 计算出来的一个非常大的数字，用十六进制表示, 因为 Git 是分布式的版本控制系统，当多人在同一个版本库里工作，如果大家都用 1，2，3……作为版本号，那肯定就冲突了
# 最后一个会打印出提交的时间等, (HEAD -> master)指向的是当前的版本
# 退出查看 log 日志,输入字母 q (英文状态)
```

### 7.版本回退 ###

为什么要版本回退？
答：当文件修改到一定程度出现问题的时候，比如把文件改乱了或者误删了文件，就可以选择一个最近保存过的版本回退。

```C

$ git reset --hard HEAD^
$ git reset --hard <commit_id>

# HEAD    表示当前版本，也就是最新的提交
# HEAD^   上一个版本
# HEAD^^  上上一个版本
# HEAD~100   往上100个版本

# 回退到 commit_id 对应的那个版本,commit_id 为版本号,只需要前几位就行
```

此时如果使用 git log 查询日志时，会发现没有最近一次的日志显示，如果想前进到回退前的版本，找到以前未来版本的提交日志显示的版本号，用以下命令回去：

```C
git reset --hard 1094a （1094a是未来版本的版本号前几位）

```

查看某一文件的内容命令

```C
cat <file_name>
```



