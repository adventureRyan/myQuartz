---
title: "quartz配置"
source: "https://wujyuhin.github.io/blog/02-Learn/01-Config/quartz%E9%85%8D%E7%BD%AE"
author:
published:
created: 2025-08-04
description: "环境配置 一、配置 quartz 步骤 0. 先决条件 在继续之前，您需要安装以下软件Node.js、Git、Obsidian，下载地址直接点链接即可。 安装的攻略如下： NodeJS (v 20.16+)：nodejs配置 Git：git快速配置 Obsidian：不用特别配置，下载安装即可。obsidian 步骤 1：下载并安装 quartz 打开终端并运行以下命令 输入 cd 你的文件夹路径 进入该文件夹 输入 git clone github.com/jackyzha0/quartz.git 将 quartz 仓库克隆到本地 输入 cd: 你的文件夹路径/quartz 进入 quartz 文件夹 输入 npm config set registry registry.npmmirror.com 添加国内镜像加速 输入 npm i(出现以下npm fund提示没关系，因为有些功能需要赞助，不用管) 输入 npx quartz create创建新的 quartz 项目 步骤 2：设置 github 仓库 Github 上完成： 在 github 上新建仓库，不要使用 README，许可证或 gitignore 文件初始化新仓库。 在 github 快速设置(quick setup) 上复制远程仓库 url：github.com/<user>/<repository>.git 本人复制的 HTTPS 链接为 github.com/wujyuhin/blog.git 在 quartz 目录 cmd 终端中运行以下命令 输入 git remote -v 显示被跟踪的远程仓库 origin github.com/jackyzha0/quartz.git(fetch) origin github.com/jackyzha0/quartz.git(push) upstream github.com/jackyzha0/quartz.git(fetch) upstream github.com/jackyzha0/quartz.git (push) 输入 git remote set-url origin <RUL> 本人输入 git remote set-url origin github.com/wujyuhin/blog.git 修改 origin 远程仓库替换为自己的 URL 输入 npx quartz sync --no-pull 将本地仓库所作的更改推送到远程仓库上 末尾带绿色的 Done！ 如果之前没有绑定 git 和 github 的关系，他会弹出网页让你绑定 步骤 3 obsidian 笔记库建立和更新 在 Obsidian 中将 quartz 目录中的 content 文件夹作为 Obsidian 笔记库打开，然后按照以往的习惯写笔记 index.md 是网站首页，不要删除。 输入 npx quartz sync 将更改后的笔记推送到远程仓库上 步骤 4 设置 Github Action 自动部署 Github Pages 在本地 quartz 中按以下路径创建新文件，并保存以下代码内容 quartz/.github/workflows/deploy.yml 前往 github 仓库，点击 Settings>Pages>Source 下拉菜单，选择 Github Actions 最后提交更改，网站将部署到 <github-username>.github.io/<repository-names>，pages 页面会有以下提示 Your site is live at insile.github.io/my- notes/ name: Deploy Quartz site to GitHub Pages on: push: branches: - v4 permissions: contents: read pages: write id-token: write concurrency: group: \"pages\" cancel-in-progress: false jobs: build: runs-on: ubuntu-22.04 steps: - uses: actions/checkout@v4 with: fetch-depth: 0 # Fetch all history for git info - uses: actions/setup-node@v4 with: node-version: 22 - name: Install Dependencies run: npm ci - name: Build Quartz run: npx quartz build - name: Upload artifact uses: actions/upload-pages-artifact@v3 with: path: public deploy: needs: build environment: name: github-pages url: ${{ steps.deployment.outputs.page_url }} runs-on: ubuntu-latest steps: - name: Deploy to GitHub Pages id: deployment uses: actions/deploy-pages@v4 引用使用 Quartz 4.0 和 GitHub Pages 发布托管 Obsidian 笔记 二、可能出现的 bug Github 仓库克隆到本地可能报错，需要将 https 端口跳到 7890，然后打开本地代理，翻墙和不翻墙都试一下 刚刚部署完后的笔记查看不了，最好写一些内容丰富的笔记，然后再打开即可 如果加入 gitignore 没有反应，可以先清楚目录缓存后再提交 清楚缓存 git rm -r --cached ."
tags:
  - "clippings"
---
## 一、配置 quartz

## 步骤 0. 先决条件

- 在继续之前，您需要安装以下软件 [Node.js](https://nodejs.org/en/about/previous-releases) 、 [Git](https://git-scm.com/) 、 [Obsidian](https://obsidian.md/) ，下载地址直接点链接即可。
- 安装的攻略如下：
	- NodeJS (v 20.16+)： [nodejs配置](https://wujyuhin.github.io/blog/02-Learn/01-Config/nodejs%E9%85%8D%E7%BD%AE)
	- Git： [git快速配置](https://wujyuhin.github.io/blog/02-Learn/01-Config/git%E5%BF%AB%E9%80%9F%E9%85%8D%E7%BD%AE)
	- Obsidian：不用特别配置，下载安装即可。 [obsidian](https://wujyuhin.github.io/blog/02-Learn/02-App/obsidian)

## 步骤 1：下载并安装 quartz

- 打开终端并运行以下命令
	- 输入 `cd 你的文件夹路径` 进入该文件夹
	- 输入 `git clone https://github.com/jackyzha0/quartz.git` 将 quartz 仓库克隆到本地
	- 输入 `cd: 你的文件夹路径/quartz` 进入 quartz 文件夹
	- 输入 `npm config set registry https://registry.npmmirror.com` 添加国内镜像加速
	- 输入 `npm i` (出现以下 `npm fund` 提示没关系，因为有些功能需要赞助，不用管)
	- 输入 `npx quartz create` 创建新的 quartz 项目

## 步骤 2：设置 github 仓库

- Github 上完成：
	- 在 github 上新建仓库，不要使用 README，许可证或 gitignore 文件初始化新仓库。
	- 在 github 快速设置(quick setup) 上复制远程仓库 url： `https://github.com/<user>/<repository>.git`
		- 本人复制的 HTTPS 链接为 `https://github.com/wujyuhin/blog.git`
- 在 quartz 目录 cmd 终端中运行以下命令
	- 输入 `git remote -v`
		- 显示被跟踪的远程仓库
		- `origin https://github.com/jackyzha0/quartz.git(fetch)`
		- `origin https://github.com/jackyzha0/quartz.git(push)`
		- `upstream https://github.com/jackyzha0/quartz.git(fetch)`
		- `upstream https://github.com/jackyzha0/quartz.git (push)`
	- 输入 `git remote set-url origin <RUL>`
		- 本人输入 `git remote set-url origin https://github.com/wujyuhin/blog.git`
		- 修改 origin 远程仓库替换为自己的 URL
	- 输入 `npx quartz sync --no-pull`
		- 将本地仓库所作的更改推送到远程仓库上
		- 末尾带绿色的 Done！
		- 如果之前没有绑定 git 和 github 的关系，他会弹出网页让你绑定

## 步骤 3 obsidian 笔记库建立和更新

- 在 Obsidian 中将 quartz 目录中的 `content` 文件夹作为 Obsidian 笔记库打开，然后按照以往的习惯写笔记
	- ![](https://wujyuhin.github.io/blog/Image/Pasted-image-20240918104733.png)
- `index.md` 是网站首页，不要删除。
- 输入 `npx quartz sync` 将更改后的笔记推送到远程仓库上

## 步骤 4 设置 Github Action 自动部署 Github Pages

- 在本地 quartz 中按以下路径创建新文件，并保存以下代码内容
	- `quartz/.github/workflows/deploy.yml`
- 前往 github 仓库，点击 Settings>Pages>Source 下拉菜单，选择 Github Actions
- 最后提交更改，网站将部署到 `<github-username>.github.io/<repository-names>` ，pages 页面会有以下提示 `Your site is live at https://insile.github.io/my- notes/`
```python
name: Deploy Quartz site to GitHub Pages

 

on:

  push:

    branches:

      - v4

 

permissions:

  contents: read

  pages: write

  id-token: write

 

concurrency:

  group: "pages"

  cancel-in-progress: false

 

jobs:

  build:

    runs-on: ubuntu-22.04

    steps:

      - uses: actions/checkout@v4

        with:

          fetch-depth: 0 # Fetch all history for git info

      - uses: actions/setup-node@v4

        with:

          node-version: 22

      - name: Install Dependencies

        run: npm ci

      - name: Build Quartz

        run: npx quartz build

      - name: Upload artifact

        uses: actions/upload-pages-artifact@v3

        with:

          path: public

 

  deploy:

    needs: build

    environment:

      name: github-pages

      url: ${{ steps.deployment.outputs.page_url }}

    runs-on: ubuntu-latest

    steps:

      - name: Deploy to GitHub Pages

        id: deployment

        uses: actions/deploy-pages@v4
```

引用 [使用 Quartz 4.0 和 GitHub Pages 发布托管 Obsidian 笔记](https://insile.github.io/my-notes/%E7%AC%94%E8%AE%B0/Text/%E4%BD%BF%E7%94%A8-Quartz-4.0-%E5%92%8C-GitHub-Pages-%E5%8F%91%E5%B8%83%E6%89%98%E7%AE%A1-Obsidian-%E7%AC%94%E8%AE%B0)

## 二、可能出现的 bug

- Github 仓库克隆到本地可能报错，需要将 https 端口跳到 7890，然后打开本地代理，翻墙和不翻墙都试一下
- 刚刚部署完后的笔记查看不了，最好写一些内容丰富的笔记，然后再打开即可
- 如果加入 gitignore 没有反应，可以先清楚目录缓存后再提交
	- 清楚缓存 `git rm -r --cached .`
	- 重新提交 `npx quartz sync`

## 三、Quartz 使用技巧

## 修改页面的元素

![](https://wujyuhin.github.io/blog/Image/Pasted-image-20240823163040.png)

![](https://wujyuhin.github.io/blog/Image/Pasted-image-20240823163102.png) 标题则在此处修改

## 同步问题

### 目标

- 需要将某些笔记部署到 github page 上，完成 blog 更新

### 目前的更新方法

- 由于 blog 由 quartz 写
- quartz 的笔记内容使用 obsidian 管理，记为笔记仓库 1
- 但是我有笔记总仓库，我希望我只在总仓库中写笔记。
- 写完后如果将笔记上传到 blog，就只需要将笔记复制到仓库 2，图床也需要同步到仓库 2

步骤 1：笔记写在主仓库

步骤 2：将需要发表的笔记复制到仓库 2 (一直打开 airexplorer 即可, 随时手动同步)

步骤 3：图床需要同步（一直打开 airexplorer 即可，随时手动同步）

步骤 4：部署(一直打开 git ，路径为 `D:\Attachments\02-study\quartz\quartz` ，输入 `npx quartz sync` 同步)

### 问题：修改后呢

如果想要修改笔记，只能手动再次复制笔记，如果这个笔记需要多次修改没问题

如果忘记了，那笔记一多就忘记哪些修改同步了，哪些修改没同步，出现管理问题

只有一个办法：记住每次修改都需要同步笔记、重新部署

## 如何加入 github 评论

直接看攻略网站 [Comments (jzhao.xyz)](https://quartz.jzhao.xyz/features/comments)

但是问题是我想取消怎么办，直接注释下面代码

![](https://wujyuhin.github.io/blog/Image/Pasted-image-20240825111352.png)

## 如何加入近期笔记

加入以下代码即可，其中

- Title 是标题
- Limit 是显示最近 5 篇
- Showtags 是不显示笔记中的标签

![](https://wujyuhin.github.io/blog/Image/Pasted-image-20240825111552.png)

[git对已经提交过的文件添加到.gitignore\_git已经commit了怎么gitignore-CSDN博客](https://blog.csdn.net/hnjb5873/article/details/108774212)

---