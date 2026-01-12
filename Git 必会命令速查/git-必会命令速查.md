# Git 必会命令速查

[toc]

## 前言

因为准备把 `量化研究` 系列的笔记和代码放到 GitHub 上，很久没用 Git 了，对常用命令记不太清楚，所以整理了这份速查表，方便日常使用。以下内容<mark>主要由 VSCode Copilot 插件中的  `GPT 5.2`  模型生成</mark>。

> 目标：覆盖日常 90% 场景的最小命令集。
> 建议配合：`git status`（随时看状态） + 小步提交（频繁 commit）。

## 把内容存到 GitHub 上有哪些好处？

- 版本管理：每次修改都有记录（可对比、可回滚），方便追踪“哪次改动导致结果变化”。
- 备份与多设备同步：本地电脑损坏 / 重装不怕；在多台电脑之间保持同一份最新代码与笔记。
- 复现与可追溯：量化研究经常需要复现结论，Git 能把“结论 ↔ 对应代码 /Notebook 版本”关联起来。
- 协作与讨论：可以用 Issue/PR 进行讨论、评审与协作；也方便他人 Fork 后复用与改进。
- 自动化：结合 GitHub Actions 可做测试、格式化、Notebook 运行 / 导出等自动化，减少手工操作和出错。
- 展示与沉淀：形成可公开的作品集与知识库（文章 /Notebook/ 工具脚本），长期积累更清晰。

> 小提示：如果仓库里包含数据文件或大图片，建议用 `.gitignore` 管理；需要分享大文件可考虑 Git LFS。

## 1. 初始化 / 克隆

- 初始化本地仓库：`git init`
- 从远端克隆：`git clone <url>`

## 2. 日常三件套（最常用）

- 看状态：`git status`
  - 常用机器可读：`git status --porcelain=v1 -b`
- 暂存改动：`git add <file>` 或 `git add .`
- 提交改动：`git commit -m "message"`

## 3. 查看历史与差异

- 看提交历史（推荐组合）：`git log --oneline --graph --decorate --all`
- 看差异：
  - 工作区 vs 暂存区：`git diff`
  - 暂存区 vs 最新提交：`git diff --staged`
- 看某次提交：`git show <commit>`

## 4. 分支（协作必备）

- 列出分支：`git branch`
- 创建并切换分支：`git switch -c <new-branch>`
- 切换分支：`git switch <branch>`
- 合并分支：`git merge <branch>`
- 变基（让历史更线性）：`git rebase <branch>`

## 5. 远端同步（推 / 拉）

- 查看远端：`git remote -v`
- 添加远端：`git remote add origin <url>`
- 抓取远端更新（不改本地文件）：`git fetch`
- 拉取并合并：`git pull`
- 拉取并变基（更常用、更干净）：`git pull --rebase`
- 推送：`git push`
- 首次推送并设置上游：`git push -u origin main`

## 6. 撤销 / 修复（非常重要）

- 丢弃工作区对某文件的修改：`git restore <file>`
- 撤销暂存（保留工作区改动）：`git restore --staged <file>`

- 回退到某提交（慎用，尤其是 `--hard`）：
  - 只回退提交，保留工作区改动：`git reset --soft <commit>`
  - 回退提交与暂存，保留工作区改动：`git reset --mixed <commit>`
  - 回退提交 + 丢弃工作区改动：`git reset --hard <commit>`

- 用“反向提交”撤销某提交（更安全，适合已推送的历史）：`git revert <commit>`

- 临时把改动收起来：
  - 暂存：`git stash`
  - 恢复：`git stash pop`

## 7. 文件操作与忽略

- 重命名 / 移动（让 Git 更容易识别为 rename）：`git mv <old> <new>`
- 删除并纳入版本控制：`git rm <file>`
- 忽略文件：`.gitignore`
  - 示例：忽略所有 markdown_img：`**/markdown_img/`

## 8. 两个常用工作流模板

### A) 写文章 / 改代码并推到 GitHub

1) `git status`
2) `git add .`
3) `git commit -m "docs: update"`
4) `git push`

### B) 先同步远端再开始干活（避免冲突）

1) `git pull --rebase`
2) 开始修改
3) `git add .`
4) `git commit -m "..."`
5) `git push`

## 9. 常见坑（Windows/ 中文路径）

- `git ls-files` 设置中文正常显示（适用于中文类似`\346\211`一大串）：
  - `git config --global core.quotepath false`
- 大小写重命名（如 readme.md -> README.md）在 Windows 可能不生效：
  - 用两步：`git mv readme.md tmp.md` 再 `git mv tmp.md README.md`

## 后记

得益于 AI 的强大，即便不熟悉 Git 命令，也能在 AI 的帮助下，快速上手并完成日常工作。希望这份速查表能帮到你！

因为公众号要修改文章太麻烦了，以后如果文章或代码有更新，只会在[ GitHub 上发布](https://github.com/purequant/QuantitativeResearch)，欢迎大家多多关注和 Star！