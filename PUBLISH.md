# 上传到 GitHub · 逐步操作

> 这个文件夹已经是一个**可以直接 push 的 git 仓库**（已 `git init` 并完成首个提交）。
> 你要做的只有三件事：改两处署名 → 在 GitHub 建空仓库 → push。

---

## 第 0 步：改两处署名（30 秒）

| 文件 | 改什么 |
|---|---|
| `LICENSE` 第 3 行 | `Copyright (c) 2026 learning-coach contributors` → 换成你的名字或 GitHub ID |
| `README.md` / `README.en.md` / `docs/*` | 搜 `ao66886`，如果不是你的账号就全局替换 |

改完记得再提交一次（见第 4 步）。

---

## 第 1 步：在 GitHub 建一个**空**仓库

打开 <https://github.com/new>：

| 字段 | 填什么 |
|---|---|
| Repository name | `learning-coach` |
| Description | `通用学习教练：一套可复制到任意 AI、任意学科的学习流程提示词与技能` |
| Visibility | Public（想私有也行，push 流程一样） |
| **Add a README / .gitignore / license** | **全部不要勾**（勾了会产生冲突，多一步 merge） |

点 **Create repository**，然后停在那页，把仓库地址复制下来。

---

## 第 2 步：push

在**本文件夹内**打开终端（Windows：在文件夹里右键 → Git Bash Here；或 `cd` 进来），逐行执行：

```bash
cd ~/Desktop/learning-coach

# 确认已在 main 分支
git branch -M main

# 关联远程仓库（把 ao66886 换成你的用户名）
git remote add origin https://github.com/ao66886/learning-coach.git

# 推上去
git push -u origin main
```

### 如果提示要密码

GitHub 从 2021 年起不接受账号密码，要用 **Personal Access Token**：

1. <https://github.com/settings/tokens> → Generate new token (classic)
2. 勾 `repo` 权限，设一个过期时间（90 天足够）
3. 复制生成的 `ghp_xxx`，**在密码框里粘它**

想免掉这一步，装 [GitHub CLI](https://cli.github.com/) 后 `gh auth login` 一次即可。

---

## 第 3 步：用 GitHub CLI 一步搞定（可选，更快）

装好 `gh` 并 `gh auth login` 之后，第 1、2 步合成一条命令：

```bash
cd ~/Desktop/learning-coach
gh repo create learning-coach --public --source=. --remote=origin --push \
  --description "通用学习教练：一套可复制到任意 AI、任意学科的学习流程提示词与技能"
```

它会自动建仓、关联、推送，一步到位。

---

## 第 4 步：后续怎么更新

```bash
cd ~/Desktop/learning-coach
git add .
git commit -m "docs: 补充 XX 案例"
git push
```

改提示词时建议先改 `prompt/learning-coach-zh.md`，再同步 `skill/learning-coach/SKILL.md`，最后在 `CHANGELOG.md` 加一行。**两份内容必须一致**，这是最容易忘的地方。

---

## 第 5 步：把仓库“装修”一下（5 分钟，明显提升观感）

### About 栏

点仓库首页右上角齿轮，填：

```
Description: 通用学习教练 · 一套可复制到任意 AI、任意学科的学习流程提示词与技能（Prompt + Skill）
Website: （留空）
```

### Topics（决定别人能不能搜到你）

```
study  learning  prompt  prompt-engineering  ai-tutor  study-planning
exam-prep  cornell-notes  llm  skill  chinese  education
```

### 发一个 Release

右侧 **Releases → Create a new release**：

- Tag: `v1.0.0`
- Title: `v1.0.0 — 首个公开版本`
- 描述直接把 `CHANGELOG.md` 里 v1.0.0 那一段粘进去

有 Release 的仓库，别人点进来会默认认为它是“成品”而不是“草稿”。

---

## 上传前自查清单

- [ ] `LICENSE` 里的名字已改成你自己
- [ ] README 里的 `ao66886` 已全局替换（`README.md`、`README.en.md`、`docs/usage.md`、`PUBLISH.md` 本身）
- [ ] 没有个人隐私：学校、班级、学号、成绩、联系方式
- [ ] 没有整段复制教材、付费课程讲义、题库原文
- [ ] HTML 文件在浏览器里能正常打开（双击试一下）
- [ ] `git log` 里第一条提交信息看得过去

---

## 常见问题

**Q：`git push` 报 `remote origin already exists`**
先删掉再重加：

```bash
git remote remove origin
git remote add origin https://github.com/<你的用户名>/learning-coach.git
```

**Q：报 `SSL certificate problem` 或连接超时**
多半是代理问题。有梯子的话让 Git 走代理：

```bash
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

不用代理就取消：`git config --global --unset http.proxy`

**Q：报 `LF will be replaced by CRLF` 警告**
Windows 换行符提示，**不是错误**，可以忽略。

**Q：中文文件名在 GitHub 上显示成 `%E5%AD%A6...`**
本仓库所有**文件名**已经用英文（内容仍是中文），就是为了避开这个问题。你自己加文件时也建议照这个来。

**Q：想改仓库名怎么办**
GitHub 上 Settings → Rename 自动重定向，但记得同步改 README 里的 clone 地址。

**Q：能不能不公开？**
可以，第 1 步选 Private。但 Private 仓库的 README 不会显示徽章图（shields.io 仍可用），也不会有陌生人给你提 issue。
