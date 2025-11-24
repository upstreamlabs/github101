# github101

本仓库为UpStream 商业训练营**GitHub基础课**作业使用

Upstream 这个代码仓用于帮助商业训练营的同学们完成作业。

## 作业安排：

每位同学首先：

1. 构建自己的仓库 Fork本仓库
2. **在训练营官网个人中心，编辑个人信息，填写 Githubname（如不完成此步骤，将无法在训练营官网排行榜处获取成绩）。**
3. 以Markdown的格式(.md)提交一篇文章 写一篇有关训练营/自己组队的想法的文章，笔记等，提交到自己的Repo请使用自己的GitHub 用户名命名该md文件。
4. 至少给其他同学的3个repo各提1个issue。
5. 给其他同学的repo 10个stars
6. 解决自己Repo至少一个issue。
7. 获得10个stars 想办法为自己的Repo获得十个点赞
8. 提交PR
9. 完成实验后，可以在训练营官网排行榜处查看成绩 [导学阶段 - 第一期源起之道开源商业创新营 - 源起之道开源商业创新营 - 训练营](https://opencamp.cn/UpstreamLabs/camp/S1/stage/0?tab=rank)

## 基础阶段第一课作业

### 作业要求
在 [assignments/lesson1](assignments/lesson1) 目录下，选择以下任一开源商业模式进行分析，并提交分析报告：
- Odoo 商业模式
- 安卓商业模式
- 红帽商业模式
- Linux 基金会商业模式
- Apache 商业模式

### 提交方式
1. 复制 [assignments/lesson1/example-report.md](assignments/lesson1/example-report.md) 并重命名为您的 GitHub 用户名
2. 按照模板要求完成分析报告
3. 提交 Pull Request

## 基础阶段第二课作业：Git工具实践

### 作业要求
1. 完成版本控制工具git安装，通过执行`git --version`查看版本信息，并截图
2. fork仓库 https://github.com/upstreamlabs/github101 到自己账号下，将个人账号下的github101（可以是fork时自定义项目名）克隆到本地（指操作设备），在[assignments/lesson2](assignments/lesson2)目录下创建以个人账号（GitHub账号）命名的markdown文件，在文件中撰写git安装过程、遇到的问题及解决方法，以及使用命令查看版本信息的截图。
3. 通过git命令将本地仓库提交到远程仓库（个人账号），向远程仓库（组织仓）提交PR合入请求。
4. 将使用git命令过程总结记录到第2步中的markdown文件，最后再次执行第3步操作提交。

### 提交方式
1. 复制 [assignments/lesson2/example-report.md](assignments/lesson2/example-report.md) 并重命名为您的 GitHub 用户名
2. 按照模板要求完成实践报告
3. 提交 Pull Request

## 自动评分系统

本仓库包含一个自动评分系统，用于评估学员在GitHub上的参与度和贡献。评分系统会根据以下指标自动计算分数：

### 计分标准

| 指标 | 权重 | 说明 |
|------|------|------|
| Stars | 10分/个 | 每获得一个star得10分 |
| 已解决的Issues | 20分/个 | 每解决一个issue得20分 |
| Pull Requests | 30分/个 | 每提交一个PR得30分 |
| 个人文章提交 | 20分 | 提交以自己GitHub用户名命名的.md文章得20分 |

### 总分说明

- 系统会每天自动计算分数并在终端输出成绩报告
- 总分上限为9999分
- 学员可以通过积极参与获得更多分数，没有严格的上限限制
- 评分结果会通过API发送到课程系统

### 如何查看自己的分数

- 系统每天北京时间早上8点自动运行计算分数
- 每次向仓库 push 到 main 分支时触发分数计算
- 可在 GitHub Actions 界面手动触发计算（首次 Fork 需手动运行）

#### 自动评分系统（CI）运行说明
- 工作流文件： [.github/workflows/calculate-score.yml](.github/workflows/calculate-score.yml)
- 触发条件：
  - 定时：每天 08:00（北京时区，UTC 00:00）
  - push：推送到 main 分支
  - pull_request：向 main 分支发起或更新 PR（用于课程作业检测）
  - 手动：在 Actions 页面使用 Run workflow
- 课程作业检测仅在 PR 事件时执行。请通过 PR 提交作业文件：
  - Lesson1：assignments/lesson1/{你的GitHub用户名}.md
  - Lesson2：assignments/lesson2/{你的GitHub用户名}.md
- 个人文章检测文件名：仓库根目录 {你的GitHub用户名}.md

#### 首次 Fork 后手动运行指引
1. 打开你 Fork 后的仓库的 GitHub 页面，点击 Actions
2. 左侧选择 Calculate Student Score 工作流
3. 点击 Run workflow，选择分支 main，确认运行
4. 运行完成后在 Jobs 的日志中查看成绩报告