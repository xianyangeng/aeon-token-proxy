# Aeon Token 中转站 — 帮助手册

> 一站式 AI API 代理平台 · 聚合 OpenAI / DeepSeek / Claude / Gemini / Groq / Ollama

---

## 🚀 快速开始

**1.** 注册账号 → 在仪表盘获取 API Key

**2.** 充值或订阅套餐 → 获得调用额度

**3.** 接入代码（OpenAI 兼容接口）：

```python
pip install openai

from openai import OpenAI
client = OpenAI(
    api_key=***
    base_url="https://your-server.com/v1"
)
response = client.chat.completions.create(
    model="deepseek-chat",
    messages=[{"role": "user", "content": "Hello"}]
)
print(response.choices[0].message.content)
```

---

## 📋 可用模型

| 模型 | Provider | 多模态 | 输入 ¥/1K | 输出 ¥/1K |
|---|---|---|---|---|
| `gpt-4o` | OpenAI | ✅ | 0.015 | 0.060 |
| `gpt-4o-mini` | OpenAI | ✅ | 0.0015 | 0.006 |
| `gpt-4.1` | OpenAI | ❌ | 0.010 | 0.040 |
| `o3` | OpenAI | ✅ | 0.050 | 0.200 |
| `o4-mini` | OpenAI | ✅ | 0.002 | 0.008 |
| `deepseek-chat` | DeepSeek | ❌ | 0.00014 | 0.00028 |
| `deepseek-v4-flash` | DeepSeek | ❌ | 0.00014 | 0.00028 |
| `deepseek-reasoner` | DeepSeek | ❌ | 0.00014 | 0.00028 |
| `claude-sonnet-4` | Anthropic | ✅ | 0.015 | 0.075 |
| `claude-haiku-4` | Anthropic | ✅ | 0.0025 | 0.010 |
| `gemini-2.5-pro` | Gemini | ✅ | 0.010 | 0.040 |
| `gemini-2.5-flash` | Gemini | ✅ | 0.001 | 0.004 |
| `groq-llama-4` | Groq | ❌ | 0.0003 | 0.0003 |
| `groq-deepseek` | Groq | ❌ | 0.0003 | 0.0003 |
| `groq-mixtral` | Groq | ❌ | 0.0003 | 0.0003 |

---

## 🖼️ 多模态接入

OPC Proxy 完整支持多模态（图片识别），兼容 OpenAI 格式。

### Python 代码示例

```python
from openai import OpenAI
import base64

client = OpenAI(
    api_key=***
    base_url="https://your-server.com/v1"
)

# 读取图片为 base64
def encode_image(path):
    with open(path, "rb") as f:
        return base64.b64encode(f.read()).decode()

base64_img = encode_image("photo.jpg")

# 多模态请求（文本 + 图片）
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{
        "role": "user",
        "content": [
            {"type": "text", "text": "这张图片里有什么？"},
            {
                "type": "image_url",
                "image_url": {
                    "url": f"data:image/jpeg;base64,{base64_img}"
                }
            }
        ]
    }]
)
print(response.choices[0].message.content)
```

### cURL 示例

```bash
curl https://your-server.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ***" \
  -d '{
    "model": "gpt-4o",
    "messages": [{
      "role": "user",
      "content": [
        {"type": "text", "text": "描述这张图片"},
        {
          "type": "image_url",
          "image_url": {
            "url": "https://example.com/photo.jpg"
          }
        }
      ]
    }]
  }'
```

---

## 🔌 SDK & 客户端

### Python SDK

```python
pip install opc-proxy

from opc_proxy import OPCClient
client = OPCClient(api_key="opc-xxx", base_url="https://your-server.com")
response = client.chat("Hello")
print(response)
```

### Node.js SDK

```bash
npm install @opc-proxy/client

const OPC = require('@opc-proxy/client');
const client = new OPC({ apiKey: 'opc-xxx', baseUrl: 'https://your-server.com' });
client.chat('Hello').then(console.log);
```

### VS Code 插件
- 侧边栏 AI 对话（多模型切换）
- 选中代码解释 / 重构
- 快捷键：`Ctrl+Alt+O` 打开对话 / `Ctrl+Alt+E` 解释代码

### Chrome 扩展
- 浏览器中随时调用 AI
- 选中文本右键 → AI 解释

---

### 🦞 OpenClaw — AI 网关/Agent 平台
- 将 Aeon 设为模型提供者，统一管理和计费
- 支持 OpenAI 兼容接口，一行配置即可
- 一键接入脚本：`./setup-aeon.sh <API_KEY> <服务器地址>`

配置示例（openclaw.json）：
```json
{
  "agents": {
    "defaults": {
      "model": {
        "openaiBaseUrl": "https://your-server.com/v1",
        "openaiApiKey": "opc-xxx"
      }
    }
  }
}
```

### 🤖 Hermes Agent — 智能 AI Agent 框架
- 支持任意 OpenAI 兼容 API 作为后端
- 配置环境变量即可接入 Aeon
- 一键接入脚本：`./setup-aeon.sh <API_KEY> <服务器地址>`

配置示例（~/.hermes/.env）：
```env
AI_GATEWAY_BASE_URL=https://your-server.com/v1
AI_GATEWAY_API_KEY=opc-xxx
```

---

## 🦞 OpenClaw 接入

将 Aeon 设为 OpenClaw 的模型提供者。

### 一键接入

```bash
curl -O https://your-server.com/sdks/setup-aeon.sh
chmod +x setup-aeon.sh
./setup-aeon.sh <你的API_KEY> https://your-server.com
```

### 手动配置

在 `openclaw.json` 中配置：

```json
{
  "agents": {
    "defaults": {
      "model": {
        "openaiBaseUrl": "https://your-server.com/v1",
        "openaiApiKey": "opc-xxx"
      }
    }
  }
}
```

或通过命令行：

```bash
openclaw config set agents.defaults.model.openaiBaseUrl "https://your-server.com/v1"
openclaw config set agents.defaults.model.openaiApiKey "opc-xxx"
openclaw gateway restart
```

---

## 🤖 Hermes Agent 接入

### 一键接入

```bash
curl -O https://your-server.com/sdks/setup-aeon.sh
chmod +x setup-aeon.sh
./setup-aeon.sh <你的API_KEY> https://your-server.com
```

### 手动配置

在 `~/.hermes/.env` 或项目根目录 `.env` 中添加：

```env
AI_GATEWAY_BASE_URL=https://your-server.com/v1
AI_GATEWAY_API_KEY=opc-xxx
```

或通过环境变量：

```bash
export AI_GATEWAY_BASE_URL=https://your-server.com/v1
export AI_GATEWAY_API_KEY=opc-xxx
hermes start
```

---

## 💰 计费说明

### 按量付费
预充值，按 Token 扣费，单价见上方表格。

### 订阅套餐
| 套餐 | 月费 | Token 额度 | 适用模型 |
|---|---|---|---|
| 🥉 入门版 | ¥99 | 5,000万 | DeepSeek + Gemini Flash + Groq |
| 🥈 标准版 | ¥299 | 2亿 | 全部模型（GPT-4o / Claude） |
| 🥇 专业版 | ¥999 | 10亿 | 全部模型 + 高并发 |
| 🎯 企业版 | 定制 | 100亿 | 全部 + 私有部署 |

### 💎 省钱建议
高频使用 DeepSeek / Gemini Flash 性价比最高；GPT-4o / Claude 适合复杂任务。推荐订阅套餐可大幅降低成本。

---

## 🎯 推荐奖励

每推荐一位好友注册并充值，你和好友各获得 **¥10** 奖励！
好友使用你的推荐码注册，首单套餐享 **9折优惠**。

推荐码可在仪表盘查看。

---

## ❓ 常见问题

**Q: API Key 在哪里获取？**
注册登录后，在仪表盘页面即可看到你的 API Key。

**Q: 支持哪些编程语言？**
任何支持 OpenAI SDK 的语言均可使用：Python、Node.js、Java、Go、Ruby 等。

**Q: 如何切换模型？**
修改请求中的 `model` 字段即可，无需改其他代码。

**Q: 数据安全如何？**
所有请求通过服务器转发，不存储你的对话内容。

**Q: 如何私有部署？**
克隆本仓库，配置 .env 后执行 `python main.py` 即可一键启动。

---

## 💬 联系 & 贡献

- GitHub：https://github.com/xianyangeng/aeon-token-proxy
- 觉得好用？给我们一个 Star ⭐
- 问题反馈请提交 Issue
