# 将本地项目推送到GitHub远程仓库 - 详细步骤

## 前置准备

### 1. 配置Git用户信息（如果还没配置）

```powershell
# 配置用户名（替换为你的真实姓名）
git config --global user.name "你的姓名"

# 配置邮箱（替换为你的真实邮箱，建议与GitHub注册邮箱一致）
git config --global user.email "your.email@example.com"

# 验证配置
git config --global user.name
git config --global user.email
```

### 2. 获取GitHub仓库地址

在GitHub仓库页面，点击"Code"按钮，选择以下地址之一：
- **HTTPS地址**：`https://github.com/用户名/仓库名.git`（推荐新手使用）
- **SSH地址**：`git@github.com:用户名/仓库名.git`（需要配置SSH密钥）

---

## 推送步骤

### 方案一：首次推送（推荐）

#### 步骤1：确认当前状态
```powershell
# 查看当前Git状态
git status

# 确认是否有未提交的文件
# 如果显示 "nothing added to commit but untracked files present"
# 说明文件已添加但未提交
```

#### 步骤2：配置Git用户信息（如果提交失败）
```powershell
# 配置全局用户信息
git config --global user.name "你的姓名"
git config --global user.email "your.email@example.com"

# 或者只为当前仓库配置（去掉--global）
git config user.name "你的姓名"
git config user.email "your.email@example.com"
```

#### 步骤3：提交所有文件
```powershell
# 确保所有文件已添加到暂存区
git add .

# 提交到本地仓库
git commit -m "初始化项目结构：创建完整的目录和文件框架

- 创建后端目录结构（114个文件）
- 创建前端uni-app目录结构（84个文件）
- 创建前端HTML版本目录结构（27个文件）
- 创建项目文档目录结构（18个文件）
- 创建部署配置目录结构（21个文件）
- 创建测试相关目录结构（13个文件）
- 创建资源目录结构（16个文件）
- 创建GitHub配置和项目根文件（18个文件）
- 总计311个空文件，符合项目规范"

# 查看提交历史（确认提交成功）
git log --oneline
```

#### 步骤4：添加远程仓库
```powershell
# 添加远程仓库（替换为你的实际仓库地址）
git remote add origin https://github.com/你的用户名/nursing-platform.git

# 验证远程仓库是否添加成功
git remote -v

# 应该显示：
# origin  https://github.com/你的用户名/nursing-platform.git (fetch)
# origin  https://github.com/你的用户名/nursing-platform.git (push)
```

#### 步骤5：推送到GitHub
```powershell
# 推送到远程仓库的main分支
git push -u origin main

# 如果远程分支是master，使用：
# git push -u origin master
```

---

### 方案二：处理远程仓库有初始文件的情况

如果GitHub仓库创建时勾选了"Add a README file"，远程仓库已有初始提交：

```powershell
# 方法1：拉取远程文件并合并
git pull origin main --allow-unrelated-histories

# 如果有冲突，手动解决后：
git add .
git commit -m "合并远程仓库文件"

# 然后推送
git push -u origin main

# 方法2：强制推送（会覆盖远程仓库的README，慎用！）
# git push -u origin main --force
```

---

## 完整推送流程（复制粘贴版）

```powershell
# 1. 配置用户信息
git config --global user.name "你的姓名"
git config --global user.email "your.email@example.com"

# 2. 添加所有文件
git add .

# 3. 提交到本地仓库
git commit -m "初始化项目结构"

# 4. 添加远程仓库（替换为你的实际地址）
git remote add origin https://github.com/你的用户名/nursing-platform.git

# 5. 推送到GitHub
git push -u origin main
```

---

## 认证方式

### HTTPS方式（推荐新手）

#### 方法1：使用个人访问令牌（推荐）

1. **创建GitHub个人访问令牌**
   - 登录GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
   - 点击 "Generate new token"
   - 设置权限：勾选 `repo`（完整仓库访问权限）
   - 点击 "Generate token"
   - **复制令牌**（只显示一次，务必保存）

2. **推送时使用令牌**
   ```powershell
   # 第一次推送时会提示输入用户名和密码
   # Username: 输入你的GitHub用户名
   # Password: 输入刚才生成的个人访问令牌（不是GitHub密码）
   ```

3. **保存凭证（避免每次输入）**
   ```powershell
   # Windows自动保存凭证
   git config --global credential.helper wincred

   # 或使用Git Credential Manager
   git config --global credential.helper manager
   ```

#### 方法2：在URL中包含令牌（不推荐，不安全）
```powershell
# 格式：https://用户名:令牌@github.com/用户名/仓库名.git
git remote set-url origin https://用户名:令牌@github.com/用户名/nursing-platform.git
```

### SSH方式（推荐熟练用户）

#### 生成SSH密钥
```powershell
# 生成SSH密钥（邮箱替换为你的GitHub邮箱）
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"

# 按Enter使用默认路径，设置密码（可选）

# 启动SSH代理
eval "$(ssh-agent -s)"

# 添加SSH密钥到代理
ssh-add ~/.ssh/id_rsa

# 查看公钥内容
cat ~/.ssh/id_rsa.pub
# 或在Windows上：
type $env:USERPROFILE\.ssh\id_rsa.pub
```

#### 添加SSH密钥到GitHub
1. 复制公钥内容（从 `ssh-rsa` 开始到邮箱结束）
2. 登录GitHub → Settings → SSH and GPG keys → New SSH key
3. 粘贴公钥内容，保存

#### 使用SSH地址推送
```powershell
# 添加远程仓库（使用SSH地址）
git remote add origin git@github.com:用户名/nursing-platform.git

# 或修改已有远程仓库地址
git remote set-url origin git@github.com:用户名/nursing-platform.git

# 推送
git push -u origin main
```

---

## 验证推送成功

### 命令行验证
```powershell
# 查看远程仓库状态
git remote -v

# 查看分支跟踪情况
git branch -vv

# 查看最近的提交
git log --oneline -5
```

### GitHub网页验证
1. 访问你的GitHub仓库页面
2. 查看文件列表是否显示所有项目文件
3. 查看提交历史是否有刚才的提交
4. 确认文件数量和内容

---

## 常见问题解决

### 问题1：推送被拒绝（remote rejected）
```powershell
# 错误信息：
# ! [rejected] main -> main (fetch first)

# 解决方法1：拉取并合并
git pull origin main --allow-unrelated-histories
git push -u origin main

# 解决方法2：强制推送（会覆盖远程内容，慎用！）
git push -u origin main --force
```

### 问题2：认证失败
```powershell
# 错误信息：
# Authentication failed for...

# 解决方法：
# 1. 确保使用的是个人访问令牌，不是GitHub密码
# 2. 检查令牌权限是否包含repo
# 3. 重新生成令牌并保存
```

### 问题3：远程仓库已存在
```powershell
# 错误信息：
# remote origin already exists

# 解决方法：
# 移除旧的远程仓库
git remote remove origin

# 重新添加新的远程仓库
git remote add origin https://github.com/用户名/nursing-platform.git
```

### 问题4：推送时提示输入密码
```powershell
# HTTPS方式推送时会提示：
# Username for 'https://github.com': 输入GitHub用户名
# Password for 'https://用户名@github.com': 输入个人访问令牌

# 保存凭证避免重复输入：
git config --global credential.helper manager
```

---

## 推送后操作

### 1. 邀请团队成员
1. 进入仓库页面 → Settings → Collaborators
2. 点击 "Add people"
3. 输入团队成员的用户名或邮箱
4. 选择权限等级（Write/Read）

### 2. 设置分支保护
1. Settings → Branches → Add rule
2. 设置main分支保护规则：
   - Require pull request reviews
   - Require status checks

### 3. 创建开发分支
```powershell
# 创建develop分支
git checkout -b develop

# 推送develop分支到远程
git push -u origin develop
```

---

## 下次推送流程

以后有新的提交时，使用以下流程：

```powershell
# 1. 查看修改
git status

# 2. 添加修改的文件
git add .

# 3. 提交
git commit -m "提交说明"

# 4. 推送
git push

# 或使用简化流程：
git add . && git commit -m "提交说明" && git push
```

---

## 项目特定推送建议

根据你的项目结构，建议按以下方式推送：

```powershell
# 首次完整推送
git add .
git commit -m "feat: 初始化项目结构

- 创建后端Spring Boot项目框架
- 创建前端uni-app和HTML版本框架
- 添加完整的部署和测试配置
- 总计313个文件，符合项目规范"

git push -u origin main

# 后续按模块推送示例
# 后端开发
git add backend/
git commit -m "feat: 实现后端API接口"
git push

# 前端开发
git add frontend/uni-app/pages/auth/
git commit -m "feat: 实现登录注册功能"
git push
```

---

## 需要帮助？

如果遇到问题，请提供：
1. 错误信息的完整截图或文本
2. 执行的命令
3. GitHub仓库地址

我会帮你解决！