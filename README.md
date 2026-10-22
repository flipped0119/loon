# loon

自用的 Loon 插件、分流规则，以及一份通用的 mihomo（Clash Meta）模板。

## 插件

<!-- plugins:start -->
| 插件 | 规则数 | 安装链接 |
|---|---|---|
| 高德地图去广告补充 | 12 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Amap_Supplement.lpx` |
| 百度网盘去广告补充 | 10 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/BaiduNetDisk_Supplement.lpx` |
| 菜鸟去广告补充 | 7 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Cainiao_Supplement.lpx` |
| 彩云天气去广告补充 | 7 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/ColorfulClouds_Supplement.lpx` |
| 闲鱼去广告补充 | 3 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Goofish_Supplement.lpx` |
| Keep去广告补充 | 8 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Keep_Supplement.lpx` |
| 墨迹天气去广告补充 | 4 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/MojiWeather_Supplement.lpx` |
| 网易云音乐去广告补充 | 25 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/NeteaseMusic_Supplement.lpx` |
| 什么值得买去广告补充 | 5 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Smzdm_Supplement.lpx` |
| 汽水音乐去广告补充 | 6 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/SodaMusic_Supplement.lpx` |
| 通用开屏广告补充 | 416 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Splash_Supplement.lpx` |
| 淘票票去广告补充 | 2 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Taopiaopiao_Supplement.lpx` |
| 百度贴吧去广告补充 | 2 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Tieba_Supplement.lpx` |
| 微博增强补充 | 5 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Weibo_Supplement.lpx` |
| 小红书去广告补充 | 13 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Xiaohongshu_Supplement.lpx` |
| 喜马拉雅去广告补充 | 21 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Ximalaya_Supplement.lpx` |
| YouTube去广告补充 | 3 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/YouTube_Supplement.lpx` |
| 知乎去广告补充 | 36 | `https://raw.githubusercontent.com/flipped0119/loon/main/plugins/Zhihu_Supplement.lpx` |
<!-- plugins:end -->

- **补充插件**（`*_Supplement`）配合各 App 常用的去广告插件使用，只处理那些插件没覆盖的接口。**请排在其他去广告插件之后**：Loon 3.5.1 起，同一个请求只执行第一条命中的脚本（本地配置排在插件之前），排在后面才不会顶掉主插件。
- 「通用开屏广告补充」覆盖数百个 App 的开屏广告，MITM 主机名有四百多个，会明显增加 Loon 的解密开销和内存占用，用得到再开。
- 微博补充附带设置页，在 Safari 打开 `https://api.weibo.cn/__qx_weibo_settings__/`。

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
