
## diff npm\ config\ list\ -gl

主要区别在于 global 和 user 字段：

```shell
faner@MBP-FAN:~/Projects/git/web/node/npm/npm-config-list|master⚡
⇒  colordiff npm\ config\ list\ -l.md npm\ config\ list\ -gl.md
3c3
< faner@MBP-FAN:~|⇒  npm config list -l
---
> faner@MBP-FAN:~|⇒  npm config list -l -g
4a5
> global = true
47c48
< global = false
---
> ; global = false (overridden)
125c126
< user = 0
---
> user = "nobody"
```

## diff cnpm\ config\ list\ -gl

主要区别在于 global 和 user 字段：

```shell
faner@MBP-FAN:~/Projects/git/web/node/npm/npm-config-list|master⚡
⇒  colordiff cnpm\ config\ list\ -l.md cnpm\ config\ list\ -gl.md
1c1
< faner@MBP-FAN:~|⇒  cnpm config list -l
---
> faner@MBP-FAN:~|⇒  cnpm config list -gl
3a4
> global = true
45c46
< global = false
---
> ; global = false (overridden)
123c124
< user = 501
---
> user = "nobody"
```