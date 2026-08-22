# surge-steamcn-downloads

A Surge rule set of the CDN hosts Steam uses for game downloads in mainland China.

Steam in China serves game files from third-party CDNs under hostnames that change often (`gdtstream.com`, `sycontroller.com`, `clngaa.com`, `eccdnx.com`, …), not from `steamcontent.com`. The entries here come from real download traffic observed on a Surge gateway, plus the hosts listed by the usual public rule projects. Store, community and API hosts are deliberately left out so they keep whatever policy you already give them.

Add one line to your profile, above your general proxy rules:

```
RULE-SET,https://raw.githubusercontent.com/Logoutx/surge-steamcn-downloads/main/SteamCN.list,DIRECT
```

Mirror if raw.githubusercontent.com is slow for you:

```
RULE-SET,https://cdn.jsdelivr.net/gh/Logoutx/surge-steamcn-downloads@main/SteamCN.list,DIRECT
```

The list is regenerated after downloads; the header of `SteamCN.list` carries the date.
