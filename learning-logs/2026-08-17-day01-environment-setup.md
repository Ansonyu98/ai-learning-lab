# AI Learning Log — Day 01

**日期：2026-08-17**

## 今日目标

搭建以后学习 AI 所需要的基础开发环境，并建立 GitHub 学习仓库。

最终形成：

**本地学习 → Git 版本管理 → GitHub 沉淀学习成果**

---

# 一、今天完成的内容

## 1. 规划开发目录

为了减少 C 盘占用，将开发环境主要放在 D 盘。

建立：

```text
D:\Dev
│
├── Apps
│   ├── Git
│   └── Python
│
├── Projects
│
├── Cache
│   ├── pip
│   └── huggingface
│
├── Models
│
└── Data
```

用途：

- `Apps`：开发软件
- `Projects`：自己的代码和 AI 项目
- `Cache`：开发工具缓存
- `Models`：以后保存 AI 模型
- `Data`：数据集和项目数据

---

# 二、安装 Git

Git 安装位置：

```text
D:\Dev\Apps\Git
```

安装过程中学习了几个重要配置：

### 默认 Branch

设置：

```text
main
```

而不是：

```text
master
```

### PATH

选择：

```text
Git from the command line and also from 3rd-party software
```

这样可以直接在：

- CMD
- PowerShell
- Cursor Terminal

使用 Git。

### SSH

选择：

```text
Use bundled OpenSSH
```

### Git Credential Manager

开启：

```text
Git Credential Manager
```

用于以后 GitHub 登录授权。

安装完成后验证：

```powershell
git --version
where git
```

确认 Git 正常运行，并安装在 D 盘。

---

# 三、安装 Python

Python 安装位置：

```text
D:\Dev\Apps\Python
```

安装时重点开启：

```text
Add Python to environment variables
```

保留：

- pip
- py launcher
- tcl/tk

没有安装不需要的：

- Python test suite
- debugging symbols
- debug binaries

安装完成后验证：

```powershell
python --version
where python
pip --version
where pip
```

确认 Python 位于：

```text
D:\Dev\Apps\Python
```

---

# 四、配置 pip 缓存

将 pip 下载缓存统一放到：

```text
D:\Dev\Cache\pip
```

配置命令：

```powershell
pip config set global.cache-dir "D:\Dev\Cache\pip"
```

检查：

```powershell
pip config list
pip cache dir
```

理解：

> pip Cache 是安装包的下载缓存，可以清理。

它和真正安装好的 Python 库不是一回事。

---

# 五、建立第一个 AI 学习项目

项目位置：

```text
D:\Dev\Projects\ai-learning-lab
```

这是以后整个 AI 学习过程的主仓库。

计划学习：

```text
Prompt Engineering
↓
Python
↓
LLM API
↓
RAG
↓
AI Agent
↓
AI Automation
↓
Deployment
```

---

# 六、学习 Python 虚拟环境 `.venv`

创建：

```powershell
python -m venv .venv
```

位置：

```text
D:\Dev\Projects\ai-learning-lab\.venv
```

今天理解了：

> Python 是“总工具厂”，`.venv` 是每个项目自己的“独立工具箱”。

不同项目可以拥有不同版本的 Python 第三方库，互不干扰。

例如：

```text
Projects
│
├── ai-learning-lab
│   └── .venv
│
└── project-B
    └── .venv
```

在 Cursor 中选择：

```text
Python 3.13.15 ('.venv': venv)
```

并确认：

```powershell
python -c "import sys; print(sys.executable)"
```

指向项目自己的：

```text
D:\Dev\Projects\ai-learning-lab\.venv\Scripts\python.exe
```

---

# 七、配置 Cursor

安装 Microsoft Python 扩展。

使用：

```text
Ctrl + Shift + P
```

选择：

```text
Python: Select Interpreter
```

指定项目：

```text
.venv
```

最终形成：

```text
Cursor
   ↓
ai-learning-lab
   ↓
.venv
   ↓
Python 3.13
```

---

# 八、初始化 Git

进入：

```text
D:\Dev\Projects\ai-learning-lab
```

执行：

```powershell
git init
```

确认默认分支：

```powershell
git branch --show-current
```

结果：

```text
main
```

项目中生成：

```text
.git
```

`.git` 是 Git 保存版本历史的地方。

---

# 九、建立 `.gitignore`

创建：

```text
.gitignore
```

加入：

```gitignore
.venv/
__pycache__/
*.pyc
.env
```

目的：

- `.venv` 不上传 GitHub
- Python 缓存不上传
- `.env` 不上传
- 避免以后 API Key 泄漏

通过：

```powershell
git ls-files
```

确认 `.venv` 没有被 Git 管理。

---

# 十、建立 README

创建：

```text
README.md
```

README 是 GitHub Repository 的项目首页说明。

目前用于记录：

- AI 学习目标
- Learning Roadmap
- 学习模块
- Projects
- 学习方法

---

# 十一、第一次 Git Commit

学习了 Git 最重要的三个动作：

```text
git add
↓
准备把哪些修改保存

git commit
↓
创建一个本地版本快照

git push
↓
上传到 GitHub
```

第一次执行：

```powershell
git add .
git commit -m "Initial commit"
```

同时配置了：

```powershell
git config --global user.name
git config --global user.email
```

完成第一次版本记录：

```text
Initial commit
```

---

# 十二、连接 GitHub

在 GitHub 创建：

```text
ai-learning-lab
```

Repository。

本地连接 GitHub：

```powershell
git remote add origin <GitHub Repository URL>
```

检查：

```powershell
git remote -v
```

理解：

```text
Local Repository
本地 ai-learning-lab

        ↓ origin

Remote Repository
GitHub ai-learning-lab
```

---

# 十三、第一次 Push

执行：

```powershell
git push -u origin main
```

通过 Git Credential Manager 完成 GitHub 授权。

第一次建立：

```text
本地 main
     ↕
GitHub main
```

之后正常情况下只需要：

```powershell
git push
```

即可同步。

---

# 十四、今天掌握的 Git 基础概念

### Repository

项目仓库。

### Local Repository

电脑里的 Git 仓库。

### Remote Repository

GitHub 上的仓库。

### Branch

项目开发分支。

目前使用：

```text
main
```

### Git Status

检查当前项目状态：

```powershell
git status
```

### A

```text
A = Added
```

新文件准备加入 Git。

### M

```text
M = Modified
```

Git 已管理的文件发生修改。

### Commit

一个项目版本的“存档点”。

### Push

把本地 Commit 上传 GitHub。

### Origin

本地 Git 给 GitHub 远程仓库使用的默认简称。

---

# 十五、目前最终环境

```text
D:\Dev
│
├── Apps
│   ├── Git
│   └── Python
│
├── Cache
│   ├── pip
│   └── huggingface
│
├── Models
├── Data
│
└── Projects
    │
    └── ai-learning-lab
        │
        ├── .git
        ├── .venv
        ├── .gitignore
        ├── README.md
        │
        ├── 01-prompt-engineering
        ├── 02-python
        ├── 03-llm-api
        ├── 04-rag
        ├── 05-agent
        ├── 06-automation
        │
        └── projects
```

---

# 十六、今天最重要的工作流

以后每天学习 AI，基本都会重复：

```text
学习
↓
写笔记 / 写代码
↓
做实验
↓
git status
↓
git add
↓
git commit
↓
git push
↓
GitHub 沉淀
```

核心原则：

> Learn → Build → Document → Commit → Share

---

# Day 02 计划

下一次开始正式进入 AI 学习。

第一阶段：

## Prompt Engineering

准备建立：

```text
01-prompt-engineering
│
├── README.md
├── 01-basics
├── 02-zero-shot
├── 03-few-shot
├── 04-structured-output
├── 05-prompt-chaining
├── 06-evaluation
└── exercises
```

下一步目标不是单纯“看 Prompt 课程”，而是形成：

**学习一个 Prompt 知识点 → 写学习笔记 → 做 Prompt 实验 → 对比结果 → Git Commit → GitHub 沉淀。**

最终逐渐形成自己的 Prompt Engineering 学习作品集。