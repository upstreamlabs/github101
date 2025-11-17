# Git工具安装与使用报告

## 学员GitHub用户名: tmacychen

## 1. Git安装过程

1. 查询 Git 的官方网站

通过搜索获得 Git 的官网，了解安装方法与 Git 下载方式。Git 官网: https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git

在MacOS 上安装，需要安装Xcode Command Line Tools，默认就安装了 Git 工具。

在 Linux 上，不同发行版使用不同的包管理器，可以直接在包管理器上安装。
例如 RHEL 或 CentOS），你可以使用 dnf：

```
$ sudo dnf install git-all
```

使用了Debian系的 Linux，可以使用 apt 来安装：
```
$ sudo apt instlal git-all
```

在 Windows 上，直接下载安装 Git 安装包。在Windows上运行的 Git，会在 msys 的环境中运行。

在 Windows 上，也可以使用 WSL 来安装 Linux 发行版，在 Linux 中使用 Git 会相对方便一些。



## 2. 遇到的问题及解决方法

曾经在 Windows 上安装过 Git，主要遇到的问题有：

1. 安装后可以右键菜单中打开 Git 命令行，但如果需要在 Windows 的终端中使用 Git，还需要考虑在环境变量中将 Git 命令路径添加到PATH中。

2. Windows 的换行符是`\r\n`,而 Git 服务器一般在 Linux 环境下运行，其换行符是`\r`,因此需要配置 Git 的换行符替换配置。

```
# 全局配置（仅需执行一次）
git config --global core.autocrlf true  # Windows 用户：提交时转换为 LF，拉取时转换为 CRLF
git config --global core.autocrlf input  # Linux/macOS 用户：提交时转换为 LF，拉取时不转换
```



## 3. 版本信息截图

目前我使用的是 MacOS 系统，截图如下：

<img width="664" height="58" alt="2025-11-17_17-00-41" src="https://github.com/user-attachments/assets/ab9aea8d-0e76-443f-b483-70bd3508f71c" />


## 4. Git命令使用过程总结

（在此处总结使用Git命令的过程，包括但不限于以下操作：

### 常用命令
- git clone: 克隆远程仓库到本地
- git add: 添加文件到暂存区
- git commit: 提交更改到本地仓库
- git push: 推送更改到远程仓库
- git pull: 从远程仓库拉取最新更改
- git tag : 创建一个快照，将当前状态保存在 tag 中，一般用于版本发布打标签。
- git log :查看当前分支的变更历史记录，可以分页查看

### 分支管理

- git branch :查看当前本地分支
- git branch -a : 查看分支，包括本地分支与远程分支
- git branch -d branch1 : 在本地删除某个分支
- git switch -c branch1 :创建新的分支并切换过去
- git checkout ：也可以用来切换分支，但容易混淆分支名与文件名。
- git stash : 用于保存当前修改到缓存区中。当修改的内容不希望加入 commit 中，但又希望现在切换到其他分支时，可以用 stash 保存起来，等切换回来后再恢复。
- git rebase : 重新梳理分支的变更记录，比如合并某些 commit，删除某些 commit等。
- git cherry-pick：将某个或某些commit 从一个分支中挑出来，合入另一个分支。

### 文件修改与恢复

- git restore :恢复某个文件,不改变提交历史，仅操作工作区域缓存区
- git reset : 回退提交历史，移动分支指针来修改提交记录。
- git diff :显示当前修改的文件差异点
- git merge :合并分支到本地，如果遇到冲突，需要手动修改冲突，打开冲突文件，在文件中会提示类似如下内容：
```
<<<<<<< HEAD
当前分支的代码
=======
合并分支的代码
>>>>>>> source-branch
```
