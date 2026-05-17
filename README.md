# ⚡ OPC API Proxy — 一站式 AI API 代理平台

[![GitHub Stars](https://img.shields.io/badge/dynamic/json?logo=github&label=Stars&query=%24.stargazers_count&url=https%3A%2F%2Fapi.github.com%2Frepos%2Fyour-username%2Fopc-api-proxy)](https://github.com/your-username/opc-api-proxy)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://python.org)

> **一人公司即可运营的 AI API 代理转发平台**  
> 聚合 OpenAI / DeepSeek / Claude / Gemini / Groq / Ollama，统一 OpenAI 兼容接口

---

## ✨ 功能特性

### 🔌 多 Provider 聚合
| Provider | 状态 | 模型 |
|:--|:--:|:--|
| OpenAI (GPT-4o/o3) | ✅ | `gpt-4o`, `gpt-4.1`, `o3`, `o4-mini` |
| DeepSeek | ✅ | `deepseek-chat`, `deepseek-v4-flash`, `deepseek-reasoner` |
| Anthropic Claude | ✅ | `claude-sonnet-4`, `claude-haiku-4` |
| Google Gemini | ✅ | `gemini-2.5-pro`, `gemini-2.5-flash` |
| Groq | ✅ | `groq-llama-4`, `groq-deepseek`, `groq-mixtral` |
| Ollama (本地) | ✅ | `ollama-llama3`, `ollama-qwen`, `ollama-deepseek-r1` |

### 🛡️ 安全防护
- IP 级别限流（防 DDoS）
- API Key 暴力破解防护
- 单 Key 并发控制
- SQL 注入检测
- Prompt 注入检测
- 请求体大小限制

### 💰 计费系统
- **按量付费** — 预充值，按 Token 扣费
- **订阅套餐** — 月付/年付，含固定额度
- **超量计费** — 额度用完后自动按量扣费
- **推荐奖励** — 推荐好友注册，双方得奖励

### 📊 管理后台
- 实时用量统计
- API Key 管理
- 套餐配置（运营可修改）
- 充值记录
- 24h 请求分布图表

### 🏪 客户门户
- 注册/登录
- 余额与用量查看
- 在线充值
- 推荐码系统
- 帮助手册

---

## 🚀 快速部署

### 前置要求
- Python 3.10+
- 香港/海外云服务器（可选，但推荐）

### 一键部署

```bash
git clone https://github.com/your-username/opc-api-proxy.git
cd opc-api-proxy
python3 -m venv venv
source venv/bin/activate
pip install fastapi uvicorn httpx python-dotenv sqlalchemy aiosqlite python-multipart

# 配置 API Key
cp .env.example .env
# 编辑 .env 填入你的 OpenAI / DeepSeek / Claude / Gemini / Groq Key

# 启动所有服务
python main.py
```

### 服务地址

| 服务 | 地址 | 说明 |
|:--|:--|:--|
| **代理接口** | `http://localhost:8787/v1/chat/completions` | OpenAI 兼容 |
| **管理后台** | `http://localhost:8788/admin/login` | 运营管理 |
| **客户门户** | `http://localhost:8789` | 用户自助 |
| **健康检查** | `http://localhost:8787/v1/health` | 监控 |

---

## 📦 客户端使用

```python
# pip install openai
from openai import OpenAI

client = OpenAI(
    api_key="opc-xxx",                    # 注册后获取
    base_url="https://your-server.com/v1"  # 替换为你的服务器地址
)

# 一行切换模型
response = client.chat.completions.create(
    model="deepseek-chat",   # 或 gpt-4o / claude-sonnet-4 / gemini-2.5-flash
    messages=[{"role": "user", "content": "Hello"}]
)
print(response.choices[0].message.content)
```

---

## 🧩 项目结构

```
opc-api-proxy/
├── proxy/
│   ├── server.py        # 代理服务器 (FastAPI)
│   ├── router.py        # 模型路由 & 转发
│   ├── auth.py          # API Key 认证 / 限流 / 计费 / 缓存
│   ├── security.py      # 安全中间件
│   ├── models.py        # 数据库模型
│   └── database.py      # 数据库初始化
├── admin/
│   └── dashboard.py     # 管理后台
├── portal/
│   └── app.py           # 客户门户
├── config/
│   └── settings.py      # 全局配置
├── sdks/
│   ├── python/          # Python 客户端 SDK
│   └── node/            # Node.js 客户端 SDK
├── main.py              # 一键启动入口
└── deploy.sh            # 境外服务器部署脚本
```

---

## 📊 定价参考

| 套餐 | 月费 | Token 额度 | 适用模型 |
|:--|:--:|:--:|:--|
| 🥉 入门版 | ¥99 | 5,000万 | DeepSeek + Gemini Flash + Groq |
| 🥈 标准版 | ¥299 | 2亿 | 全部模型（GPT-4o/Claude） |
| 🥇 专业版 | ¥999 | 10亿 | 全部模型 + 高并发 |
| 🎯 企业版 | 定制 | 100亿 | 全部 + 私有部署 |

---

## 🤝 贡献

欢迎提交 Issue 和 PR！一起建设最好的开源 AI API 代理平台。

## 📄 License

MIT License

## ⭐ Star History

如果你觉得这个项目有帮助，请给我们一个 Star ⭐，让更多人看到！
