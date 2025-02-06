---

# **Git与GitHub操作指南**
**版本控制与协作开发必备工具**

---

## **目录**
1. Git基础概念
2. Git安装与配置
3. Git日常使用
4. GitHub远程仓库操作
5. 分支管理与协作流程
6. 高级操作与问题处理
7. 常见问题与解决方案

---

## **1. Git基础概念**
### 1.1 什么是Git？
- **分布式版本控制系统**：记录文件变更历史，支持多人协作。
- **核心功能**：代码版本管理、分支合并、冲突解决、历史回溯。

### 1.2 核心术语
- **仓库（Repository）**：存储项目历史和元数据的目录。
- **提交（Commit）**：一次代码变更的快照，包含唯一ID（SHA-1哈希值）。
- **分支（Branch）**：独立开发线，默认主分支为`main`或`master`。
- **远程仓库（Remote）**：托管在服务器（如GitHub）的共享仓库。
- **暂存区（Staging Area）**：提交前临时存放变更的区域。

---

## **2. Git安装与配置**
### 2.1 安装Git
- **Windows**：下载 [Git for Windows](https://git-scm.com/downloads)。
- **Mac**：通过 `brew install git` 或官网安装。
- **Linux**：`sudo apt-get install git`（Debian系）或 `sudo yum install git`（Red Hat系）。

### 2.2 初始配置
```bash
# 设置全局用户名和邮箱（提交时显示身份）
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 启用颜色高亮
git config --global color.ui auto

# 查看配置
git config --list
```

---

## **3. Git日常使用**
### 3.1 创建仓库
```bash
# 初始化新仓库
git init

# 克隆现有仓库
git clone https://github.com/username/repo.git
```

### 3.2 基本操作流程
```bash
# 1. 修改文件后，添加变更到暂存区
git add <file-name>      # 添加单个文件
git add .                # 添加所有变更

# 2. 提交到本地仓库
git commit -m "提交描述"

# 3. 查看状态
git status

# 4. 查看提交历史
git log
```

### 3.3 撤销操作
```bash
# 撤销未暂存的修改（还原到最近一次提交状态）
git checkout -- <file-name>

# 撤销暂存区的文件（保留修改）
git reset HEAD <file-name>

# 修改最后一次提交（未推送时）
git commit --amend -m "新提交信息"
```

---

## **4. GitHub远程仓库操作**
### 4.1 关联远程仓库
```bash
# 添加远程仓库（命名为origin）
git remote add origin https://github.com/username/repo.git

# 查看远程仓库
git remote -v
```

### 4.2 推送与拉取
```bash
# 推送本地分支到远程（首次推送需指定上游分支）
git push -u origin main

# 拉取远程变更（自动合并）
git pull origin main

# 强制推送（谨慎使用！）
git push -f origin main
```

### 4.3 克隆与Fork
- **Clone**：直接复制他人仓库到本地。
- **Fork**：在GitHub上创建个人副本，用于贡献代码（通过Pull Request）。

---

## **5. 分支管理与协作流程**
### 5.1 分支操作
```bash
# 创建新分支
git branch feature-branch

# 切换分支
git checkout feature-branch
# 或（创建并切换）
git checkout -b feature-branch

# 合并分支到当前分支（如main）
git checkout main
git merge feature-branch

# 删除分支
git branch -d feature-branch
```

### 5.2 解决合并冲突
1. 冲突时，Git会在文件中标记冲突位置（`<<<<<<<` 和 `>>>>>>>`）。
2. 手动编辑文件，保留需要的代码。
3. 添加解决后的文件并提交：
   ```bash
   git add <file-name>
   git commit -m "解决合并冲突"
   ```

### 5.3 GitHub协作流程（Pull Request）
1. **Fork仓库**：在GitHub页面点击Fork按钮。
2. **克隆到本地**：`git clone https://github.com/your-username/repo.git`
3. **创建分支**：`git checkout -b fix-bug`
4. **提交修改**并推送：`git push origin fix-bug`
5. **发起Pull Request**：在GitHub仓库页面点击 `New Pull Request`。
6. **审核与合并**：维护者审查代码后合并到主分支。

---

## **6. 高级操作**
### 6.1 储藏临时修改（Stash）
```bash
# 储藏当前未提交的修改
git stash

# 恢复储藏的修改
git stash pop
```

### 6.2 回滚提交
```bash
# 撤销某次提交（生成新提交）
git revert <commit-id>

# 重置到某个提交（谨慎使用！）
git reset --hard <commit-id>   # 丢弃之后的所有变更
git reset --soft <commit-id>   # 保留变更到暂存区
```

### 6.3 标签管理
```bash
# 创建标签（用于版本发布）
git tag v1.0.0

# 推送标签到远程
git push origin --tags
```

---

## **7. 常见问题与解决方案**
### 7.1 提交了错误文件
- 使用 `git reset` 回退提交，或 `git rm --cached <file>` 移除文件。

### 7.2 忘记切换分支直接修改
- 储藏修改（`git stash`），切换分支后恢复（`git stash pop`）。

### 7.3 误删分支
- 通过提交哈希值恢复：`git checkout -b new-branch <commit-id>`。

---

## **附录**
### A. Git命令速查表
| 命令                | 说明                          |
|---------------------|-----------------------------|
| `git init`          | 初始化新仓库                  |
| `git clone <url>`   | 克隆远程仓库                  |
| `git add <file>`    | 添加文件到暂存区              |
| `git commit -m "msg"` | 提交变更                     |
| `git push`          | 推送代码到远程                |
| `git pull`          | 拉取远程变更                  |
| `git branch`        | 查看/管理分支                 |
| `git checkout`      | 切换分支或恢复文件            |
| `git merge`         | 合并分支                      |

### B. 推荐学习资源
- **官方文档**：[Git Book](https://git-scm.com/book/)
- **交互式学习**：[Learn Git Branching](https://learngitbranching.js.org/)
- **GitHub Guides**：[GitHub Guides](https://guides.github.com/)

---
