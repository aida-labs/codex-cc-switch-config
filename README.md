# codex-cc-switch-config

Aida Labs（api.lsidestudio.com）Codex 中转接入的 CC Switch 配置模板。

## 用法

### 方式 A：粘贴模板（推荐，配置形态完整）

1. CC Switch → Codex → 添加供应商
2. 把 [`config.toml`](./config.toml) 全文粘贴到 config.toml 编辑框
3. 将 `<YOUR_API_KEY>` 替换为你的密钥，保存

### 方式 B：deeplink 一键导入

```
ccswitch://v1/import?resource=provider&app=codex&name=Aida%20Labs&endpoint=https%3A%2F%2Fapi.lsidestudio.com%2Fv1&apiKey=<YOUR_API_KEY>&model=SWE-2&enabled=true
```

注意：deeplink 导入由 CC Switch 源码生成固定模板（key 写入 `auth.json`，`model_reasoning_effort` 固定为 `high`），与本文件形态不同但都能正常接入。两种方式选一种即可。

## 配置项说明

| 配置项 | 值 | 作用 |
|---|---|---|
| `model` | `gpt-6.1-sol` | 默认模型，可用 `GET /v1/models` 查全部可用模型 |
| `model_provider` | `custom` | 指向下面的 `[model_providers.custom]` 块 |
| `wire_api` | `responses` | 使用 OpenAI Responses API（中转站要求） |
| `model_reasoning_effort` | `medium` | 默认推理强度，可选 low/medium/high/xhigh |
| `model_reasoning_summary` | `auto` | 推理摘要展示方式 |
| `model_verbosity` | `high` | 输出详细度 |
| `disable_response_storage` | `true` | 禁止 Codex 存储响应内容 |
| `sandbox_mode` | `workspace-write` | 沙箱策略：仅可写当前工作区 |
| `approval_policy` | `on-request` | 越权操作时请求批准 |
| `base_url` | `https://api.lsidestudio.com/v1` | 中转站 API 端点 |
| `model_catalog_url` | `https://api.lsidestudio.com/v1/models` | 模型清单端点（配合 API Key 发现模型） |
| `requires_openai_auth` | `true` | 携带 OpenAI 风格鉴权头 |
| `experimental_bearer_token` | `<YOUR_API_KEY>` | API 密钥，**必须写在 `[model_providers.*]` 块内**（顶层会被 Codex 忽略） |
| `api_key_model_discovery` | `true` | 允许用 API Key 拉取模型清单 |

## 不包含的内容

本模板刻意不携带任何本机状态（`[projects.*]` 信任记录、`[mcp_servers]`、`[desktop]`/`[tui]` 外观、hooks、插件、OAuth token）。这些应由各用户本机自行管理。
