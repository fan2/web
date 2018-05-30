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

安装 whistle：`npm install -g whistle`；  
同时安装 tslint 和 typescript：`cnpm install -g tslint typescript`；  


### npm i npm -g 升级 npm

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

以上执行 `npm config get prefix` 提示 npm 有可更新版本，也可执行 `[c]npm outdated -g` 或 `[c]npm outdated -g npm` 检测 npm 是否过期。

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

而应执行 `npm i npm -g` 全局升级 npm。

```
faner@MBP-FAN:~|⇒ npm i npm -g
/usr/local/bin/npm -> /usr/local/lib/node_modules/npm/bin/npm-cli.js
/usr/local/bin/npx -> /usr/local/lib/node_modules/npm/bin/npx-cli.js
+ npm@6.1.0
added 247 packages, removed 41 packages and updated 129 packages in 9.802s

faner@MBP-FAN:~|⇒ npm -v
6.1.0
```

> 最好不要执行 `npm i npm -g` 升级 npm，而应该走 `brew update/upgrade` 随带 node 升级 npm？  
> 也可执行 `cnpm i npm -g`？  

### cnpm i cnpm -g 升级 cnpm

执行 `cnpm outdated -g` 或 `cnpm outdated -g cnpm` 检测 cnpm 是否过期：

```shell
faner@MBP-FAN:~|⇒  cnpm -v
cnpm@5.3.0 (/usr/local/lib/node_modules/cnpm/lib/parse_argv.js)
npm@5.10.0 (/usr/local/lib/node_modules/cnpm/node_modules/npm/lib/npm.js)
node@10.2.1 (/usr/local/Cellar/node/10.2.1/bin/node)
npminstall@3.6.2 (/usr/local/lib/node_modules/cnpm/node_modules/npminstall/lib/index.js)
prefix=/usr/local
darwin x64 17.6.0
registry=https://registry.npm.taobao.org

# cnpm outdated -g
faner@MBP-FAN:~|⇒  npm outdated -g --registry=https://registry.npm.taobao.org
Package  Current  Wanted  Latest  Location
cnpm       5.3.0   5.3.0   6.0.0
```

执行 `cnpm i cnpm -g` 升级 cnmp 自身：

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



## [npm-outdated](https://docs.npmjs.com/cli/outdated)

Check for outdated packages

```
npm outdated [[<@scope>/]<pkg> ...]
```

This command will check the registry to see if any (or, specific) installed packages are currently outdated.

基于淘宝 cnpm 源检测过期：

```shell
# cnpm outdated -g
npm outdated -g --registry=https://registry.npm.taobao.org
```

基于淘宝 cnpm 源检测具体某个 package 是否过期：`cnpm outdated -g whistle`

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

基于淘宝 cnpm 源更新过期：

```shell
# cnpm update -g
npm update -g --registry=https://registry.npm.taobao.org
```

基于淘宝 cnpm 源更新具体某个过期的 package：`cnpm outdated -g whistle`

## [npm-uninstall](https://docs.npmjs.com/cli/uninstall)

Remove a package

```
npm uninstall [<@scope>/]<pkg>[@<version>]... [-S|--save|-D|--save-dev|-O|--save-optional|--no-save]

aliases: remove, rm, r, un, unlink
```
