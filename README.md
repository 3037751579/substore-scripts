# substore-scripts

个人使用的 Sub-Store 脚本，把节点订阅转换成带分流规则的 Mihomo 配置，配合 Clash Verge 使用。

> 这是公开仓库。**不要提交节点地址、密码、UUID、令牌或订阅链接。** 节点信息由脚本运行时从 Sub-Store 读取，不写在这里。

## 文件

| 文件 | 说明 |
|---|---|
| `substore.js` | Sub-Store 脚本：生成代理组、规则集和分流规则 |

## 在 Sub-Store 中使用

1. 打开目标文件，进入「操作」→「脚本操作」。
2. 类型选「远程链接」，填入：

   ```text
   https://raw.githubusercontent.com/Eggfin/substore-scripts/main/substore.js
   ```

3. 打开「关闭缓存」，然后保存文件。
4. 预览输出，确认分组和规则符合预期。
5. 在 Clash Verge 中更新订阅。

运行 Sub-Store 的服务器需要能访问 `raw.githubusercontent.com`。

## 代理组

| 分组 | 用途 | 默认选项 |
|---|---|---|
| 🚀 节点选择 | 通用代理流量 | ⚡ 自动选择 |
| ⚡ 自动选择 | 按延迟自动选节点 | 延迟最低的节点 |
| 💱 交易所 | 加密货币交易所 | DIRECT |
| 🤖 AI服务 | OpenAI、Gemini、Copilot、Muse / Meta AI 等 | `AI_NODE` |
| 🟣 Claude AI | Claude / Anthropic | `AI_NODE` |
| ✈️ Telegram | Telegram | 🚀 节点选择 |
| 📺 YouTube | YouTube | 🚀 节点选择 |
| 🍎 苹果服务 | Apple 服务 | DIRECT |
| 🛑 广告拦截 | 广告域名 | REJECT |
| 🐟 漏网之鱼 | 未匹配的流量 | 🚀 节点选择 |

默认选项只在没有保存过选择时生效，平时以 Clash Verge 里手动选的节点为准。

## 分流顺序

规则从上到下匹配，命中即停止：

1. 本地和局域网地址直连
2. 汽水音乐直连
3. Claude / Anthropic
4. 其他 AI 服务，以及 Muse / Meta AI
5. 加密货币交易所
6. Apple
7. 广告拦截
8. GitHub、YouTube、Telegram
9. 中国大陆域名和 IP 直连
10. 其他国外域名走 🚀 节点选择
11. 其余流量走 🐟 漏网之鱼

新增规则时，要放在 `RULE-SET,Foreign` 和 `MATCH` 之前，否则不会生效。

## 常见修改

- **加 AI 域名：** 在 `config.rules` 的 D 段域名列表里添加。
- **换 AI 默认节点：** 修改 `AI_NODE`。节点改名后也要同步修改，否则 AI 分组会默认跟随 🚀 节点选择。
- **新增分组：** 在 `G` 中加分组名，在 `config["proxy-groups"]` 中加分组，再把规则指向它。

## 更新流程

1. 修改 `substore.js` 并推送到 `main`。
2. 等几分钟，让 GitHub Raw 链接更新。
3. 在 Clash Verge 中更新订阅。
4. 新增分组后，在「代理」页为它选择节点。

## 注意

- `main` 上的脚本会直接被 Sub-Store 使用，推送前先确认语法无误。
- 脚本运行时能读取全部节点信息，请保护好 GitHub 账号，并只引用自己的仓库。
- `facebook.com` 和 `meta.com` 也走 🤖 AI服务，因为 Muse 依赖这些域名。
