# 更新记录

## 2026-11-06

### 修复 Bitget 客户端备用域名漏分流

- 根据用户提供的连接截图，确认 `appapi.bitget.com` 命中原有规则，而多个备用主机落到 `MATCH`；此前仅验证主域名及其子域名，未覆盖这些备用域名。
- 将 `krbitget.com`、`bitgetapps.com` 及其子域名加入「💱 交易所」。
- 为截图中的 `appapi.gdrichem.com`、`appapi.abcdstable.com`、`www.abcdstable.com` 添加精确域名规则，不扩大到其他子域名。
- 已通过脚本语法、截图中七个完整可见主机、现有交易所主域名、匹配顺序、域名边界及 OpenAI / Claude 分流回归检查；客户端实际出口需更新配置后重连确认。
- 使用时重新生成 Sub-Store 文件、更新客户端配置并重启 Bitget；已建立的连接需断开重连。

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
