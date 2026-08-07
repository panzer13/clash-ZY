# clash-ZY 项目记忆

## 仓库信息

- **本仓库**：`panzer13/clash-ZY`（个人定制版）
- **上游仓库**：`qichiyuhub/rule`（原作者 qichiyu 的模板仓库）
- **开发分支**：`claude/upstream-repo-check-r966uo`
- **主分支**：`main`

## 项目结构

```
config/
  mihomo/
    AI/               # smart 路由（对应上游的 smart/ 目录）
      smart.yaml      # 主配置（含 MosDNS、台湾节点、EMBY、广告拦截）
      transform.go    # LightGBM 智能路由 Go 代码（LF 行尾）
      go_parser.py    # Python 解析工具
      train_flexible.py
    config.yaml       # 标准 Mihomo 配置
    configdns.yaml    # 带 DNS 防泄漏版本
    fuxie.yaml        # 副配置
    full.ini / mini.ini  # Clash for Windows 配置
    nikki / openclash   # 插件版配置
  proxychain/         # 代理链配置（对应上游的 mihomo/proxychain.yaml）
  singbox/1.12.x/     # Sing-box 1.12.x 配置
  singbox/1.13X/      # Sing-box 1.13X 配置（config/reF1nd/momo/substore-scripts）
  zijian/             # 自建节点配置（对应上游的 singbox/1.12.x/vps/）
direct.list           # 直连规则（本地，与上游 rules/ 目录内容一致）
proxy.list            # 代理规则
fakeipfilter.json     # FakeIP 过滤列表
```

## 本地相对上游的定制内容（已领先上游）

1. **台湾节点支持**：`♻️ 台湾智能` 智能组，已加入各主要策略组
2. **EMBY 流媒体分流**：`🎬 EMBY` 策略组 + `emby_domain` inline 规则集
3. **MosDNS DNS 防泄漏**：nameserver 指向 `127.0.0.1:5335`，DNS 规则强制 8.8.8.8/1.1.1.1 走代理
4. **广告拦截**：`RULE-SET,ads,REJECT` + `RULE-SET,reject,REJECT`
5. **URL 路径已更新**：所有配置中 `rules/proxy.list` → `proxy.list`（上游仍是旧路径）
6. **规则分区注释**：smart.yaml 规则区用注释分成 6 个区块

## 上游同步记录

- **最后同步日期**：2026-08-07
- **上游最新 commit**：`56efb3b`
- **已同步 commits**：
  - `34f0ab9`（2026-04-11）：新增 `config/singbox/1.13X/` 目录（config/fork/iphone/momo/combine）
  - `80a856e`（2026-06-29）：README 添加禁止转载声明，删除机场广告；删除 `.github/FUNDING.yml`（本地已无此文件）
  - `22ab486`：上游目录重构（mihomo 拆 config//other/）—— 本地不跟，保留原命名
  - `aecaec6`：sing-box 配置优化（inet4_range→198.19.0.0/16，fakeipfilter-cn，log info，去 client_subnet，去 cache path，外部 UI→"ui"）
  - `b81cdd8`：路由规则重构（去 Mijia Cloud，STUN/QUIC 合并+no_drop，ICMP resolve+直连）
  - `1c6d4df`：1.13X 文件整理（fork→reF1nd，iphone 删除，combine→substore-scripts）
  - `1fe2801`：删除 proxylite 规则和 rule-provider（mihomo config/smart/configdns 全部同步）
  - `80fe5b1`：fake-ip-range 修正（mihomo 28.0.0.1/8→198.18.0.0/16）
  - `56efb3b`：删除 respect-rules（mihomo DNS 配置）
- **历史同步操作**（2026-06-15，基于 `e419bd0`）：
  - transform.go / go_parser.py：CRLF → LF
  - smart.yaml：proxylite URL 去掉 `rules/` 前缀

## 注意事项

- 上游 `qichiyuhub/rule` 文件在 `rules/` 子目录，本仓库已移至根目录
- 目录结构保持本地命名（`AI/` 不改为 `smart/`，`zijian/` 不改为 `vps/`）
- smart.yaml 的 nameserver 当前为 `127.0.0.1:5335`（配合 MosDNS 使用）
