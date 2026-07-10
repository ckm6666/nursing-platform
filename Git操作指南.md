

## 前置准备

1. **确保已安装Git**
   - 下载地址: https://git-scm.com/downloads
   - 安装后打开命令行输入 `git --version` 验证

2. **配置Git用户信息**（首次使用需要配置）
   ```bash
   git config --global user.name "你的姓名"
   git config --global user.email "你的邮箱@example.com"
   ```

3. **配置GitHub认证**
   - 生成SSH密钥: `ssh-keygen -t rsa -b 4096 -C "你的邮箱@example.com"`
   - 将公钥添加到GitHub: Settings → SSH and GPG keys → New SSH key

---

## 方案一：推送到新创建的GitHub仓库

### 步骤1：在GitHub上创建仓库

1. 登录GitHub，点击右上角 "+" → "New repository"
2. 填写仓库信息：
   - Repository name: `nursing-platform`
   - Description: `互联网+智慧护理平台`
   - 选择 Private（私有仓库，适合团队开发）
   - ✅ 勾选 "Add a README file"
   - ✅ 勾选 "Add .gitignore" → 选择 "Java"
   - 点击 "Create repository"

### 步骤2：初始化本地Git仓库

在项目根目录 `d:\IDEA JAVA\javaProject\D-nursing-platform` 打开PowerShell或命令行：

```bash
# 初始化Git仓库
git init

# 查看当前状态
git status

# 添加所有文件到暂存区
git add .

# 查看暂存状态
git status

# 提交到本地仓库
git commit -m "初始化项目结构：创建完整的目录和文件框架"

# 查看提交历史
git log --oneline
```

### 步骤3：连接远程仓库并推送

```bash
# 添加远程仓库（替换为你的实际仓库地址）
git remote add origin https://github.com/你的组织名/nursing-platform.git

# 或使用SSH地址（推荐）
git remote add origin git@github.com:你的组织名/nursing-platform.git

# 验证远程仓库
git remote -v

# 推送代码到远程仓库
git push -u origin master

# 或推送到main分支（GitHub新仓库默认）
git push -u origin main
```

---

## 方案二：推送到已存在的GitHub小组仓库

### 步骤1：克隆远程仓库

```bash
# 克隆仓库到本地（替换为实际地址）
git clone https://github.com/你的组织名/nursing-platform.git

# 进入项目目录
cd nursing-platform
```

### 步骤2：复制项目文件

1. 将你创建的所有文件复制到克隆下来的目录
2. 或者在克隆的仓库目录中重新创建文件结构

### 步骤3：推送更新

```bash
# 查看变更
git status

# 添加所有新文件
git add .

# 提交变更
git commit -m "初始化项目结构：创建完整的目录和文件框架"

# 推送到远程
git push origin master
```

---

## 添加团队成员（仓库管理员操作）

### 方法1：添加协作者

1. 进入仓库页面 → Settings → Collaborators
2. 点击 "Add people"
3. 输入团队成员的GitHub用户名或邮箱
4. 选择权限等级：
   - **Write**: 可以推送代码（推荐给开发人员）
   - **Read**: 只能查看代码（推荐给产品或测试）

### 方法2：使用组织（推荐）

1. 创建GitHub组织：
   - 点击右上角 "+" → "New organization"
   - 填写组织名称，如：`nursing-platform-team`

2. 邀请成员加入组织：
   - 进入组织页面 → People → Invite member
   - 批量邀请团队成员

3. 创建团队仓库：
   - 在组织下创建仓库
   - 所有团队成员自动获得访问权限

---

## 团队协作最佳实践

### 分支管理策略

```bash
# 创建并切换到开发分支
git checkout -b develop

# 创建个人功能分支
git checkout -b feature/auth-module      # 人员B：登录注册模块
git checkout -b feature/booking-module    # 人员C：下单预约模块
git checkout -b feature/order-module      # 人员D：订单管理模块

# 推送功能分支到远程
git push origin feature/auth-module
```

### 日常开发流程

```bash
# 1. 拉取最新代码
git pull origin develop

# 2. 创建功能分支
git checkout -b feature/新功能名称

# 3. 开发并提交
git add .
git commit -m "feat: 添加新功能描述"

# 4. 推送功能分支
git push origin feature/新功能名称

# 5. 在GitHub上创建Pull Request（PR）
#    - 进入仓库页面
#    - 点击 "Compare & pull request"
#    - 填写PR描述
#    - 指定审核人员
#    - 点击 "Create pull request"

# 6. 等待代码审核和合并
```

### 提交信息规范

```bash
# 格式：<type>: <subject>

# 常用类型：
feat:     新功能
fix:      修复Bug
docs:     文档更新
style:    代码格式调整
refactor: 代码重构
test:     测试相关
chore:    构建/工具变动

# 示例：
git commit -m "feat: 实现用户登录功能"
git commit -m "fix: 修复订单状态更新问题"
git commit -m "docs: 更新API接口文档"
```

---

## 常见问题解决

### 问题1：推送被拒绝（远程有更新）

```bash
# 拉取远程更新
git pull origin master --rebase

# 解决冲突后提交
git add .
git rebase --continue

# 再次推送
git push origin master
```

### 问题2：忘记切换分支就开发了

```bash
# 保存当前修改到暂存区
git stash

# 切换到正确的分支
git checkout develop

# 恢复修改
git stash pop
```

### 问题3：需要撤销最近的提交

```bash
# 撤销最近一次提交，保留修改
git reset --soft HEAD~1

# 撤销最近一次提交，丢弃修改
git reset --hard HEAD~1
```

---

## 本项目特定的Git操作

### 按人员分工推送代码

```bash
# 人员A - 后端开发
git checkout -b feature/backend-api
# 开发 backend/ 目录下的文件
git add backend/
git commit -m "feat: 实现后端API接口"
git push origin feature/backend-api

# 人员B - 前端用户模块
git checkout -b feature/auth-catalog
# 开发 frontend/uni-app/pages/auth/ 和 catalog/
git add frontend/uni-app/pages/auth/ frontend/uni-app/pages/catalog/
git commit -m "feat: 实现登录注册和服务浏览功能"
git push origin feature/auth-catalog

# 人员C - 前端交易模块
git checkout -b feature/booking-address
# 开发 frontend/uni-app/pages/booking/ 和 address/
git add frontend/uni-app/pages/booking/ frontend/uni-app/pages/address/
git commit -m "feat: 实现下单预约和地址管理功能"
git push origin feature/booking-address

# 人员D - 前端售后模块
git checkout -b feature/order-review-complaint
# 开发 frontend/uni-app/pages/order/、review/、complaint/
git add frontend/uni-app/pages/order/ frontend/uni-app/pages/review/ frontend/uni-app/pages/complaint/
git commit -m "feat: 实现订单管理和评价投诉功能"
git push origin feature/order-review-complaint
```

---

## 验证推送成功

1. 访问你的GitHub仓库页面
2. 检查文件是否都已上传
3. 确认团队成员是否都能访问
4. 测试克隆和推送权限

---

## 需要帮助？

- GitHub官方文档: https://docs.github.com/cn
- Git官方文档: https://git-scm.com/book/zh/v2
- 团队协作问题：联系项目负责人（人员A）
