# 01 项目创建与手动部署流程

> 记录日期: 2025-06-29  
> 作者: ChaosRealms-AI

## 概述

本教程记录了从零开始创建 Docusaurus 项目、提交到 Git 仓库并手动部署到 GitHub Pages 的完整流程，包括项目创建、Git 初始化、配置和部署的所有命令行操作。


## 发给Claude Code / Cursor 的Prompt


```
帮我从零创建一个 Docusaurus 项目并部署到 GitHub Pages，让它可以通过公开链接访问。

任务步骤：
第一步：创建项目
- 用 npx create-docusaurus@latest [项目名] classic 创建项目
- 进入项目目录，确认能正常启动

第二步：Git 初始化
- 初始化 git 仓库
- 添加所有文件并提交
- 连接到 GitHub 远程仓库并推送

第三步：配置 GitHub Pages（这一步需要提醒用户操作）
- 修改 docusaurus.config.js，设置正确的 url 和 baseUrl
- 运行 npm run build 构建项目
- 提交配置更改

第四步：手动部署
- 创建 gh-pages 分支
- 把 build 目录的文件复制到根目录
- 提交并推送 gh-pages 分支
- 切换回 main 分支

第五步：验证
- 在 GitHub 仓库设置中启用 Pages（源设置为 gh-pages 分支）
- 等几分钟后访问网站链接确认部署成功
- 发送部署后的链接给我

要求：
- 链接可以正常访问
- 及时询问不了解的信息，如项目名等等
```

---

## 🎯 跟着开发日志走完，您将实现：


✅ **从零创建 Docusaurus 项目**
- 一个完整的 Docusaurus 文档网站项目
- 包含默认主题和基础页面结构
- 本地开发环境正常运行

✅ **支持公开链接访问**
- 网站成功部署到 GitHub Pages
- 通过公网 URL 随时访问：`https://chaosrealms-ai.github.io/build-your-own-x-by-VibeCoding/`
- 支持 HTTPS 安全访问

✅ **完整的版本控制**
- Git 仓库正确初始化
- 代码托管在 GitHub 上
- 掌握手动部署流程

## 前置条件

- Node.js (v18+)
- npm 或 yarn
- Git
- GitHub 账户

## 1. 创建 Docusaurus 项目

### 1.1 创建新项目
```bash
# 进入项目目录
cd /path/to/your/projects

# 使用 npx 创建 Docusaurus 项目
npx create-docusaurus@latest build-your-own-x-by-VibeCoding classic

# 选择 JavaScript 或 TypeScript（根据提示选择）
```

### 1.2 进入项目目录
```bash
cd build-your-own-x-by-VibeCoding
```

## 2. Git 仓库初始化

### 2.1 初始化 Git 仓库
```bash
# 初始化 git 仓库
git init

# 添加所有文件
git add .

# 提交初始版本
git commit -m "first commit"

# 设置主分支名称
git branch -M main
```

### 2.2 连接 GitHub 远程仓库
```bash
# 添加远程仓库地址
git remote add origin https://github.com/ChaosRealms-AI/build-your-own-x-by-VibeCoding.git

# 推送到 GitHub
git push -u origin main
```

## 3. 配置 GitHub Pages 部署

### 3.1 修改 Docusaurus 配置
编辑 `docusaurus.config.js` 文件，更新以下配置：

```javascript
const config = {
  // ... 其他配置

  // 设置生产环境 URL
  url: 'https://chaosrealms-ai.github.io',
  
  // 设置 baseUrl，通常是项目名称
  baseUrl: '/build-your-own-x-by-VibeCoding/',

  // GitHub Pages 部署配置
  organizationName: 'ChaosRealms-AI', // GitHub 用户名或组织名
  projectName: 'build-your-own-x-by-VibeCoding', // 仓库名称

  // ... 其他配置
};
```

### 3.2 构建项目
```bash
# 构建静态文件
npm run build
```

### 3.3 提交配置更改
```bash
# 添加更改
git add .

# 提交配置更改
git commit -m "Configure GitHub Pages deployment"

# 推送到 GitHub
git push origin main
```

## 4. 手动部署到 GitHub Pages

由于 SSH 配置问题，我们使用手动方式部署：

### 4.1 创建并切换到 gh-pages 分支
```bash
# 创建并切换到 gh-pages 分支
git checkout -b gh-pages
```

### 4.2 复制构建文件到根目录
```bash
# 复制 build 目录下的所有文件到根目录
cp -r build/* .
```

### 4.3 提交并推送 gh-pages 分支
```bash
# 添加所有文件
git add .

# 提交部署文件
git commit -m "Deploy to GitHub Pages"

# 强制推送到 gh-pages 分支
git push origin gh-pages --force
```

### 4.4 切换回主分支
```bash
# 切换回 main 分支
git checkout main
```

## 5. 验证部署

1. 访问 GitHub 仓库设置页面：`https://github.com/ChaosRealms-AI/build-your-own-x-by-VibeCoding/settings/pages`
2. 确认 GitHub Pages 已启用，源分支设置为 `gh-pages`
3. 等待几分钟后访问部署地址：`https://chaosrealms-ai.github.io/build-your-own-x-by-VibeCoding/`

## 6. 后续更新流程

当需要更新网站内容时：

```bash
# 1. 在 main 分支上进行开发
git checkout main

# 2. 修改内容后提交
git add .
git commit -m "Update content"
git push origin main

# 3. 构建新版本
npm run build

# 4. 切换到 gh-pages 分支
git checkout gh-pages

# 5. 复制新的构建文件
cp -r build/* .

# 6. 提交并推送
git add .
git commit -m "Deploy updated content"
git push origin gh-pages --force

# 7. 切换回 main 分支
git checkout main
```

## 常见问题解决

### 问题 1: SSH 权限错误
**错误信息**: `Host key verification failed`

**解决方案**: 使用 HTTPS 方式推送，或配置 SSH 密钥。

### 问题 2: 自动部署失败
**错误信息**: `Please set the GIT_USER environment variable`

**解决方案**: 使用手动部署方式，如本教程所示。

### 问题 3: 页面 404 错误
**检查项**:
- 确认 GitHub Pages 已启用
- 确认源分支设置正确（gh-pages）
- 确认 baseUrl 配置正确

## 总结

通过以上步骤，我们成功将 Docusaurus 项目部署到了 GitHub Pages。关键点包括：

1. 正确配置 `docusaurus.config.js` 中的 URL 和 baseUrl
2. 使用手动方式创建和维护 gh-pages 分支
3. 定期更新部署内容的工作流程

部署完成后，网站将在 `https://chaosrealms-ai.github.io/build-your-own-x-by-VibeCoding/` 地址可访问。