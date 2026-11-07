# surge-ruleset-patching

从真实流量生成的 Surge ruleset，补公共规则列表跟不上的地方。每个子目录一个 ruleset。

## steamcn-cdn-auto：Steam 中国下载

Steam 中国地区的游戏下载会用不同的域名，而且经常有新的，比如 `gdtstream.com`、`sycontroller.com`、`cyngaa.com`、`eccdnx.com`…… 这个 ruleset 适合默认代理、针对中国区网站走白名单的用户。

原有列表主要来自监控真实的 Steam 下载；2026-11-07 的补充同时包含公共列表中核对过的 CDN 候选，见下文。这些地址只针对游戏下载，不影响商店、社区和 API 正常走代理。发现新域名时列表会自动更新，每次更新发一个 release，写明新增了哪些域名。

### 使用方法

在 Surge profile 里加一行：

```
RULE-SET,https://raw.githubusercontent.com/Logoutx/surge-ruleset-patching/main/steamcn-cdn-auto/steamcn-cdn-auto.list,DIRECT
```

镜像地址：

```
RULE-SET,https://cdn.jsdelivr.net/gh/Logoutx/surge-ruleset-patching@main/steamcn-cdn-auto/steamcn-cdn-auto.list,DIRECT
```

## 2026-11-07：Steam CDN 主机名补充

保留现有规则，补充本轮审计发现的主机名：新增 41 条精确 `DOMAIN` 规则。其中 18 条来自观察到的 Steam 内容连接或下载日志，23 条为公共列表中的下载、内容分发和客户端更新候选。部分精确规则已由现有后缀规则覆盖，仍保留以便核对本次发现；不将它们统计为新发现的流量泄漏。

最近下载日志中的 `dl.steam.clngaa.com`、`st.dl.eccdnx.com`、`xz.pphimalayanrt.com`、`yif.gdtstream.com`、`gstore.val.smogfly.com` 原本已命中直连，现明确记录到列表。国际 CDN、客户端更新和 Azure 内容存储候选不等同于中国大陆出口，也不代表本次会话使用过这些服务；列表名称沿用原目录。

建议在广泛的 Steam 代理规则之前引用，并开启 TLS SNI / HTTP Host 扩展匹配：

```ini
RULE-SET,https://raw.githubusercontent.com/Logoutx/surge-ruleset-patching/main/steamcn-cdn-auto/steamcn-cdn-auto.list,DIRECT,extended-matching
```

这批只增加公共 CDN 主机名；未加入商店、社区、登录或 API 主机名，也未加入新的 IP 网段。仅 IP 且无可识别主机名的连接仍需要独立、受限的本地规则。DNS 失效或历史 CDN 退役不会因加入直连规则而恢复可用。

后续自动更新应保留并合并本补充区块，不能仅凭新一轮流量快照覆盖掉这些已审计的主机名。仓库目前没有内置生成脚本或 Actions 工作流；本次未改变外部监控程序。

参考来源：

- [Steam 公共规则](https://github.com/blackmatrix7/ios_rule_script/blob/master/rule/Surge/Steam/Steam.list)
- [SteamCN 公共规则](https://github.com/blackmatrix7/ios_rule_script/blob/master/rule/Surge/SteamCN/SteamCN.list)
- [V2Fly Steam 主机名列表](https://github.com/v2fly/domain-list-community/blob/master/data/steam)
