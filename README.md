# iyangming 的个人博客

基于 **Hugo** 静态网站生成器构建，部署在 **GitHub Pages** 上。

## 🌐 访问地址

https://iyangming.github.io

## ✨ 技术栈

- **静态生成器**: [Hugo](https://gohugo.io/) (v0.147.7)
- **主题**: [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke)
- **CSS 框架**: Tachyons
- **部署平台**: GitHub Pages
- **CI/CD**: GitHub Actions (自动构建和部署)

## 📂 项目结构

```
iyangming.github.io/
├── content/          # 博客文章源码（Markdown）
├── static/           # 静态资源
├── layouts/          # 自定义布局
├── config.toml       # Hugo 配置文件
└── public/           # 构建输出目录
```

## 🚀 本地开发

```bash
# 安装 Hugo
brew install hugo

# 启动开发服务器
hugo server -D

# 访问 http://localhost:1313
```

## 📝 撰写博客

```bash
# 创建新文章
hugo new posts/my-new-post.md

# 编辑 content/posts/my-new-post.md
# 添加你的内容...

# 构建静态文件
hugo
```

## 🔧 配置

主要配置文件：`hugo.toml` 或 `config.toml`

关键配置项：
- `baseURL`: 网站基础 URL
- `title`: 网站标题
- `theme`: 使用的主题

## 📊 内容分类

- **技术分享**: AI 智能体、企业数字化
- **项目展示**: 个人项目和实践案例
- **学习笔记**: 技术学习和思考

## 🔗 相关链接

- **作品集**: [iyangjialin.github.io](https://iyangjialin.github.io) - Vibe Coding 作品展示
- **GitHub**: [@iyangming](https://github.com/iyangming)

## 📄 License

本项目采用 MIT License 开源。

---

**最后更新**: 2026-05-13
