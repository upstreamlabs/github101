# Git工具安装与使用报告

## 学员GitHub用户名: RaQiu

## 1. Git安装过程

在macOS上安装Git非常直接。我使用了Homebrew方式：

```bash
$ brew install git
```

安装过程大概用了1分钟，Homebrew自动处理了所有依赖。安装完成后，打开一个新的终端窗口验证：

```bash
$ git --version
git version 2.39.3
```

## 2. 遇到的问题及解决方法

**问题1：Homebrew未安装**
首次运行`brew`命令时提示"command not found"。解决方法是先安装Homebrew：
```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
安装完成后需要关闭并重新打开终端。

**问题2：首次使用Git时提示配置用户名和邮箱**
执行`git commit`时提示需要配置身份：
```bash
$ git config --global user.name "RaQiu"
$ git config --global user.email "qiu@example.com"
```

**问题3：克隆仓库时权限错误**
使用HTTPS方式克隆时提示权限被拒绝。解决方法是先配置凭据管理器：
```bash
$ git config --global credential.helper osxkeychain
```
这样密码会被安全地存储在macOS钥匙串中。

## 3. 版本信息截图

在终端执行`git --version`后显示：
```
git version 2.39.3
```

## 4. Git命令使用过程总结

Fork upstreamlabs/github101仓库到我的账户后，开始本地操作：

```bash
# 克隆仓库
$ git clone https://github.com/RaQiu/github101.git
$ cd github101

# 创建作业文件并编辑
$ mkdir -p assignments/lesson2
$ touch assignments/lesson2/RaQiu.md
# 使用VS Code编辑内容...

# 查看状态
$ git status
Untracked files:
  assignments/lesson2/RaQiu.md

# 添加到暂存区
$ git add assignments/lesson2/RaQiu.md

# 提交到本地仓库
$ git commit -m "Add lesson 2 assignment - RaQiu"

# 推送到远程
$ git push origin main
```

最后，在GitHub网页上创建了Pull Request。

**使用体会**：Git的核心是三个状态——工作区、暂存区、仓库区。`add`负责将文件从工作区移到暂存区，`commit`将暂存区内容保存到仓库，`push`则将本地仓库同步到远程。macOS上使用Git很流畅，配合Homebrew管理版本也很方便。这次作业让我熟悉了完整PR流程，对后续参与开源项目很有帮助。

---

## CI 自动评分与运行指引
- 课程作业检测仅在 PR 到 main 时执行，请通过 Pull Request 提交本文件。
- 文件命名：assignments/lesson2/{你的GitHub用户名}.md。
- 自动评分工作流： [.github/workflows/calculate-score.yml](../../.github/workflows/calculate-score.yml)。
- 首次 Fork 后：进入 Actions → 选择 “Calculate Student Score” → 点击 “Run workflow” 并选择 main → 在日志中查看成绩。