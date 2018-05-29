```shell
faner@MBP-FAN:~/Projects/git/web/node/npm/npm-config-list|master⚡
⇒  colordiff npm\ config\ list\ -l.md cnpm\ config\ list\ -l.md
1d0
<
3c2
< faner@MBP-FAN:~|⇒  npm config list -l
---
> faner@MBP-FAN:~|⇒  cnpm config list -l
4a4
> disturl = "https://npm.taobao.org/mirrors/node"
6c6,7
< metrics-registry = "https://registry.npmjs.org/"
---
> metrics-registry = "https://registry.npm.taobao.org/"
> registry = "https://registry.npm.taobao.org/"
8,11c9,10
< user-agent = "npm/6.1.0 node/v10.2.1 darwin x64"
<
< ; builtin config undefined
< prefix = "/usr/local"
---
> user-agent = "npm/5.10.0 node/v10.2.1 darwin x64"
> userconfig = "/Users/faner/.cnpmrc"
49,50c48,49
< globalconfig = "/usr/local/etc/npmrc"
< globalignorefile = "/usr/local/etc/npmignore"
---
> globalconfig = "/usr/local/Cellar/node/10.2.1/etc/npmrc"
> globalignorefile = "/usr/local/Cellar/node/10.2.1/etc/npmignore"
88c87
< ; prefix = "/usr/local/Cellar/node/10.2.1" (overridden)
---
> prefix = "/usr/local/Cellar/node/10.2.1"
94c93
< registry = "https://registry.npmjs.org/"
---
> ; registry = "https://registry.npmjs.org/" (overridden)
125c124
< user = 0
---
> user = 501
127c126
< userconfig = "/Users/faner/.npmrc"
---
> ; userconfig = "/Users/faner/.npmrc" (overridden)
131c130
< ```
\ No newline at end of file
---
> ```
```

## user-agent

`user-agent` 不同，cnpm 基于较老版本的 `npm/5.10.0`。

## registry

cnpm overridden 了 `registry`；  
`metrics-registry` 不同，cnpm 基于淘宝的 registry。  

## prefix

cnpm 比 npm 多了 `disturl`。  
npm overridden 了 `prefix`。  

## config

cnpm overridden 了`userconfig`，  
`globalconfig` 和 `globalignorefile` 不同。  
