# 小酷哥的文章（示例）

在今天的商业训练营的开源项目的产品经理的课程里，我了解到如何成为一个AI时代的个人创业者Solopreneur的一些知识和信息。

Solopreneurs的特点是：
1. 他们动作很快，快速Build，快速试错。
2. 他们只build自己用的产品。
3. 他们的产品不需要维护。

---

## CI 自动评分与运行指引
- 个人文章检测文件名：仓库根目录 {你的GitHub用户名}.md（例如：XiaoKuge.md）
- 课程作业检测仅在 PR 到 main 时执行，请通过 Pull Request 提交作业：
  - Lesson1：assignments/lesson1/{你的GitHub用户名}.md
  - Lesson2：assignments/lesson2/{你的GitHub用户名}.md
- 自动评分工作流： [.github/workflows/calculate-score.yml](.github/workflows/calculate-score.yml)
- 首次 Fork 后手动运行：
  1. 打开你 Fork 后的仓库页面，点击 Actions
  2. 选择 “Calculate Student Score” 工作流
  3. 点击 “Run workflow”，选择分支 main 并运行
  4. 在 Jobs 日志中查看成绩报告
