# Git工具安装与使用报告

## 学员GitHub用户名: Daily-AC

## 1. Git安装过程

### 操作系统环境
- **操作系统**: Windows 11 专业版
- **系统架构**: x64
- **安装方式**: Git for Windows 官方安装包

### 详细安装步骤

#### 步骤 1：下载安装包
访问 Git 官方网站 [https://git-scm.com/download/win](https://git-scm.com/download/win)，下载最新版本的 Git for Windows 安装程序（64-bit）。当前安装的版本为 **2.51.1**。

#### 步骤 2：运行安装程序
双击下载的 `Git-2.51.1-64-bit.exe` 安装文件，启动安装向导。

#### 步骤 3：配置安装选项
在安装过程中，我选择了以下关键配置：

1. **组件选择**
   - ✅ Git Bash Here（右键菜单集成）
   - ✅ Git GUI Here（图形界面）
   - ✅ Associate .git* configuration files
   - ✅ Associate .sh files to be run with Bash
   - ✅ Windows Terminal 集成

2. **默认编辑器**
   - 选择 **Visual Studio Code** 作为 Git 默认编辑器
   - 这样在编写 commit message 时会自动打开 VS Code

3. **PATH 环境配置**
   - 选择 **Git from the command line and also from 3rd-party software**
   - 这样可以在 CMD、PowerShell、Windows Terminal 中都能使用 Git

4. **SSH 可执行文件**
   - 使用捆绑的 OpenSSH

5. **HTTPS 传输后端**
   - 使用 OpenSSL 库

6. **行尾转换配置**
   - 选择 **Checkout Windows-style, commit Unix-style line endings**
   - 这是 Windows 开发者的推荐设置

7. **终端模拟器**
   - 选择 **Use Windows' default console window**
   - 与 Windows Terminal 更好地集成

8. **其他配置**
   - 启用文件系统缓存（提升性能）
   - 启用 Git Credential Manager（管理凭据）
   - 启用符号链接支持

#### 步骤 4：完成安装
点击 "Install" 按钮，等待安装完成。安装时间约 2-3 分钟。

#### 步骤 5：验证安装
安装完成后，打开 Windows Terminal（或 CMD），执行以下命令验证：

```bash
git --version
```

输出结果：`git version 2.51.1.windows.1`，说明安装成功！

## 2. 遇到的问题及解决方法

### 问题 1：中文路径乱码问题
**现象**：在 Git Bash 中，包含中文的文件路径显示为乱码（如 `\350\256\255\347\273\203\350\220\245`）

**原因**：Git 默认对非 ASCII 字符进行转义显示

**解决方法**：
```bash
# 禁用路径转义，正确显示中文
git config --global core.quotepath false
```

执行后，中文路径能正常显示，例如：`assignments/训练营/lesson1.md`

---

### 问题 2：Git Credential Manager 首次登录
**现象**：首次 `git push` 时提示需要登录 GitHub

**解决方法**：
1. 现代 Git 会自动打开浏览器进行 OAuth 授权
2. 在浏览器中登录 GitHub 账号并授权
3. Git Credential Manager 会自动保存凭据，后续操作无需重复登录

**最佳实践**：
- 对于长期使用，推荐配置 SSH 密钥代替 HTTPS
- SSH 配置步骤：
  ```bash
  # 生成 SSH 密钥对
  ssh-keygen -t ed25519 -C "qifenzhiyi142857@gmail.com"

  # 将公钥添加到 GitHub Settings → SSH and GPG keys
  cat ~/.ssh/id_ed25519.pub
  ```

---

### 问题 3：行尾符（CRLF vs LF）警告
**现象**：执行 `git add` 时出现警告：
```
warning: LF will be replaced by CRLF in xxx.md
```

**原因**：Windows 使用 CRLF（`\r\n`）作为行尾符，而 Linux/macOS 使用 LF（`\n`）。跨平台协作时会产生冲突。

**解决方法**：
```bash
# 推荐配置（已在安装时选择）
git config --global core.autocrlf true

# 或在项目根目录创建 .gitattributes 文件
echo "* text=auto" > .gitattributes
```

**说明**：
- `core.autocrlf true`：提交时自动转换 CRLF → LF，检出时转换 LF → CRLF
- 这样在 Windows 上开发，推送到仓库时自动统一为 LF

---

### 问题 4：大文件推送失败
**现象**：推送包含大文件（>100MB）的提交时失败

**解决方法**：
使用 Git LFS（Large File Storage）管理大文件：
```bash
# 安装 Git LFS（Git for Windows 2.x 已内置）
git lfs install

# 追踪大文件类型（如模型文件）
git lfs track "*.pth"
git lfs track "*.bin"

# 提交 .gitattributes 文件
git add .gitattributes
git commit -m "Add Git LFS tracking"
```

## 3. 版本信息截图

由于这是文本文档，我以代码块形式展示执行结果：

```bash
$ git --version
git version 2.51.1.windows.1

$ git config --list --show-origin | grep user
file:C:/Users/29084/.gitconfig  user.name=Daily-AC
file:C:/Users/29084/.gitconfig  user.email=qifenzhiyi142857@gmail.com
```

**Git 配置信息**：
- ✅ Git 版本：2.51.1（2024年11月发布的最新稳定版）
- ✅ 用户名：Daily-AC
- ✅ 邮箱：qifenzhiyi142857@gmail.com
- ✅ 默认分支名：main（已配置）

## 4. Git命令使用过程总结

作为一名活跃的开发者，我每天都在使用 Git 进行版本控制。以下是我对常用 Git 命令的使用体验和理解：

### 核心工作流命令

#### `git clone` - 克隆远程仓库到本地

**使用场景**：首次获取项目代码

```bash
# HTTPS 方式（推荐新手）
git clone https://github.com/Daily-AC/qiAgent.git

# SSH 方式（推荐长期使用）
git clone git@github.com:Daily-AC/qiAgent.git

# 克隆指定分支
git clone -b develop https://github.com/Daily-AC/qiAgent.git

# 浅克隆（只获取最近历史，节省空间和时间）
git clone --depth=1 https://github.com/Daily-AC/qiAgent.git
```

**心得体会**：
- 对于大型仓库（如机器学习项目含大模型文件），使用 `--depth=1` 可以显著加速克隆
- SSH 方式配置好后比 HTTPS 更方便，不用每次输入密码
- 我的 qiAgent 项目就是通过 `git clone` 克隆到本地，然后开始开发的

---

#### `git add` - 添加文件到暂存区

**使用场景**：选择要提交的文件变更

```bash
# 添加单个文件
git add README.md

# 添加所有修改的文件
git add .

# 添加所有 Python 文件
git add *.py

# 交互式添加（可选择性暂存代码块）
git add -p
```

**心得体会**：
- `git add .` 是我最常用的命令，但在大型项目中需谨慎，避免误添加临时文件
- `git add -p` 是高级用法，可以只提交一个文件的部分修改（代码审查时很有用）
- 养成好习惯：添加前先用 `git status` 检查，避免添加不该提交的文件（如 `.env`、`__pycache__/`）

**实际案例**：
在开发 qiAgent 时，我经常需要同时修改多个文件（Python 后端 + HTML 前端），但分开提交以保持 commit 历史清晰：
```bash
git add pdfprocessor.py qibot.py
git commit -m "feat: 优化简历解析和对话逻辑"

git add templates/*.html static/*.css
git commit -m "style: 更新 Web 界面样式"
```

---

#### `git commit` - 提交更改到本地仓库

**使用场景**：将暂存区的修改保存为一个版本快照

```bash
# 基础提交
git commit -m "feat: 添加模拟面试功能"

# 详细提交（打开编辑器编写多行说明）
git commit

# 跳过暂存区直接提交所有已跟踪文件的修改
git commit -a -m "fix: 修复简历解析中文乱码问题"

# 修改上一次提交（谨慎使用！）
git commit --amend -m "feat: 添加模拟面试功能（包含语音识别）"
```

**心得体会**：
- **Commit Message 规范**非常重要！我遵循 Conventional Commits 规范：
  - `feat:` 新功能
  - `fix:` 修复 Bug
  - `docs:` 文档更新
  - `style:` 代码格式（不影响功能）
  - `refactor:` 重构
  - `test:` 测试相关
  - `chore:` 构建/工具链更新

- **提交频率**：我倾向于"小步快跑"，每完成一个小功能就提交，而不是一次性提交大量代码
- `git commit --amend` 仅用于修改**未推送**的提交，已推送的提交不要 amend（会导致历史冲突）

**优秀 Commit Message 示例**：
```
feat(qiAgent): 实现基于 MCP 的多 Agent 协同框架

- 新增 mcp_server 模块，支持 HTTP MCP 协议
- 实现 pdfprocessor、qibot、asrbot 三个专业 Agent
- 集成 OpenAI 兼容 API，支持多种 LLM 后端

Closes #12
```

---

#### `git push` - 推送更改到远程仓库

**使用场景**：将本地提交同步到 GitHub

```bash
# 推送当前分支到远程
git push

# 首次推送新分支（设置上游跟踪）
git push -u origin feature/interview-bot

# 推送所有分支
git push --all

# 推送标签
git push --tags

# 强制推送（危险！仅用于个人分支）
git push --force
```

**心得体会**：
- 推送前先 `git pull`，避免远程有新提交导致冲突
- 在团队协作中，**绝对不要** `git push --force` 到 main/master 分支
- 我在开发 qiAgent 新功能时，会创建独立分支（如 `feature/voice-interview`），开发完成后再合并到主分支

**典型工作流**：
```bash
# 1. 创建功能分支
git checkout -b feature/job-matching

# 2. 开发并提交
git add classified_data/*.py
git commit -m "feat: 实现智能岗位匹配算法"

# 3. 推送到远程
git push -u origin feature/job-matching

# 4. 在 GitHub 创建 Pull Request 进行代码审查
# 5. 审查通过后合并到 main 分支
```

---

#### `git pull` - 从远程仓库拉取最新更改

**使用场景**：同步远程仓库的最新代码到本地

```bash
# 拉取当前分支的最新代码
git pull

# 拉取并变基（保持线性历史）
git pull --rebase

# 拉取指定分支
git pull origin develop

# 拉取所有分支信息
git fetch --all
```

**心得体会**：
- `git pull` = `git fetch` + `git merge`
- 我更推荐使用 `git pull --rebase`，可以避免不必要的合并提交，保持历史整洁
- 在团队协作时，每天开始工作前先 `git pull`，避免长时间不同步导致大量冲突

**处理拉取冲突**：
```bash
# 拉取时发现冲突
git pull
# Auto-merging qibot.py
# CONFLICT (content): Merge conflict in qibot.py

# 1. 打开冲突文件，手动解决冲突
# 2. 标记为已解决
git add qibot.py

# 3. 完成合并
git commit -m "Merge branch 'main' - 解决对话逻辑冲突"
```

---

### 高级命令使用体验

#### `git status` - 查看工作区状态

**我最常用的命令之一**，几乎每次操作前都会先 `git status` 确认状态。

```bash
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  modified:   Daily-AC.md

Untracked files:
  assignments/lesson1/Daily-AC.md
  assignments/lesson2/Daily-AC.md
```

---

#### `git log` - 查看提交历史

```bash
# 美化的提交历史
git log --oneline --graph --all --decorate

# 查看某个文件的修改历史
git log -p qibot.py

# 查看最近 5 次提交
git log -5
```

**我的别名配置**：
```bash
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# 使用
git lg
```

---

#### `git branch` - 分支管理

```bash
# 查看所有分支
git branch -a

# 创建新分支
git branch feature/export-pdf

# 切换分支
git checkout feature/export-pdf
# 或使用新命令
git switch feature/export-pdf

# 创建并切换（一步到位）
git checkout -b feature/export-pdf

# 删除分支
git branch -d feature/export-pdf
```

**分支命名规范**（我在 qiAgent 项目中使用）：
- `feature/xxx` - 新功能分支
- `fix/xxx` - Bug 修复分支
- `refactor/xxx` - 重构分支
- `docs/xxx` - 文档更新分支

---

#### `git diff` - 查看差异

```bash
# 查看工作区与暂存区的差异
git diff

# 查看暂存区与最后一次提交的差异
git diff --staged

# 对比两个分支
git diff main..feature/interview-bot
```

---

#### `git stash` - 暂存工作现场

**使用场景**：正在开发功能时，需要紧急切换到另一个分支修复 Bug

```bash
# 暂存当前修改
git stash save "正在开发面试评分功能"

# 切换分支修复 Bug
git checkout main
# 修复...
git commit -m "hotfix: 修复简历上传失败问题"

# 切回原分支，恢复暂存
git checkout feature/interview-scoring
git stash pop
```

---

### 团队协作命令

#### `git remote` - 管理远程仓库

```bash
# 查看远程仓库
git remote -v

# 添加远程仓库（用于 Fork 后的上游同步）
git remote add upstream https://github.com/original-owner/repo.git

# 同步上游仓库
git fetch upstream
git merge upstream/main
```

**实际应用**：
我参加开源商业训练营时，Fork 了官方仓库 `UpstreamLabs/camp`，然后添加上游仓库以同步最新课程内容：
```bash
git remote add upstream https://github.com/UpstreamLabs/camp.git
git fetch upstream
git merge upstream/main
```

---

#### `git rebase` - 变基（高级用法）

**使用场景**：保持提交历史线性

```bash
# 将当前分支变基到 main 分支
git rebase main

# 交互式变基（合并/编辑/删除提交）
git rebase -i HEAD~3
```

**注意**：已推送到远程的提交不要 rebase，会导致团队成员冲突！

---

### 撤销与回退命令

```bash
# 撤销工作区修改（危险！）
git checkout -- file.py

# 撤销暂存区文件
git reset HEAD file.py

# 回退到上一个版本（保留工作区修改）
git reset --soft HEAD^

# 回退到上一个版本（丢弃所有修改，危险！）
git reset --hard HEAD^
```

---

## 总结与感悟

通过几年的 Git 使用经验，我深刻体会到：

1. **Git 是开发者必备技能**：无论个人项目还是团队协作，Git 都是不可或缺的工具
2. **良好的 Commit 习惯**：清晰的提交信息 + 合理的提交粒度，能让项目历史一目了然
3. **分支工作流**：Feature Branch 工作流能有效降低协作冲突
4. **持续学习**：Git 命令众多，但核心命令就那几个，其他命令遇到需求时再学即可
5. **工具辅助**：VS Code 的 GitLens 插件、GitHub Desktop 等图形化工具能提升效率

在开发 qiAgent 项目时，Git 帮助我：
- ✅ 管理多个功能分支的并行开发
- ✅ 通过 `.gitignore` 排除敏感文件（如 API Key）
- ✅ 使用 Git LFS 管理机器学习模型文件
- ✅ 通过 GitHub Actions 实现 CI/CD 自动化

**最后建议**：新手不要被 Git 的复杂性吓倒，先掌握基础工作流（clone → add → commit → push → pull），其他命令用到时再学。记住：**多练习，多犯错，多 Google**，你会发现 Git 其实没那么难！

---

## CI 自动评分与运行指引
- 课程作业检测仅在 PR 到 main 时执行，请通过 Pull Request 提交本文件。
- 文件命名：assignments/lesson2/{你的GitHub用户名}.md。
- 自动评分工作流： [.github/workflows/calculate-score.yml](../../.github/workflows/calculate-score.yml)。
- 首次 Fork 后：进入 Actions → 选择 "Calculate Student Score" → 点击 "Run workflow" 并选择 main → 在日志中查看成绩。
