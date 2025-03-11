

# 目录
- [目录](#目录)
- [Git入门](#git入门)
  - [git和github基本操作](#git和github基本操作)
    - [安装git（for mac）](#安装gitfor-mac)
    - [上传文件到github](#上传文件到github)
  - [独自使用git的基本操作](#独自使用git的基本操作)
    - [找到所有的操作记录](#找到所有的操作记录)
    - [配置git用户名和邮箱](#配置git用户名和邮箱)
    - [修改项目中的文件](#修改项目中的文件)
    - [删除文件](#删除文件)
    - [文件重命名](#文件重命名)
    - [移动文件到其他文件夹](#移动文件到其他文件夹)
  - [独自使用git的常见问题及解决方法](#独自使用git的常见问题及解决方法)
    - [文件有变化时如何查看前后变化](#文件有变化时如何查看前后变化)
    - [操作失误的情况下如何一键还原](#操作失误的情况下如何一键还原)
    - [不再追踪时如何实现撤销追踪操作](#不再追踪时如何实现撤销追踪操作)
    - [回到上一个版本或指定版本](#回到上一个版本或指定版本)
    - [指定文件版本回退](#指定文件版本回退)
    - [修改内容后推送到远程仓库](#修改内容后推送到远程仓库)
    - [创建版本标签以及标签管理](#创建版本标签以及标签管理)
    - [创建、切换、删除远程分支](#创建切换删除远程分支)
    - [合并分支](#合并分支)
    - [合并分支时的冲突](#合并分支时的冲突)
  - [git多人分支集成协作时的常见场景](#git多人分支集成协作时的常见场景)
    - [不同人想要查看版本路线如何操作](#不同人想要查看版本路线如何操作)
    - [不同的人删除分支](#不同的人删除分支)
    - [不同人修改了不同文件该如何处理](#不同人修改了不同文件该如何处理)
    - [不同人修改相同文件](#不同人修改相同文件)
  - [github拓展](#github拓展)
  - [总结](#总结)


# Git入门
[🔝](#目录)

---
## git和github基本操作

### 安装git（for mac）

在终端输入`git --version`检查是否安装了git，如果没有安装git进入[git官网](https://git-scm.com/?hl=zh-cn)下载对应操作系统（Mac、Linux、Windows等）的git。
![alt text](<截屏2025-03-08 22.13.53.png>)

mac系统推荐使用homebrew进行安装，命令为：
`brew install git`

### 上传文件到github

如果有不需要上传到仓库中的文件或文件夹，可以添加到`.gitignore`文件中。如
```
foldname
.DS_Store
file.txt
```

接下来在待上传的文件目录下执行以下命令：
`git init ` # 初始化git仓库
`git add .` # 添加所有文件到暂存区
`git commit -m "第一次上传"` # 上传描述
`git remote add origin https://github.com/Damon-Chang/Embodied-AI.git` # 添加远程仓库地址
`git push -u origin main` # 上传到远程仓库

> [!NOTE]
> 这里出现了报错：
> `错误：源引用规格 main 没有匹配`
> `错误：无法推送一些引用到 'https://github.com/Damon-Chang/Embodied-AI.git'` 
> 排查发现是本地分支（master）和远程分支（main）不一致，于是先更改分支名称：
> `git branch -M main` 
> 再执行
> `git push -u origin main` 
> 成功上传！
> PS.很有可能遇到连不上github的问题，此时需要科学上网了！

终端出现` * [new branch]      main -> main`表示上传成功。

---
## 独自使用git的基本操作
[🔝](#git入门)

### 找到所有的操作记录

`git status` # 查看当前工作目录状态
终端显示为：
```
位于分支 main
您的分支与上游分支 'origin/main' 一致。

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）
        gitignore

提交为空，但是存在尚未跟踪的文件（使用 "git add" 建立跟踪）
```
表示并未进行改动，如果对文件内的文件进行改动，再执行`git status`查看状态，会得到：
```
位于分支 main
您的分支与上游分支 'origin/main' 一致。

尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     "papers/\345\205\267\350\272\253\344\272\272\345\267\245\346\231\272\350\203\275/\345\205\267\350\272\253\344\272\272\345\267\245\346\231\272\350\203\275\347\273\274\350\277\260.md"

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）
        gitignore

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```
接下来如果要保存着这一改动，执行：
`git add .`
`git commit -m "修改:filename`

提交之后，就可以在github上查看到修改了。
```
[main be0bda5] 测试改动
 Committer: 常宇航 <damonchang@changyuhangdeMacBook-Pro.local>
您的姓名和邮件地址基于登录名和主机名进行了自动设置。请检查它们正确
与否。您可以对其进行设置以免再出现本提示信息：

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

设置完毕后，您可以用下面的命令来修正本次提交所使用的用户身份：

    git commit --amend --reset-author

 2 files changed, 64 insertions(+), 3 deletions(-)
```

此外还可以通过`git log`命令来查看**全部**提交记录，例如：
`git log`
在终端中得到：
```
commit be0bda53c823ec635290cba8dc7f8a6c3ddc3a2f (HEAD -> main)
Author: 常宇航 <damonchang@changyuhangdeMacBook-Pro.local>
Date:   Sun Mar 9 10:35:12 2025 +0800

    测试改动

commit bdb6aeadf000b0413d294360c9f977d4c36d92c1 (origin/main)
Author: 常宇航 <damonchang@changyuhangdeMacBook-Pro.local>
Date:   Sun Mar 9 09:56:53 2025 +0800

    第一次上传
```

可以使用`git log --oneline`来简化输出，只显示提交记录的摘要信息，包括提交哈希值和提交信息。

命令`git log -- author=='常宇航'`表示只查看一个用户的修改记录。

### 配置git用户名和邮箱

在终端中执行命令
`git config --global user.name "DamonChang"` # 用户名
`git config --global user.email "18804012206@163.com"` # 邮箱
检查配置是否成功，执行
`git config --global --list`
显示为
```
http.sslverify=false
user.name=DamonChang
user.email=18804012206@163.com
```
表示配置用户名和邮箱成功。配置成功后，这一信息将用于查看代码提交记录时，显示的作者信息。

### 修改项目中的文件

如果添加新文件如`test.py`，执行
`git add test.py`
再执行`git status`查看状态得到
```
位于分支 main
您的分支领先 'origin/main' 共 1 个提交。
  （使用 "git push" 来发布您的本地提交）

要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        新文件：   test.py
```
表示新文件已添加到**暂存区**。保存更改，执行`git commit -m "新增文件"`，输出
```
[main 8a9188c] 新增文件
 1 file changed, 8 insertions(+)
 create mode 100644 test.py
```
再执行`git log`查看历史信息得到
```
commit 8a9188c583d685ecedead90c578d2ed8f5ab44e1 (HEAD -> main)
Author: DamonChang <18804012206@163.com>
Date:   Sun Mar 9 13:10:14 2025 +0800

    新增文件

commit be0bda53c823ec635290cba8dc7f8a6c3ddc3a2f
Author: 常宇航 <damonchang@changyuhangdeMacBook-Pro.local>
Date:   Sun Mar 9 10:35:12 2025 +0800

    测试改动
```
最后使用`git push origin main`提交到github。
```
枚举对象中: 13, 完成.
对象计数中: 100% (13/13), 完成.
使用 8 个线程进行压缩
压缩对象中: 100% (8/8), 完成.
写入对象中: 100% (9/9), 1.45 KiB | 1.45 MiB/s, 完成.
总共 9（差异 4），复用 0（差异 0），包复用 0（来自  0 个包）
```

### 删除文件

1.手动删除
右键直接删除，通过`git status`查看：
```
位于分支 main
您的分支与上游分支 'origin/main' 一致。

尚未暂存以备提交的变更：
  （使用 "git add/rm <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        删除：     test.py

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```
接着执行
`git add .`
`git status`
输出
```
位于分支 main
您的分支与上游分支 'origin/main' 一致。

要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        删除：     test.py
```
表示文件已经删除，接着执行提交操作
`git commit -m "删除test.py文件"`
输出：
```
[main 8b989e4] 删除test.py文件
 1 file changed, 8 deletions(-)
 delete mode 100644 test.py
```

2. 通过命令行删除文件
再加回`test1.py`文件
`git add test1.py`
`git add test1_copy.py`
`git commit -m "添加回test1.py文件"`
通过命令行，执行
`git rm test1.py`
得到
```
rm 'test1.py'
```
再执行
`git add .`
`git commit -m "命令行删除文件"`
显示文件已经被删除的信息：
```
[main df4b168] 命令行删除文件
 1 file changed, 8 deletions(-)
 delete mode 100644 test1.py
```

### 文件重命名

1. **手动重命名**

手动重命名相当于删除原文件之后新增一个文件，因此在执行`git status`之后会显示
```
位于分支 main
您的分支领先 'origin/main' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）

尚未暂存以备提交的变更：
  （使用 "git add/rm <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     papers/.DS_Store
        删除：     test1_copy.py

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）
        test1_copy_rename.py

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```
因此接下来需要连续执行
`git add test1_copy_rename.py`
`git rm test1_copy.py`
接下来执行`git status`显示
```
位于分支 main
您的分支领先 'origin/main' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）

要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        重命名：   test1_copy.py -> test1_copy_rename.py
```
这表示已经完成重命名。最后进行提交
`git commit -m "手动重命名"`
显示
```
[main 32c75af] 手动重命名
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename test1_copy.py => test1_copy_rename.py (100%)
```
接下再次来执行`git status`查看状态，显示
```
位于分支 main
您的分支领先 'origin/main' 共 4 个提交。
  （使用 "git push" 来发布您的本地提交）

尚未暂存以备提交的变更：
```
表示已经完成重命名。这一方法较为繁琐。

2. **通过git命令重命名**

执行命令
`git mv test1_copy_rename.py test1.py`
`git status` # 查看状态
显示
```
位于分支 main
您的分支领先 'origin/main' 共 4 个提交。
  （使用 "git push" 来发布您的本地提交）

要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        重命名：   test1_copy_rename.py -> test1.py
```
直接进行提交
`git commit -m "git命令重命名"`
显示
```
[main 72b8b13] 命令行重命名文件
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename test1_copy_rename.py => test1.py (100%)
```
完成了重命名，十分简单便捷。

### 移动文件到其他文件夹

1. **移动文件**

假设要移动`test1.py`到gitest文件夹下，使用命令
`git mv test1.py gitest`
执行`git status`查看状态得到
```
位于分支 main
您的分支领先 'origin/main' 共 5 个提交。
  （使用 "git push" 来发布您的本地提交）

要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        重命名：   test1.py -> gitest/test1.py
```
最后提交
`git commit -m "move test1.py to gitest"`

1. **移动到文件夹并重命名**

仍然使用`git mv`，不过要直接指定文件名，例如将test1.py移动到gitest文件夹下，并重命名为`test3.py`:
`git mv test1.py gitest/test3.py`
执行后，通过`git status`可以查看到如下信息：
```
位于分支 main
您的分支领先 'origin/main' 共 7 个提交。
  （使用 "git push" 来发布您的本地提交）

要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        重命名：   test1.py -> gitest/test3.py
```
提交到远程仓库：
`git commit -m "重命名test1.py为gitest/test3.py"`
得到输出
```
[main 0a38849] 重命名test1.py为gitest/test3.py
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename test1.py => gitest/test3.py (100%)
```

---
## 独自使用git的常见问题及解决方法
[🔝](#git入门)

### 文件有变化时如何查看前后变化

在命令行输入
`git log --pretty=oneline gitest/test3.py`
得到如下的信息
```
0a38849ada09000566a69b2ca4063bd520177bca (HEAD -> main) 重命名test1.py为gitest/test3.py
```
前面的部分是提交id，后面是commit时提供的信息。这个id就是查看前后文件的关键。复制这个id，在命令行输入
`git show 0a38849ada09000566a69b2ca4063bd520177bca`
查看具体的改动信息，包括谁在什么时间提交的，改动了哪些内容等
```
commit 0a38849ada09000566a69b2ca4063bd520177bca (HEAD -> main)
Author: DamonChang <18804012206@163.com>
Date:   Sun Mar 9 21:29:31 2025 +0800

    重命名test1.py为gitest/test3.py

diff --git a/test1.py b/gitest/test3.py
similarity index 100%
rename from test1.py
rename to gitest/test3.py
```
此外，还能查看具体修改的内容，在命令行执行
`git log -p gitest/test3.py`
输出
```
ommit 0a38849ada09000566a69b2ca4063bd520177bca (HEAD -> main)
Author: DamonChang <18804012206@163.com>
Date:   Sun Mar 9 21:29:31 2025 +0800

    重命名test1.py为gitest/test3.py

diff --git a/gitest/test3.py b/gitest/test3.py
new file mode 100644
index 0000000..6904a13
--- /dev/null
+++ b/gitest/test3.py
@@ -0,0 +1,8 @@
+import numpy as ny
+
+def test():
```
如果文件夹内容修改了，如在`test2.py`中`hello`函数添加了一行内容，执行
`git add test2.py`
`git commit -m "修改test2.py"`
`git log -p test2.py`
输出
```
commit 059fee2df0dd1ed8eb9910a8808ef8099b086b2c (HEAD -> main)
Author: DamonChang <18804012206@163.com>
Date:   Sun Mar 9 21:50:06 2025 +0800

    修改test2.py

diff --git a/test2.py b/test2.py
index ef8947a..3357130 100644
--- a/test2.py
+++ b/test2.py
@@ -1,6 +1,7 @@
 
 def hello():
     print("hello world")
+    print("测试改动")
```
此时所做的改动全部展示。

### 操作失误的情况下如何一键还原

例如，在编辑`test2.py`时，不小心写错了一行代码，此时可以查看区别：
`git diff`
看到`test2.py`有改动
```
diff --git a/papers/.DS_Store b/papers/.DS_Store
index b1b0260..77520cf 100644
Binary files a/papers/.DS_Store and b/papers/.DS_Store differ
diff --git a/test2.py b/test2.py
index 3357130..0a582a4 100644
--- a/test2.py
+++ b/test2.py
@@ -2,6 +2,7 @@
 def hello():
     print("hello world")
     print("测试改动")
+    我是错误
 
 if '__main__' == __name__:
     hello()
```
通过找到文件修改回去再提交是一种方法，不过未免有些麻烦和笨拙。**在提交之前**可以一键清空改动，返回上一个版本，执行
`git checkout -- test2.py`
此时发现`test2.py`文件中的`我是错误`已经被删除了。

### 不再追踪时如何实现撤销追踪操作

> [!NOTE]**追踪的定义**
> 追踪：指git对文件的管理，git会记录文件的修改记录，并保存到本地仓库中，当文件被修改时，git会记录文件的修改记录，并保存到本地仓库中。**当使用`git add`命令将文件添加到暂存区**时，就实现了git对文件的追踪，此时通过`git checkout -- `命令无法再将文件一键还原。

入要撤销git对`test2.py`追踪操作，需要执行命令
`git reset HEAD test2.py`
输出
```
重置后取消暂存的变更：
M       test2.py
```
这时就可以实现一键还原。

### 回到上一个版本或指定版本

先改动`test2.py`，执行`git add test2.py`，`git commit -m "修改test2.py"`，此时`test2.py`的改动已经提交到本地仓库中。执行这一流程5次，于是`test2.py`已经实现了5个版本，如果想要回到上一版本或者指定版本，执行命令
`git reset --hard HEAD^`
其中`HEAD^`表示上一版本，`HEAD^^`表示上上版本，以此类推。得到输出为
```
HEAD 现在位于 b3a1ff7 修改test2.py到版本4
```
但如果版本较多，输入`^`控制回退的次数，会比较麻烦，此时可以通过提交id来控制回退的版本，如果想要回到版本2，执行命令`git log`找到版本2提交id为`ea8bc504393df8523cb040db90555f8aebfb236b`，此时执行
`git reset --hard ea8bc504393df8523cb040db90555f8aebfb236b`
得到输出为
```
HEAD 现在位于 ea8bc50 修改test2.py到版本2
```
这表示代码版本直接回到了版本2，而且可以看到相应的代码文件也已经回到了版本2时的代码。

### 指定文件版本回退

上一节的方法是将整个文件回退到指定版本，如果想要回退`test2.py`到指定版本4，执行命令`git log`找到版本4提交id为`bcbc45b2363bff1f3f1e284de1ddab254137c9bd`，执行
`git checkout bcbc45b2363bff1f3f1e284de1ddab254137c9bd -- test2.py`
其中`test2.py`为要回退的文件，`bcbc45b2363bff1f3f1e284de1ddab254137c9bd`为指定版本4的提交id。此时只有`test2.py`文件回退到指定版本4，其他文件没有回退。

### 修改内容后推送到远程仓库

之前我们新增了`test2.py`，和`gitest/test3.py`，此时如果想将这些改动保存到远程仓库，执行命令
`git add .`
`git commit -m "新增test2.py和gitest/test3.py"`
`git push origin main`
如果我们打开github查看的话可以发现，`main`就是当前仓库坐在分支（分支的概念以后再讲）。（此时涉及到远程连接，别忘了科学上网）。显示
```
枚举对象中: 51, 完成.
对象计数中: 100% (51/51), 完成.
使用 8 个线程进行压缩
压缩对象中: 100% (45/45), 完成.
写入对象中: 100% (48/48), 4.63 KiB | 4.63 MiB/s, 完成.
总共 48（差异 24），复用 0（差异 0），包复用 0（来自  0 个包）
remote: Resolving deltas: 100% (24/24), completed with 3 local objects.
To https://github.com/Damon-Chang/Embodied-AI.git
   8a9188c..9d106c7  main -> main
```
回到github查看，可以看到`main`分支增加了两个文件`test2.py`和`gitest/test3.py`。

### 创建版本标签以及标签管理

给当前版本的代码增加标签，可以执行
`git tag v1.0`
表示给最近提交的代码增加标签`v1.0`，此时执行`git tag`可以查看到标签`v1.0`，执行`git log`看到上一个提交的代码已经被打上了标签：
```
commit 9d106c7df377d4b05eb95f7902d19faede5b1bed (HEAD -> main, tag: v1.0, origin/main)
Author: DamonChang <18804012206@163.com>
Date:   Mon Mar 10 09:00:26 2025 +0800

    将指定文件回退到指定版本
```
如果想为指定版本的代码添加标签的话只需要在上面的命令后面添加对应提交版本的id，例如通过`git log`查看版本3的提交id为`f809a23`（前七位），若想要为其添加`v0.5`的标签，执行
`git tag v0.5 f809a23`
再通过`git tag`查看标签，得到输出
```
commit f809a23edb36139f57546f33ec61b41a9b8013d0 (tag: v0.5)
Author: DamonChang <18804012206@163.com>
Date:   Mon Mar 10 08:52:53 2025 +0800

    版本3
```
看到相应版本的标签成功添加。如果要删除指定标签，以`v0.5`为例，需要执行
`git tag -d v0.5`
显示
```
已删除标签 'v0.5'（曾为 f809a23）
```
如果想要将标签`v1.0`推送到远程仓库，执行
`git push origin v1.0`
输出
```
总共 0（差异 0），复用 0（差异 0），包复用 0（来自  0 个包）
To https://github.com/Damon-Chang/Embodied-AI.git
 * [new tag]         v1.0 -> v1.0
```
同时也可以在远程仓库中发现新增了tag变化。


### 创建、切换、删除远程分支

> [!NOTE]**分支**
> 在Git中，分支是一个指向提交对象的可变指针，它允许开发者在不影响主代码库的情况下，**并行**开展不同功能的开发、试验新想法、进行代码审查等。通过创建分支，团队成员能各自**独立**工作，隔离开发风险，方便管理不同版本的代码。当功能开发完成或问题修复后，分支上的代码可以通过合并操作整合到主分支，从而推动项目的持续演进。 

例如要创建一个名称为`kpitest`的分支，需要执行命令
`git branch kpitest`
再通过`git branch`查看分支，得到输出
```
  kpitest
* main
```
其中`*`表示所在的当前分支，`main`表示主分支。再用同样的方法创建一个名为`llm`的分支。如果想切换分支从`main`切换到`kpitest`，需要执行命令
`git checkout kpitest`
显示
```
切换到分支 'kpitest'
```
再通过`git branch`查看分支，得到输出
```
* kpitest
  llm
  main
```
此时`kpitest`分支被切换到，`main`分支还在。若要杀删除分支`llm`，需要执行命令
`git branch -d llm`
显示
```
已删除分支 llm（曾为 9d106c7）。
```
> [!NOTE]
> 不能删除当前所在的分支，若要删除当前所在分支，请先移动到其他分支。

如果要创建分支并跳转到刚刚创建的分支上，以`llm2`为例，执行命令
`git checkout -b llm2`
显示
```
切换到一个新分支 'llm2'
```
如果当前分支执行了`commit`操作，此时分支不能被删除，执行下`-D`可以强制删除
`git branch -D llm2`

### 合并分支

如果在`llm2`分支上修改了代码，执行了`commit`操作，此时要合并到`main`分支上，首先执行
`git checkout main`
切换到主分支，再执行命令
`git merge llm2`
输出
```
更新 9d106c7..d9a6fdd
Fast-forward
 .vscode/settings.json | 3 +++
 test2.py              | 2 ++
 2 files changed, 5 insertions(+)
 create mode 100644 .vscode/settings.json
```
这表示在llm2分支上修改了代码，并提交了，此时将llm2分支合并到main分支上。

### 合并分支时的冲突

如果两个分支的用户在同一文件中的同一位置，执行`git merge`操作，可能会出现冲突
```
自动合并 test2.py
冲突（内容）：合并冲突于 test2.py
自动合并失败，修正冲突然后提交修正的结果。
```
接着，在`main`分支上执行
`git merge --abort`
表示当前的合并只保留`main`分支的内容，其他分支被忽略。执行后发现其他分支的冲突信息被删除。但是若想保留二者，只需要在代码段中删除冲突提示即可
```python
<<<<<<< HEAD # 删除本行提示
    print("在main分支上改动代码2")
======= # 删除本行提示
    print("在llm2分支上改动代码")
>>>>>>> llm2 # 删除本行提示
```
此时查看状态`git status`，得到输出
```
位于分支 main
您的分支领先 'origin/main' 共 2 个提交。
  （使用 "git push" 来发布您的本地提交）

您有尚未合并的路径。
  （解决冲突并运行 "git commit"）
  （使用 "git merge --abort" 终止合并）

未合并的路径：
  （使用 "git add <文件>..." 标记解决方案）
        双方修改：   test2.py

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```
表示双方同时修改代码，**手动将代码中的冲突信息删除后**，执行`git add`命令，再执行`git commit`命令，进入一个可编辑界面
```
# 请为您的变更输入提交说明。以 '#' 开始的行将被忽略，而一个空的提交
# 说明将会终止提交。
#
# 位于分支 main
# 您的分支领先 'origin/main' 共 2 个提交。
#   （使用 "git push" 来发布您的本地提交）
#
# 所有冲突已解决但您仍处于合并中。
#
# 要提交的变更：
#       修改：     test2.py
```
键入`I`进入编辑模式，键入提交信息后`esc`退出并键入`:wq`保存并退出。状态信息为：
```
您的分支领先 'origin/main' 共 4 个提交。
  （使用 "git push" 来发布您的本地提交）

要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        修改：     test2.py
```
已经解决了冲突，提交保存即可。


---
## git多人分支集成协作时的常见场景
[🔝](#git入门)

### 不同人想要查看版本路线如何操作

先前已经介绍过`git log`命令，查看提交信息。`git log --oneline`命令查看提交id和信息，没有提交者信息：
```
d93fc92 (HEAD -> main, origin/main) 解决冲突之后的代码
c79ae9d Merge branch 'llm2'
7512e96 (llm2) 在llm2分支上修改
b40fae3 在main分支上修改
d9a6fdd 在llm2分支上改动代码
9d106c7 (tag: v1.0, kpitest) 将指定文件回退到指定版本
a016ebe 3的版本1
a437a3f 版本6
0396e88 版本5
bcbc45b 版本4
f809a23 版本3
ea8bc50 修改test2.py到版本2
29c9b17 修改test2.py到版本1
059fee2 修改test2.py
```
使用命令
`git log --oneline --graph`可以查看版本路线：
```
* d93fc92 (HEAD -> main, origin/main) 解决冲突之后的代码
*   c79ae9d Merge branch 'llm2'
|\  
| * 7512e96 (llm2) 在llm2分支上修改
* | b40fae3 在main分支上修改
|/  
* d9a6fdd 在llm2分支上改动代码
* 9d106c7 (tag: v1.0, kpitest) 将指定文件回退到指定版本
* a016ebe 3的版本1
* a437a3f 版本6
* 0396e88 版本5
* bcbc45b 版本4
* f809a23 版本3
* ea8bc50 修改test2.py到版本2
```
### 不同的人删除分支

补充一点：如果在github中手动改变一些地方，假设是手动添加了分支，`git branch -av`可查看分支变化情况。此时本地想要和远程仓库同步，需要执行
`git fetch`
输出
```
来自 https://github.com/Damon-Chang/Embodied-AI
 * [新分支]          test       -> origin/test
 * [新分支]          test1      -> origin/test1
 * [新分支]          test2      -> origin/test2
```
如果当前分支`test2`已经合并到主分支，已经不被需要，想要删除，可以执行命令
`git push origin --delete test2`
得到
```
To https://github.com/Damon-Chang/Embodied-AI.git
 - [deleted]         test2
```
在github远程仓库中观察到分支`test2`已经被删除.

> [!NOTE]
> 在删除分支之前要确认
> - 该分支已经合并到主分支；
> - 该分支已不被需要。

### 不同人修改了不同文件该如何处理

假设用户1在`test1`分支中修改了`test.txt`文件，用户2在`test1`分支中修改了`test2.txt`文件，那么当后者执行`git push`提交时会报错，在此之前应该进行合并操作
`git merge origin/test1`
进入可编辑区后键入修改信息。便可以成功推送。

### 不同人修改相同文件

---
## github拓展
[🔝](#git入门)

---
## 总结
[🔝](#git入门)


