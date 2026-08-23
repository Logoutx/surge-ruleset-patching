# surge-ruleset-patching

从真实流量生成的 Surge ruleset，补公共规则列表跟不上的地方。每个子目录一个 ruleset。

## steamcn-cdn-auto：Steam 中国下载

Steam 中国地区的游戏下载会用不同的域名，而且经常有新的，比如 `gdtstream.com`、`sycontroller.com`、`cyngaa.com`、`eccdnx.com`…… 这个 ruleset 适合默认代理、针对中国区网站走白名单的用户。

所有域名都通过监控真实的 Steam 下载所获得。这些地址只针对游戏下载，不影响商店、社区和 API 正常走代理。发现新域名时列表会自动更新，每次更新发一个 release，写明新增了哪些域名。

### 使用方法

在 Surge profile 里加一行：

```
RULE-SET,https://raw.githubusercontent.com/Logoutx/surge-ruleset-patching/main/steamcn-cdn-auto/steamcn-cdn-auto.list,DIRECT
```

镜像地址：

```
RULE-SET,https://cdn.jsdelivr.net/gh/Logoutx/surge-ruleset-patching@main/steamcn-cdn-auto/steamcn-cdn-auto.list,DIRECT
```
