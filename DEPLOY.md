# 宝塔面板部署指南

## 环境要求

- 宝塔面板 7.0+
- Node.js 版本管理器（可在宝塔软件商店安装）
- Nginx（用于反向代理）

## 部署步骤

### 1. 安装 Node.js

在宝塔面板中：
1. 登录宝塔面板
2. 前往 "软件商店" → "Node.js" → 安装
3. 推荐安装 Node.js 18.x 或 20.x 版本

### 2. 上传项目

1. 将 `cnruqi_site_node` 文件夹压缩打包
2. 通过宝塔文件管理器上传到服务器
3. 解压到 `/www/wwwroot/你的域名/`

### 3. 安装依赖

在终端中执行：
```bash
cd /www/wwwroot/你的域名/cnruqi_site_node
npm install
```

### 4. 初始化数据库

```bash
cd /www/wwwroot/你的域名/cnruqi_site_node
node src/scripts/init-db.js
```

### 5. 配置 Nginx 反向代理

在宝塔面板中：
1. 前往 "网站" → 添加站点
2. 填写你的域名
3. 创建站点后，点击 "设置"
4. 找到 "反向代理" → 添加反向代理
5. 配置：
   - 代理名称：cnruqi
   - 目标URL：http://127.0.0.1:3000
   - 发送域名：$host

或者直接修改 Nginx 配置文件：

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /www/wwwroot/your-domain/cnruqi_site_node/public;
    index index.html;

    # 静态文件
    location / {
        try_files $uri @node;
    }

    # Node.js 反向代理
    location @node {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_cache_bypass $http_upgrade;
    }

    # 静态资源缓存
    location ~* \.(css|js|jpg|jpeg|png|gif|ico|svg|woff|woff2)$ {
        expires 30d;
        add_header Cache-Control "public, immutable";
    }
}
```

### 6. 配置 PM2 进程管理器（推荐）

在宝塔面板中：
1. 前往 "软件商店" → "PM2管理器" → 安装
2. 启动 Node.js 项目：
   - 项目路径：/www/wwwroot/你的域名/cnruqi_site_node
   - 启动文件：src/app.js
   - 项目名称：cnruqi-site

或在终端中：
```bash
cd /www/wwwroot/你的域名/cnruqi_site_node
pm2 start src/app.js --name cnruqi-site
pm2 save
pm2 startup
```

### 7. 配置环境变量

在服务器上创建 `.env` 文件：
```bash
cd /www/wwwroot/你的域名/cnruqi_site_node
cp .env.example .env
nano .env
```

修改配置：
```env
PORT=3000
NODE_ENV=production
SESSION_SECRET=随机密钥字符串
DB_PATH=./data/cnruqi.db
```

### 8. 重启服务

```bash
# 如果使用 PM2
pm2 restart cnruqi-site

# 如果直接运行
npm start
```

## 访问网站

- 前台：http://your-domain.com
- 后台：http://your-domain.com/login
- 默认管理员：admin / admin123

## 常见问题

### 1. 端口被占用
```bash
# 查看端口占用
lsof -i:3000
# 杀掉进程
kill -9 <PID>
```

### 2. 数据库权限问题
```bash
chmod -R 755 data/
chown -R www:www data/
```

### 3. 静态资源404
确保 Nginx 配置了静态文件目录，或者使用 PM2 运行时保持静态文件可访问。
