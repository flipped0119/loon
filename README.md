# loon

自用的 Loon 插件、分流规则，以及一份通用的 mihomo（Clash Meta）模板。

## 插件

| 插件 | 安装链接 | 说明 |
|---|---|---|
| 微博增强补充 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Weibo_Supplement.lpx` | 配合常用的「微博去广告」插件使用，只补它没处理的接口：视频流广告与频道、首页红点与消息数、直播头像栏等。附带设置页，在 Safari 打开 `https://api.weibo.cn/__qx_weibo_settings__/` |

Loon 3.5.1 起，同一个请求只执行第一条命中的脚本（本地配置排在插件之前），两个去广告插件同时处理一个接口时只有一个生效。所以补充类插件只处理主插件没覆盖的接口。

## 分流规则

| 清单 | 链接 | 建议策略 |
|---|---|---|
| Claude | `https://raw.githubusercontent.com/flipped0119/loon/main/rules/Claude.list` | 能用 Claude 的地区（不含香港） |
| 银行防 VPN 检测 | `https://raw.githubusercontent.com/flipped0119/loon/main/rules/BankAntiVPN.list` | REJECT |

Loon 写在 `[Remote Rule]`，例如：

```
https://raw.githubusercontent.com/flipped0119/loon/main/rules/Claude.list, policy=Claude, tag=Claude, enabled=true
```

专用清单要放在 proxy.list 这类大清单之前，否则会被大清单先命中。

## mihomo 模板

[`mihomo/config.yaml`](mihomo/config.yaml)：把 `proxy-providers` 里的 `url` 换成你的机场订阅即可使用。

- 地区组按节点名自动归组（旗帜、中英文地名、城市、中转简称、大写缩写），自动排除回国、游戏节点和「到期、剩余流量」这类信息条目
- 分流用 MetaCubeX meta-rules-dat 的 mrs 规则集，DNS 用 fake-ip 加国内 DoH
- 机场没有的地区组是空的，mihomo 会在里面放一个 COMPATIBLE（等同直连），不要在服务分组里手动选择空的地区组
