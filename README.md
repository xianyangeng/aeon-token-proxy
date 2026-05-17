<div align="center">

# ⚡ Aeon Token 中转站

### 一站式 AI API 代理平台

**聚合 OpenAI · DeepSeek · Claude · Gemini · Groq · Ollama**

统一 OpenAI 兼容接口 · 按量计费 · 订阅套餐 · 安全防护 · SSE 流式

[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10+-blue)](https://python.org)
[![Status](https://img.shields.io/badge/status-production-green)]()
[![Stars](https://img.shields.io/github/stars/xianyangeng/aeon-token-proxy?style=social)]()

---

### 🚀 30 秒接入

```python
pip install openai
from openai import OpenAI
client = OpenAI(
    api_key="你的 API Key",                    # 注册后免费获取
    base_url="https://你的服务器地址/v1"         # 香港节点，直连无需梯子
)
response = client.chat.completions.create(
    model="deepseek-chat",                    # 一行切换模型
    messages=[{"role": "user", "content": "你好"}]
)
print(response.choices[0].message.content)
```

[✨ 免费注册 →](https://你的域名/register) · [📖 帮助手册 →](HELP.md) · [💬 问题反馈 →](https://github.com/xianyangeng/aeon-token-proxy/issues)

---

</div>

## 🌟 核心优势

<table>
<tr>
<td width="33%">
<h3>🔌 零改造接入</h3>
<p>完全兼容 OpenAI SDK，只需改一行 <code>base_url</code>。<br>Python、Node.js、Java、Go… 任何语言即接即用。</p>
</td>
<td width="33%">
<h3>💰 极致性价比</h3>
<p>DeepSeek 低至 ¥0.14/百万 Token，<br>比直连官方还便宜，不需要为每个 Provider 充值。</p>
</td>
<td width="33%">
<h3>🛡️ 企业级安全</h3>
<p>IP 限流 · Key 防爆破 · 并发控制 · SQL/注入检测<br>香港节点直连，无需科学上网。</p>
</td>
</tr>
<tr>
<td>
<h3>🎯 多模型聚合</h3>
<p>一个接口调用所有主流模型：<br>GPT-4o · Claude · DeepSeek · Gemini · Groq</p>
</td>
<td>
<h3>📊 实时用量</h3>
<p>仪表盘实时看余额/消耗/请求量。<br>每个 Token 花在哪里，一目了然。</p>
</td>
<td>
<h3>⚡ SSE 流式</h3>
<p>完整的流式推流支持，<br>逐 Token 输出，和直连体验完全一致。</p>
</td>
</tr>
</table>

---

## 🤖 支持模型（持续更新中）

| 模型 | 供应商 | 输入 ¥/1K Tokens | 输出 ¥/1K Tokens |
|---|---|---|---|
| `deepseek-chat` | DeepSeek 🟢 | ¥0.00014 | ¥0.00028 |
| `deepseek-v4-flash` | DeepSeek 🟢 | ¥0.00014 | ¥0.00028 |
| `deepseek-reasoner` | DeepSeek 🟢 | ¥0.00014 | ¥0.00028 |
| `gemini-2.5-flash` | Gemini 🟢 | ¥0.001 | ¥0.004 |
| `groq-llama-4` | Groq 🟢 | ¥0.0003 | ¥0.0003 |
| `gpt-4o-mini` | OpenAI | ¥0.0015 | ¥0.006 |
| `gpt-4o` | OpenAI | ¥0.015 | ¥0.060 |
| `claude-sonnet-4` | Anthropic | ¥0.015 | ¥0.075 |
| `ocl3` | OpenAI | ¥0.050 | ¥0.200 |

> 📌 性价比之王：**DeepSeek** 系列 + **Gemini Flash** · 复杂任务：**GPT-4o** + **Claude**

---

## 💎 定价方案

| 套餐 | 月费 | Token 额度 | 适用人群 |
|---|---|---|---|
| 🥉 **入门版** | **¥99** | 5,000万 | 个人开发者，DeepSeek + Gemini + Groq |
| 🥈 **标准版** | **¥299** | 2亿 | 小团队，解锁全部模型 |
| 🥇 **专业版** | **¥999** | 10亿 | 企业级，高并发 + 优先线路 |
| 🎯 **企业版** | 定制 | 100亿+ | 私有部署 · SLA 保障 · 定制路由 |

### 🎁 推荐奖励
> 每推荐一位好友注册并充值，**你和好友各得 ¥10**！推荐码在仪表盘查看。

---

## 🔌 客户端接入

<details>
<summary><b>🦞 OpenClaw 用户</b> — 点击展开</summary>

```json
{
  "agents": {
    "defaults": {
      "model": {
        "openaiBaseUrl": "https://你的服务器地址/v1",
        "openaiApiKey": "你的 API Key"
      }
    }
  }
}
```

或通过命令行：
```bash
openclaw config set agents.defaults.model.openaiBaseUrl "https://你的服务器地址/v1"
openclaw config set agents.defaults.model.openaiApiKey "你的 API Key"
openclaw gateway restart
```
</details>

<details>
<summary><b>🤖 Hermes Agent 用户</b> — 点击展开</summary>

在 `~/.hermes/.env` 中添加：
```env
AI_GATEWAY_BASE_URL=https://你的服务器地址/v1
AI_GATEWAY_API_KEY=你的 API Key
```
</details>

<details>
<summary><b>📦 一键接入脚本</b> — 点击展开</summary>

```bash
curl -O https://你的服务器地址/sdks/setup-aeon.sh
chmod +x setup-aeon.sh
./setup-aeon.sh <API_KEY> <服务器地址>
```
自动检测 OpenClaw / Hermes 环境，一键配置。
</details>

---

## 🏗️ 为什么选择 Aeon Token？

| 对比项 | 直连官方 | Aeon Token 中转站 |
|---|---|---|
| Key 管理 | 每个 Provider 一个 Key | **一个 Key 管理所有** |
| 计费 | 多账户多账单 | **统一余额 + 自动扣费** |
| 网络 | 需要科学上网 | **香港节点直连** |
| 团队协作 | 共享 Key 不便 | **独立子 Key + 用量监控** |
| 安全防护 | 需自建 | **限流/防爆破/注入检测 内置** |
| 订阅套餐 | ❌ | **月付/年付省更多** |

---

## 📞 联系我们

<table>
<tr>
<td align="center">
<b>🌐 官网</b><br>
<a href="#">your-server.com</a>
</td>
<td align="center">
<b>📧 邮箱</b><br>
<a href="mailto:support@opc-proxy.com">support@opc-proxy.com</a>
</td>
<td align="center">
<b>💬 问题反馈</b><br>
<a href="https://github.com/xianyangeng/aeon-token-proxy/issues">GitHub Issues</a>
</td>
</tr>
</table>

---

<div align="center">

### ⭐ 觉得有用？给我们一个 Star！

你的支持是我们持续迭代的动力 ❤️

[✨ 免费注册体验 →](https://你的域名/register) · [📖 查看完整帮助手册 →](HELP.md)

---

**墨菲 OPC · 一个人就是一支队伍**

</div>
