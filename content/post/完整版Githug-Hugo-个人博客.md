---
title: "完整版Githug Hugo 个人博客"
date: 2023-06-07T19:55:57+08:00
draft: false
ShowToc: true
TocOpen: true
---

## 🎉 Windown 本地安装 Hugo

### 打开 [Hugo windows installation](https://gohugo.io/installation/windows/) 

### 使用**管理员权限** `winget` 包管理工具安装
```bash
winget install Hugo.Hugo.Extended
```

### 打开 [Git windows installation](https://git-scm.com/download/win)
```bash
winget install --id Git.Git -e --source winget
```


### Hugo 建立新项目
```bash
hugo new site web3-blog
```


### cd 进入项目根目录
```bash
cd web3-blog
```


### 安装 hugo 模板
```bash
git init
git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

### 修改 `hugo.toml` 配置文件
```
baseURL = 'https://「你的Github账号」.github.io/web3-blog/'
languageCode = 'en-us'
title = 'Web3 撸毛日记'
theme = 'PaperMod'

enableEmoji = true # 开启MarkDown表情包解析
```

### 修改文章模版 `achetypes/default.md`
```
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: false
ShowToc: true # 开启 Table Of Content 功能
TocOpen: true # 展开 Table Of Content
---
```

### 发布第一篇文章
```bash
hugo new post/第一篇博文.md
```

### 本地预览网站
```bash
hugo server -D
```

```bash
david@Davids-Mac-mini web-blog % hugo server -D
Start building sites … 
hugo v0.112.4+extended darwin/arm64 BuildDate=unknown

                   | EN  
-------------------+-----
  Pages            | 16  
  Paginator pages  |  0  
  Non-page files   | 10  
  Static files     |  0  
  Processed images |  0  
  Aliases          |  2  
  Sitemaps         |  1  
  Cleaned          |  0  

Built in 95 ms
Watching for changes in /Users/david/Desktop/web-blog/{archetypes,assets,content,data,layouts,static,themes}
Watching for config changes in /Users/david/Desktop/web-blog/hugo.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/web3-blog/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

---

## 🎉 Github pages 绑定 Vscode

### 配置Github SSH链接
```bash
ssh-keygen -t ed25519 -C "你的Github邮箱 your_email@example.com" 
```
> 生成密钥后看提示找到文件 `id_ed25519.pub` 路径
> 
> 使用 `cat ~/.ssh/id_ed25519.pub` 命令读取文件内容填入Github

![](https://raw.githubusercontent.com/davidpythonseo/web3blog/main/content/post/images/sshkey.png)

### 点击创建 *[githug](https://github.com/new)* 新项目

![](https://raw.githubusercontent.com/davidpythonseo/web3blog/main/content/post/images/GithubNewRepository.png)

- 使用SSH链接Github
```bash
echo "# web3-blog" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:davidpythonseo/web3-blog.git
git push -u origin main
```
- Githug 创建分支 `gh-pages`

![](https://raw.githubusercontent.com/davidpythonseo/web3blog/main/content/post/images/gh-pages.png)

- 设置分支读写权限

![](https://raw.githubusercontent.com/davidpythonseo/web3blog/main/content/post/images/分支读写权限.png)

- 写入GitHub Actions脚本
```bash
mkdir -p .github/workflows
touch .github/workflows/deploy.yml
vim .github/workflows/deploy.yml
```
- 填入脚本代码
```bash
name: Publish to GH Pages
on:
  push:
    branches:
      - main
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout source
        uses: actions/checkout@v3
        with:
          submodules: true

      - name: Checkout destination
        uses: actions/checkout@v3
        if: github.ref == 'refs/heads/main'
        with:
          ref: gh-pages
          path: built-site

      - name: Setup Hugo
        run: |
          curl -L -o /tmp/hugo.tar.gz 'https://github.com/gohugoio/hugo/releases/download/v0.110.0/hugo_extended_0.110.0_linux-amd64.tar.gz'
          tar -C ${RUNNER_TEMP} -zxvf /tmp/hugo.tar.gz hugo                    
      - name: Build
        run: ${RUNNER_TEMP}/hugo

      - name: Deploy
        if: github.ref == 'refs/heads/main'
        run: |
          cp -R public/* ${GITHUB_WORKSPACE}/built-site/
          cd ${GITHUB_WORKSPACE}/built-site
          git add .
          git config user.name 'dhij'
          git config user.email 'davidhwang.ij@gmail.com'
          git commit -m 'Updated site'
          git push
```
- 三件套命令

```bash
git add .
git commit -m "更新"
git push
```
---
## 🎉 挂载谷歌网盘

## 🎉 在线更新项目

- `https://vscode.dev/`