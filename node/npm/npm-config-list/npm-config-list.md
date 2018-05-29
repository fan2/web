## npm config list

```shell
faner@MBP-FAN:~|⇒  npm config list
; cli configs
metrics-registry = "https://registry.npmjs.org/"
scope = ""
user-agent = "npm/6.1.0 node/v10.2.1 darwin x64"

; builtin config undefined
prefix = "/usr/local"

; node bin location = /usr/local/Cellar/node/10.2.1/bin/node
; cwd = /Users/faner
; HOME = /Users/faner
; "npm config ls -l" to show all defaults.
```

`npm config list -g` 比 `npm config list` 多输出了一项 `global = true`，其他相同。

### npm config ls -l

执行 `npm config ls -l` 可查看更详细配置信息：

```shell
cache = "/Users/faner/.npm"

globalconfig = "/usr/local/etc/npmrc"
globalignorefile = "/usr/local/etc/npmignore"

heading = "npm"
https-proxy = null

init-module = "/Users/faner/.npm-init.js"

node-version = "10.2.1"

; prefix = "/usr/local/Cellar/node/10.2.1" (overridden)

registry = "https://registry.npmjs.org/"

userconfig = "/Users/faner/.npmrc"
```

### [Cache](https://docs.npmjs.com/files/folders#cache)

See [npm-cache](https://docs.npmjs.com/cli/cache). Cache files are stored in **`~/.npm`** on Posix, or **`%AppData%/npm-cache`** on Windows.

This is controlled by the *cache* configuration param.

## cnpm config list

```shell
faner@MBP-FAN:~|⇒  cnpm config list
; cli configs
disturl = "https://npm.taobao.org/mirrors/node"
metrics-registry = "https://registry.npm.taobao.org/"
registry = "https://registry.npm.taobao.org/"
scope = ""
user-agent = "npm/5.10.0 node/v10.2.1 darwin x64"
userconfig = "/Users/faner/.cnpmrc"

; node bin location = /usr/local/Cellar/node/10.2.1/bin/node
; cwd = /Users/faner
; HOME = /Users/faner
; "npm config ls -l" to show all defaults.
```

`cnpm config list -g` 比 `cnpm config list` 多输出了一项 `global = true`，其他相同。

### cnpm config ls -l