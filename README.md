# Agent Skills Sync

个人 Agent Skills 配置同步仓库。用于跨设备同步 AI Agent（OpenClaw、Claude Code、Codex 等）的技能配置。

> **注意**：这不是 Skill 发布仓库。自制 Skills 请使用单独的仓库（如 `canxing/my-skills`）。

## 快速开始

### 新机器初始化

```bash
# 1. 克隆仓库
git clone https://github.com/canxing/agent-skills.git
cd agent-skills

# 2. 安装所有 skills
npx skills experimental_install -y

# 3. 验证安装
npx skills list
```

## 日常使用

### 添加新 skill（第三方）

```bash
# 搜索 skill
npx skills find <关键词>

# 安装并记录到锁定文件
npx skills add <owner/repo> --skill <skill-name>

# 提交到 Git
git add skills-lock.json
git commit -m "Add <skill-name>"
git push
```

### 更新 skills

```bash
# 方式1：从锁定文件重新安装（推荐，确保版本一致）
npx skills experimental_install -y

# 方式2：检查并更新到最新版本
npx skills check          # 查看可更新的 skills
npx skills update         # 更新所有 skills
git add skills-lock.json  # 更新后的锁定文件会变化
git commit -m "Update skills"
git push
```

### 移除 skill

```bash
# 交互式移除
npx skills remove

# 或指定移除
npx skills remove <skill-name> -y

# 提交变更
git add skills-lock.json
git commit -m "Remove <skill-name>"
git push
```

### 同步其他设备的更新

```bash
# 拉取最新锁定文件
git pull

# 应用变更
npx skills experimental_install -y
```

## 开发自己的 Skills

如需开发自制 Skills，请使用单独的 Skill 发布仓库：

```bash
# 创建独立的 skill 发布仓库
git clone https://github.com/canxing/my-skills.git

# 开发完成后，在本仓库中使用
cd agent-skills
npx skills add canxing/my-skills --skill my-awesome-skill
```

## 当前 Skills

| Skill | 来源 | 用途 |
|-------|------|------|
| api-design-principles | wshobson/agents | API 设计原则 |
| cve-vulnerability-analysis | canxing/skills | CVE 漏洞分析 |
| find-skills | vercel-labs/skills | 搜索和发现 skills |
| git-commit | github/awesome-copilot | Git 提交信息生成 |
| prompt-engineering | inference-sh-9/skills | Prompt 工程指南 |

## 注意事项

- `skills-lock.json` 是核心文件，务必提交到 Git
- 本地 `.agents/` 目录由 skills.sh 自动生成，无需提交（已加入 .gitignore）
- Windows 用户建议使用 PowerShell 或 Git Bash 运行上述命令
