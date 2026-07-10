# 如何查看Git提交内容

## 方法一：命令行查看

### 1. 查看提交历史
```bash
# 简洁模式查看提交历史
git log --oneline

# 查看详细提交历史
git log

# 查看最近3次提交
git log -3
```

### 2. 查看具体提交内容
```bash
# 查看最近一次提交的详细信息
git log -1 --stat

# 查看最近一次提交的文件列表
git show --name-only HEAD

# 查看提交的完整diff（差异）
git show HEAD

# 查看特定文件的变更
git show HEAD -- backend/src/main/java/com/nursing/NursingApplication.java
```

### 3. 查看文件状态
```bash
# 查看当前工作区状态
git status

# 查看暂存区文件列表
git diff --cached --name-only
```

### 4. 图形化查看提交历史
```bash
# 查看分支图形历史
git log --graph --oneline --all

# 查看更详细的图形历史
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
```

---

## 方法二：IDE中查看

### VS Code

1. **查看Git历史**
   - 点击左侧源代码管理图标（分支图标）
   - 或按快捷键 `Ctrl + Shift + G`

2. **查看提交记录**
   - 点击"提交历史"或"Timeline"
   - 可以看到所有提交记录

3. **查看文件变更**
   - 点击具体文件可以看到diff差异
   - 绿色表示新增，红色表示删除

### IntelliJ IDEA

1. **Git工具窗口**
   - 底部点击"Git"标签
   - 或按 `Alt + 9`

2. **查看提交历史**
   - 在Git工具窗口中点击"Log"标签
   - 可以看到图形化的提交历史

3. **查看文件变更**
   - 右键点击提交 → "Show Diff"
   - 或双击文件查看具体变更

---

## 方法三：Git GUI工具

### GitKraken
1. 打开GitKraken
2. 自动显示提交历史图
3. 点击提交节点查看详细内容

### SourceTree
1. 打开SourceTree
2. 选择仓库
3. 查看提交历史和文件变更

### GitHub Desktop
1. 打开GitHub Desktop
2. 选择仓库
3. 点击"History"查看提交历史
4. 点击提交查看文件变更

---

## 方法四：GitHub网页查看

### 推送到GitHub后查看

1. 登录GitHub仓库页面
2. 点击"Commits"标签
3. 点击具体提交查看：
   - 提交信息
   - 提交者信息
   - 提交时间
   - 文件变更列表
   - 代码差异对比

---

## 常用查看命令总结

```bash
# 查看提交历史（简洁）
git log --oneline

# 查看最近一次提交详情
git log -1 --stat

# 查看提交的文件列表
git show --name-only HEAD

# 查看完整diff
git show HEAD

# 查看特定文件的变更历史
git log --follow -- filename

# 查看谁修改了某文件
git blame filename

# 搜索提交内容
git log -S "搜索内容"
```

---

## 实际操作演示

在你的项目中，已经执行了以下查看命令：

1. `git log --oneline` - 查看提交历史
2. `git log -1 --stat` - 查看最近提交详情
3. `git show --name-only HEAD` - 查看提交的文件列表

你可以随时使用这些命令来查看项目提交内容！

---

## 提示

- 使用 `q` 键退出Git日志查看（在命令行中）
- 使用方向键上下滚动查看更多内容
- 按空格键向下翻页
- 按 `b` 键向上翻页