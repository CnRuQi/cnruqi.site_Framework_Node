# 🌸 cnruqi.site - Node.js 版本

> ✨ 披花沐雪博客系统 | Express.js + SQLite | 玻璃拟态设计

---

## 📖 项目简介

这是披花沐雪博客系统的 Node.js 版本，使用 Express.js 框架和 SQLite 数据库重构自原来的 PHP 版本。

---

## ✨ 核心特性

| 特性 | 说明 |
|------|------|
| 🎨 **玻璃拟态设计** | 半透明背景 + 模糊效果，现代化视觉层次 |
| 📱 **响应式布局** | 移动端友好，卡片式网格布局 |
| 📝 **文章管理** | 支持增删改查、文章置顶 |
| 🎬 **平滑过渡动画** | 页面淡入淡出，滚动位置记忆 |
| 🔐 **后台管理系统** | 完整的管理面板 |
| 👤 **用户认证** | 安全登录机制 (bcrypt + Session) |
| 🛡️ **安全防护** | XSS防护、CSRF令牌、Session超时 |

---

## 🚀 快速部署

### 📋 环境要求

| 环境 | 版本 |
|------|------|
| 🟢 Node.js | 16.0+ (推荐 18.0+) |
| 📦 npm | 8.0+ |

---

### 🛠️ 部署步骤

#### 步骤 1️⃣：安装依赖

```bash
cd cnruqi_site_node
npm install
```

#### 步骤 2️⃣：初始化数据库

```bash
npm run init-db
```

这将创建数据库表并生成默认管理员账号：
- 用户名: `admin`
- 密码: `admin123`

> ⚠️ **请务必在首次登录后修改默认密码！**

#### 步骤 3️⃣：启动服务器

```bash
# 开发模式
npm run dev

# 或生产模式
npm start
```

服务器默认运行在 http://localhost:3000

---

## 📁 目录结构

```
cnruqi_site_node/
├── src/
│   ├── app.js                 # 主应用入口
│   ├── config/
│   │   └── db.js              # 数据库配置
│   ├── routes/
│   │   ├── index.js           # 前台路由
│   │   ├── login.js           # 登录路由
│   │   └── admin.js           # 后台管理路由
│   ├── utils/
│   │   └── security.js        # 安全模块
│   └── scripts/
│       └── init-db.js         # 数据库初始化脚本
├── public/
│   ├── css/
│   │   └── style.css          # 样式文件
│   ├── index.html             # 首页模板
│   ├── post.html              # 文章详情模板
│   ├── login.html             # 登录模板
│   ├── 404.html               # 404模板
│   └── admin/                 # 后台模板
│       ├── index.html
│       ├── add.html
│       └── edit.html
├── data/                      # SQLite数据库目录
├── logs/                      # 日志目录
├── package.json
├── .env.example
└── README.md
```

---

## 📝 使用说明

### ➕ 发布文章
1. 访问登录页面，使用管理员账号登录
2. 点击「后台」进入管理面板
3. 点击「+ 写文章」按钮
4. 填写标题、简介、正文内容
5. 可选：添加封面图片 URL
6. 可选：设置优先度 (0-100)
7. 点击「发布」按钮

### ✏️ 管理文章
| 操作 | 说明 |
|------|------|
| 📄 查看 | 后台文章列表显示所有文章 |
| ✏️ 编辑 | 点击文章右侧的「编辑」链接 |
| 🗑️ 删除 | 点击文章右侧的「删除」链接 |
| 📌 置顶 | 在发布/编辑时设置优先度 |

---

## 🔒 安全建议

> ⚡ 部署完成后请务必执行以下操作！

- [ ] 🔑 **立即修改默认密码**
- [ ] 🛡️ **使用强密码保护**
- [ ] 💾 **定期备份数据库** (`data/cnruqi.db`)
- [ ] ⚙️ **在生产环境修改 `SESSION_SECRET`**

---

## 🛠️ 技术栈

<div align="center">

| 分类 | 技术 |
|------|------|
| 🌐 前端 | HTML5, CSS3, JavaScript, EJS模板 |
| ⚙️ 后端 | Node.js, Express.js, SQLite |
| 🔐 安全 | bcryptjs, csurf, express-session |
| 🎨 设计 | Glassmorphism（玻璃拟态） |

</div>

---

## 许可证

本项目为个人学习项目，可自由使用和修改。

---

<div align="center">

**🌸 披花沐雪** - 记录思维的涟漪

*One Last Kiss for the Beautiful World*

</div>
