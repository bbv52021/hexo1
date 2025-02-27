---
abbrlink: ''
categories:
- - 个人网站
comments: null
copyright: null
cover: null
date: '2025-02-27T19:45:28.033970+08:00'
mermaid: false
sponsor: null
sticky: false
tags:
- Git Hook
title: 实现每次修改完本地的 Hexo 后自动推送到远程 main 分支
updated: '2025-02-27T19:45:29.853+08:00'
---
### **实现每次修改完本地的 Hexo 后自动推送到远程 main 分支**

#### **方法 1：使用 Git Hook（本地自动化）**

Git 提供了 Hook 功能，可以在特定事件（如提交）发生时自动执行脚本。你可以利用这个功能，在每次提交后自动推送到远程仓库。

---

#### **步骤 1：创建 Git Hook 脚本**

1. 进入 Hexo 项目的 `.git/hooks` 目录：
   bash

   复制

   ```
   cd /volume1/docker/hexo1/.git/hooks
   ```
2. 创建一个 `post-commit` 钩子脚本：
   bash

   复制

   ```
   vi post-commit
   ```
3. 在脚本中添加以下内容：
   bash

   复制

   ```
   #!/bin/sh
   # 自动推送到远程 main 分支
   git push origin main
   ```
4. 保存并退出。
5. 赋予脚本执行权限：
   bash

   复制

   ```
   chmod +x post-commit
   ```

---

#### **步骤 2：测试自动推送**

1. 在 Hexo 项目中修改文件并提交：
   bash

   复制

   ```
   git add .
   git commit -m "测试自动推送"
   ```
2. 提交后，Git 会自动执行 `post-commit` 钩子脚本，将更改推送到远程 `main` 分支。

---

#### **注意事项**

1. **确保远程仓库已配置**：
   * 在运行脚本之前，确保本地仓库已正确配置远程仓库：
     bash

     复制

     ```
     git remote -v
     ```
   * 如果未配置远程仓库，可以使用以下命令添加：
     bash

     复制

     ```
     git remote add origin https://github.com/bbv52021/hexo1.git
     ```
2. **Git Hook 的局限性**：
   * Git Hook 是本地脚本，仅在本地生效。
   * 如果你在多台设备上工作，需要在每台设备上配置相同的 Hook 脚本。
3. **避免无限循环**：
   * 如果 `post-commit` 脚本中包含了提交操作（如 `git commit`），可能会导致无限循环。确保脚本仅包含推送操作。

---

### **总结**

通过配置 `post-commit` Git Hook，你可以在本地修改文件并提交后，自动将更改推送到远程 `main` 分支，而无需手动输入命令。

按照以上步骤操作，即可实现本地修改后自动推送的功能。如果仍有问题，请随时告诉我！
