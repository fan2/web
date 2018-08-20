## [npm-install](https://docs.npmjs.com/cli/install)

Install a package

```
npm install (with no args, in package dir)
npm install [<@scope>/]<name>
npm install [<@scope>/]<name>@<tag>
npm install [<@scope>/]<name>@<version>
npm install [<@scope>/]<name>@<version range>
npm install <git-host>:<git-user>/<repo-name>
npm install <git repo url>
npm install <tarball file>
npm install <tarball url>
npm install <folder>

alias: npm i
common options: [-P|--save-prod|-D|--save-dev|-O|--save-optional] [-E|--save-exact] [-B|--save-bundle] [--no-save] [--dry-run]

```

This command installs a package, and any packages that it depends on. If the package has a package-lock or shrinkwrap file, the installation of dependencies will be driven by that, with an **`npm-shrinkwrap.json`** taking precedence if both files exist.

See [package-lock.json](https://docs.npmjs.com/files/package-lock.json) and [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

---

**`npm install (in package directory, no arguments)`**:

Install the dependencies in the local node_modules folder.

In global mode (ie, with **`-g`** or **`--global`** appended to the command), it installs the current package context (ie, the current working directory) as a global package.

By default, **npm install** will install all modules listed as dependencies in [package.json](https://docs.npmjs.com/files/package.json).

用 npm 安装淘宝 [cnpm](https://npm.taobao.org/)：`npm install cnpm -g --registry=https://registry.npm.taobao.org`  
安装 whistle：`[c]npm install -g whistle`；  
同时安装 tslint 和 typescript：`[c]npm i -g tslint typescript`；  
	
## [npm-outdated](https://docs.npmjs.com/cli/outdated)

Check for outdated packages

```
npm outdated [[<@scope>/]<pkg> ...]
```

This command will check the registry to see if any (or, specific) installed packages are currently outdated.

基于 cnpm 源检测所有过期包：

```shell
# npm outdated -g --registry=https://registry.npm.taobao.org
faner@MBP-FAN:~|⇒  cnpm outdated -g
Package     Current  Wanted  Latest  Location
npm         6.2.0    6.4.0   6.4.0
typescript  2.8.3    2.9.1   2.9.1
whistle     1.12.0   1.12.1  1.12.1
```

基于 cnpm 源检测某个具体 package 是否过期：`cnpm outdated -g whistle`

## [npm-update](https://docs.npmjs.com/cli/update)

Update a package

```
npm update [-g] [<pkg>...]

aliases: up, upgrade
```

This command will update all the packages listed to the latest version (specified by the **tag** config), respecting semver.

It will also install missing packages. As with all commands that install packages, the **`--dev`** flag will cause **devDependencies** to be processed as well.

If the **`-g`** flag is specified, this command will update globally installed packages.

If no package name is specified, ***all*** packages in the specified location (global or local) will be updated.

- `npm update pkg`：升级本地包；  
- `npm update -g pkg`：升级全局包。  

不指定 pkg 时，则升级所有过期包：

```shell
# cnpm update -g
npm update -g --registry=https://registry.npm.taobao.org
```

### 升级 npm

执行 npm 相关命令（例如 `npm config get prefix`）时，提示有可更新版本：

```shell
faner@MBP-FAN:~|⇒  npm config get prefix
/usr/local


   ╭─────────────────────────────────────╮
   │                                     │
   │   Update available 5.6.0 → 6.0.0    │
   │       Run npm i npm to update       │
   │                                     │
   ╰─────────────────────────────────────╯

```

请勿执行 `npm i npm`：

```shell
faner@MBP-FAN:~|⇒  npm i npm
npm WARN saveError ENOENT: no such file or directory, open '/Users/faner/package.json'
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN enoent ENOENT: no such file or directory, open '/Users/faner/package.json'
npm WARN faner No description
npm WARN faner No repository field.
npm WARN faner No README data
npm WARN faner No license field.

+ npm@6.0.0
added 680 packages in 11.459s
```

> 最好也不要执行 `npm i npm -g` 升级 npm，而应该走 `brew update/upgrade` 随 node 升级 npm？

---

执行 `cnpm outdated -g` 或 `cnpm outdated -g npm` 也会检测 npm 是否过期：

```shell
faner@MBP-FAN:~|⇒  cnpm outdated -g
Package     Current  Wanted  Latest  Location
npm         6.2.0    6.4.0   6.4.0
```

因此，也可执行 **`cnpm up npm -g`** 可升级 npm：

```shell
# update/upgrade
faner@MBP-FAN:~|⇒  cnpm up npm -g
/usr/local/bin/npm -> /usr/local/lib/node_modules/npm/bin/npm-cli.js
/usr/local/bin/npx -> /usr/local/lib/node_modules/npm/bin/npx-cli.js
+ npm@6.4.0
added 5 packages from 3 contributors, removed 9 packages and updated 19 packages in 5.607s
faner@MBP-FAN:~|⇒  npm -v
6.4.0
```

### 升级 cnpm

执行 `[c]npm outdated -g` 或 `cnpm outdated -g cnpm` 检测 cnpm 自身是否过期：

```shell
# cnpm outdated -g
faner@MBP-FAN:~|⇒  npm outdated -g --registry=https://registry.npm.taobao.org
Package  Current  Wanted  Latest  Location
cnpm       5.3.0   5.3.0   6.0.0
```

执行 `cnpm i cnpm -g` 覆盖安装最新的 cnpm：

```shell
faner@MBP-FAN:~|⇒  cnpm i cnpm -g
Downloading cnpm to /usr/local/lib/node_modules/cnpm_tmp
Copying /usr/local/lib/node_modules/cnpm_tmp/_cnpm@6.0.0@cnpm to /usr/local/lib/node_modules/cnpm
Installing cnpm's dependencies to /usr/local/lib/node_modules/cnpm/node_modules
[1/13] auto-correct@^1.0.0 installed at node_modules/_auto-correct@1.0.0@auto-correct
[2/13] ini@^1.3.4 installed at node_modules/_ini@1.3.5@ini
[3/13] giturl@^1.0.0 installed at node_modules/_giturl@1.0.0@giturl
[4/13] bagpipe@^0.3.5 installed at node_modules/_bagpipe@0.3.5@bagpipe
[5/13] colors@^1.1.2 installed at node_modules/_colors@1.3.0@colors
[6/13] npm-request@^1.0.0 installed at node_modules/_npm-request@1.0.0@npm-request
[7/13] debug@^2.2.0 installed at node_modules/_debug@2.6.9@debug
[8/13] commander@~2.10.0 installed at node_modules/_commander@2.10.0@commander
[9/13] open@^0.0.5 installed at node_modules/_open@0.0.5@open
[10/13] cross-spawn@~0.2.8 installed at node_modules/_cross-spawn@0.2.9@cross-spawn
[11/13] urllib@^2.17.0 installed at node_modules/_urllib@2.28.0@urllib
[12/13] npminstall@^3.0.0 installed at node_modules/_npminstall@3.6.2@npminstall
[13/13] npm@^6.1.0 installed at node_modules/_npm@6.1.0@npm
deprecate urllib@2.28.0 › proxy-agent@2.3.1 › socks-proxy-agent@3.0.1 › socks@^1.1.10 If using 2.x branch, please upgrade to at least 2.1.6 to avoid a serious bug with socket data flow and an import issue introduced in 2.1.0
Recently updated (since 2018-05-23): 6 packages (detail see file /usr/local/lib/node_modules/cnpm/node_modules/.recently_updates.txt)
  2018-05-26
    → npminstall@3.6.2 › node-gyp@3.6.2 › which@1(1.3.1) (06:27:32)
  2018-05-25
    → urllib@^2.17.0(2.28.0) (13:35:54)
    → npminstall@3.6.2 › tar@^4.0.1(4.4.4) (08:58:46)
    → npminstall@3.6.2 › node-gyp@3.6.2 › npmlog@4.1.2 › are-we-there-yet@~1.1.2(1.1.5) (06:08:00)
    → npminstall@3.6.2 › node-gyp@3.6.2 › npmlog@4.1.2 › gauge@2.7.4 › wide-align@^1.1.0(1.1.3) (05:36:50)
  2018-05-24
    → npm@^6.1.0(6.1.0) (13:28:35)
All packages installed (235 packages installed from npm registry, used 5s, speed 2.73MB/s, json 218(1.95MB), tarball 11.18MB)
[cnpm@6.0.0] link /usr/local/bin/cnpm@ -> /usr/local/lib/node_modules/cnpm/bin/cnpm

faner@MBP-FAN:~|⇒  cnpm -v
cnpm@6.0.0 (/usr/local/lib/node_modules/cnpm/lib/parse_argv.js)
npm@6.1.0 (/usr/local/lib/node_modules/cnpm/node_modules/_npm@6.1.0@npm/lib/npm.js)
node@10.2.1 (/usr/local/Cellar/node/10.2.1/bin/node)
npminstall@3.6.2 (/usr/local/lib/node_modules/cnpm/node_modules/_npminstall@3.6.2@npminstall/lib/index.js)
prefix=/usr/local
darwin x64 17.6.0
registry=https://registry.npm.taobao.org
faner@MBP-FAN:~|⇒
```

### 升级 typescript

执行 `cnpm outdated -g` 或 `cnpm outdated -g typescript` 命令，检测到 typescript 过期后，可执行 `cnpm up -g typescript` 进行升级：

```shell
faner@MBP-FAN:~|⇒  cnpm up -g typescript
/usr/local/bin/tsc -> /usr/local/lib/node_modules/typescript/bin/tsc
/usr/local/bin/tsserver -> /usr/local/lib/node_modules/typescript/bin/tsserver
+ typescript@2.9.1
updated 1 package in 2.984s
```

> 类似升级 **npm**：`cnpm up npm -g`

### 升级 whistle

检测到 whistle 过期后，执行 `cnpm up -g whistle` 升级报错文件目录已存在（EEXIST）导致 mkdir 失败：

```shell
faner@MBP-FAN:~|⇒  cnpm up whistle -g
npm ERR! path /usr/local/lib/node_modules/whistle/node_modules/concat-stream
npm ERR! code EEXIST
npm ERR! errno -17
npm ERR! syscall mkdir
npm ERR! EEXIST: file already exists, mkdir '/usr/local/lib/node_modules/whistle/node_modules/concat-stream'
npm ERR! File exists: /usr/local/lib/node_modules/whistle/node_modules/concat-stream
npm ERR! Move it away, and try again.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/faner/.npm/_logs/2018-08-20T22_26_09_101Z-debug.log
```

可根据提示先执行 `rm -rf /usr/local/lib/node_modules/whistle/node_modules/concat-stream` 移除该目录，再尝试执行 update 命令。

---

当然，也可以执行原始安装命令重新覆盖安装，达到升级的目的：**`cnpm i -g whistle`**。

```shell
faner@MBP-FAN:~|⇒  cnpm i whistle -g
Downloading whistle to /usr/local/lib/node_modules/whistle_tmp
Copying /usr/local/lib/node_modules/whistle_tmp/_whistle@1.12.1@whistle to /usr/local/lib/node_modules/whistle
Installing whistle's dependencies to /usr/local/lib/node_modules/whistle/node_modules

[1/28] adm-zip@0.4.11 installed at node_modules/_adm-zip@0.4.11@adm-zip
[2/28] extend@^3.0.1 installed at node_modules/_extend@3.0.2@extend
[3/28] cookie@^0.3.1 installed at node_modules/_cookie@0.3.1@cookie
[4/28] colors@1.1.2 installed at node_modules/_colors@1.1.2@colors
...
[25/28] starting@^4.0.1 installed at node_modules/_starting@4.0.3@starting
[26/28] express@4.12.3 installed at node_modules/_express@4.12.3@express
[27/28] xml2js@0.4.17 installed at node_modules/_xml2js@0.4.17@xml2js
[28/28] weinre2@^1.1.0 installed at node_modules/_weinre2@1.1.0@weinre2

All packages installed (124 packages installed from npm registry, used 2s(network 2s), speed 2.62MB/s, json 104(737.57kB), tarball 4.1MB)
[whistle@1.12.1] link /usr/local/bin/whistle@ -> /usr/local/lib/node_modules/whistle/bin/whistle.js
[whistle@1.12.1] link /usr/local/bin/w2@ -> /usr/local/lib/node_modules/whistle/bin/whistle.js
[whistle@1.12.1] link /usr/local/bin/wproxy@ -> /usr/local/lib/node_modules/whistle/bin/whistle.js
```

## [npm-uninstall](https://docs.npmjs.com/cli/uninstall)

Remove a package

```
npm uninstall [<@scope>/]<pkg>[@<version>]... [-S|--save|-D|--save-dev|-O|--save-optional|--no-save]

aliases: remove, rm, r, un, unlink
```
