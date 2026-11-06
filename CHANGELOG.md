# 更新记录

## 2026-11-06

### 交易所分流检查

- 核验 `bitget.com`、`www.bitget.com`、`api.bitget.com`、`ws.bitget.com` 及现有 Binance、Bybit、OKX、Coinbase、Kraken 主域名的生成规则，均指向「💱 交易所」，且早于 `Foreign`。
- 确认当前上游 Crypto 规则集未包含 Bitget；主域名及其子域名由脚本显式规则覆盖。
- README 新增命中规则、代理链、分组保存选项、配置更新和长连接的排查步骤。
- 本次未修改分流脚本；尚无客户端连接记录，不能确认用户反馈的具体请求域名、命中规则或实际出口。

### 新增

- 新增「🟢 OpenAI」独立代理分组，支持为 ChatGPT / OpenAI 单独选择节点。
- 将 `openai.com`、`chatgpt.com`、`oaistatic.com`、`oaiusercontent.com` 和已有 OpenAI 远程规则集指向新分组。

### 调整

- OpenAI 流量从「🤖 AI服务」分组独立出来，规则位于其他 AI 和通用兜底规则之前。
- 新分组沿用 `AI_NODE` 默认节点（当前为 `Host-V-家宽`）；节点不存在时默认跟随「🚀 节点选择」。
- README 同步更新代理组说明和分流顺序。

### 验证与使用

- 已通过 JavaScript 语法检查，以及 OpenAI 规则指向、优先级、默认节点回退和节点重名处理检查。
- 等待 GitHub Raw 缓存更新后，在 Clash Verge 更新订阅，并在「代理」页为「🟢 OpenAI」选择节点。
