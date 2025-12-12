# 本地开发指南

## 快速开始

### 1. 克隆项目
```bash
git clone https://github.com/PastKing/tgbot-verify.git
cd tgbot-verify
```

### 2. 安装依赖
```bash
pip install -r requirements.txt
playwright install chromium
```

### 3. 配置环境变量

项目根目录下已经为您创建了 `.env` 文件，包含以下配置：

```env
# Telegram Bot 配置
BOT_TOKEN=YOUR_BOT_TOKEN
CHANNEL_USERNAME=pk_oa
CHANNEL_URL=https://t.me/pk_oa
ADMIN_USER_ID=YOUR_ADMIN_ID

# MySQL 数据库配置
MYSQL_HOST=YOUR_DB_HOST
MYSQL_PORT=3306
MYSQL_USER=YOUR_DB_USER
MYSQL_PASSWORD=YOUR_DB_PASSWORD
MYSQL_DATABASE=YOUR_DB_NAME
```

> 📌 **注意**：
> - `.env` 文件已被 `.gitignore` 忽略，不会提交到 Git
> - 如果需要修改配置，直接编辑 `.env` 文件
> - 项目会自动加载 `.env` 文件（使用 python-dotenv）

### 4. 启动机器人

```bash
python bot.py
```

## 目录结构

```
tgbot-verify/
├── bot.py              # 机器人主程序
├── config.py           # 全局配置（自动加载 .env）
├── database_mysql.py   # MySQL 数据库管理
├── .env                # 本地环境变量（已被 Git 忽略）
├── env.example         # 环境变量模板
├── handlers/           # 命令处理器
│   ├── user_commands.py
│   ├── admin_commands.py
│   └── verify_commands.py
├── one/                # Apple 教育认证模块
├── k12/                # K-12 学生认证模块
├── Boltnew/            # Bolt 学生认证模块
└── utils/              # 工具函数
```

## 环境变量说明

| 变量名 | 必填 | 说明 | 示例 |
|--------|------|------|------|
| `BOT_TOKEN` | ✅ | Telegram Bot Token | `123456:ABC-DEF...` |
| `CHANNEL_USERNAME` | ❌ | 频道用户名 | `pk_oa` |
| `CHANNEL_URL` | ❌ | 频道链接 | `https://t.me/pk_oa` |
| `ADMIN_USER_ID` | ✅ | 管理员 Telegram ID | `123456789` |
| `MYSQL_HOST` | ✅ | MySQL 主机地址 | `localhost` |
| `MYSQL_PORT` | ❌ | MySQL 端口 | `3306` |
| `MYSQL_USER` | ✅ | MySQL 用户名 | `root` |
| `MYSQL_PASSWORD` | ✅ | MySQL 密码 | `yourpassword` |
| `MYSQL_DATABASE` | ✅ | 数据库名称 | `tgbot_verify` |

## 开发技巧

### 查看日志
```bash
tail -f logs/bot.log
```

### 测试配置加载
```bash
python -c "import config; print('BOT_TOKEN:', 'OK' if config.BOT_TOKEN else 'MISSING')"
```

### 验证数据库连接
```bash
python -c "from database_mysql import Database; db = Database(); print('Database connected!')"
```

### 清理 Python 缓存
```bash
find . -type d -name __pycache__ -exec rm -rf {} +
find . -type f -name "*.pyc" -delete
```

## 常见问题

### Q: 为什么没有读取到 .env 文件？
**A**: 确保 `python-dotenv` 已安装：
```bash
pip install python-dotenv
```

### Q: 数据库连接失败？
**A**: 检查 MySQL 服务是否启动，以及 `.env` 中的数据库配置是否正确。

### Q: Playwright 浏览器安装失败？
**A**: 手动安装：
```bash
playwright install chromium --with-deps
```

### Q: .env 文件会提交到 Git 吗？
**A**: 不会！`.gitignore` 已经配置忽略 `.env` 文件。

## 提交代码前检查

✅ 确认 `.env` 文件没有被提交
```bash
git check-ignore -v .env
# 输出: .gitignore:49:.env	.env
```

✅ 确认没有硬编码敏感信息
```bash
git diff
```

## 相关链接

- 📖 [完整部署文档](DEPLOY.md)
- 📖 [项目 README](README.md)
- 📖 [English README](README_EN.md)
- 🔗 [Telegram 频道](https://t.me/pk_oa)
- 🔗 [Telegram 群组](https://t.me/pastking_server)
- 💻 [GitHub 仓库](https://github.com/PastKing/tgbot-verify)

