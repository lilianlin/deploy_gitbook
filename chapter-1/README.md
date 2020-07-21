# 建立 GitHub 项目
建立用于托管 Gitbook 的项目，并完成项目配置。在 master 分支提交 Gitbook 后，会自动触发 GitHub Actions 完成 Gitbook 的 build，并将 build 结果 部署到 gh-pages 分支。然后通过 GitHub Pages 即可浏览 gh-pages 分支中 Gitbook 中的发布内容。

## 新建 GitHub 项目
略

## 新建 gh-pages branch
将新建的 GitHub 项目 clone 至本地后，执行以下命令：
```shell
git push -f origin gh-pages
```

## 配置 GitHub Pages
进入 GitHub 项目的设置页，在GitHub Pages 设置栏，将 `source` 设为 `gh-pages branch`。

## 配置 Deploy key
本地执行以下命令：
```shell
ssh-keygen -t rsa -b 4096 -C "$(git config user.email)" -f gh-pages -N ""
```
生成一下两个文件：
- gh-pages
- gh-pages.pub

在项目设置的 deploy keys 中添加新的key，并将生成的公钥文件（gh-pages.pub）内容贴入其中。
在项目设置的 secrets 中添加新的key，并将生成的密钥文件（gh-pages）内容贴入其中，密钥名设为 `ACTIONS_DEPLOY_KEY`。

## 配置 Actions
新建 workflow，配置文件内容如下：
```yaml
name: 'deploy website and ebooks'

on:
  push:
    branches:
      - master

jobs:
  job_deploy_website:
    name: 'deploy website'
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - uses: actions/setup-node@v1
      with:
        node-version: '10.x'
    - name: 'Installing gitbook cli'
      run: npm install -g gitbook-cli
    - name: 'Generating distributable files'
      run:  |
        mkdir -p ./docs
        gitbook build ./ ./docs
    - uses: peaceiris/actions-gh-pages@v2.5.0
      env:
        ACTIONS_DEPLOY_KEY: ${{ secrets.ACTIONS_DEPLOY_KEY }}
        allow_empty_commit: true
        enable_jekyll: true
        PUBLISH_BRANCH: gh-pages
        PUBLISH_DIR: ./docs
```
