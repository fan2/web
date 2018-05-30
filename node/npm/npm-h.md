## node

```shell
faner@MBP-FAN:~|⇒  node -v
v10.1.0

faner@MBP-FAN:~|⇒  which node
/usr/local/bin/node

faner@MBP-FAN:~|⇒  type -a node
node is /usr/local/bin/node

faner@MBP-FAN:~|⇒  ls -al `which node`
lrwxr-xr-x  1 faner  admin  30 May 12 20:32 /usr/local/bin/node -> ../Cellar/node/10.1.0/bin/node
```

## npm

```shell
faner@MBP-FAN:~|⇒  npm -v
6.1.0

faner@MBP-FAN:~|⇒  which npm
/usr/local/bin/npm

faner@MBP-FAN:~|⇒  type -a npm
npm is /usr/local/bin/npm

faner@MBP-FAN:~|⇒  ls -al `which npm`
lrwxr-xr-x  1 faner  admin  38 May 24 06:38 /usr/local/bin/npm -> ../lib/node_modules/npm/bin/npm-cli.js
```

### npm -h

```shell
faner@MBP-FAN:~|⇒  npm -h

Usage: npm <command>

where <command> is one of:
    access, adduser, audit, bin, bugs, c, cache, ci, cit,
    completion, config, create, ddp, dedupe, deprecate,
    dist-tag, docs, doctor, edit, explore, get, help,
    help-search, hook, i, init, install, install-test, it, link,
    list, ln, login, logout, ls, outdated, owner, pack, ping,
    prefix, profile, prune, publish, rb, rebuild, repo, restart,
    root, run, run-script, s, se, search, set, shrinkwrap, star,
    stars, start, stop, t, team, test, token, tst, un,
    uninstall, unpublish, unstar, up, update, v, version, view,
    whoami

npm <command> -h     quick help on <command>
npm -l           display full usage info
npm help <term>  search for help on <term>
npm help npm     involved overview

Specify configs in the ini-formatted file:
    /Users/faner/.npmrc
or on the command line via: npm <command> --key value
Config info can be viewed via: npm help config

npm@6.1.0 /usr/local/lib/node_modules/npm
```

模块：`/usr/local/lib/node_modules/npm`  
配置：`/Users/faner/.npmrc`  

## [cnpm](http://npm.taobao.org/)

In China, you can install whistle using npm mirror of taobao to speed up installing progress and avoid failure：

> [tnpm /cnpm 安装报错](https://segmentfault.com/q/1010000009008062)  
> [nodejs linux 环境设置 tnpm 安装](https://blog.csdn.net/lilei_ndsc/article/details/52190010)  

执行 npm 命令时，指定 `--registry` 参数，从 cnpm 镜像源安装：

```shell
# or specify mirror install directly：
npm install whistle -g --registry=https://registry.npm.taobao.org
```

或用 npm 安装 cnpm，然后用 cnpm 命令替代 npm：

```shell
faner@MBP-FAN:~|⇒  npm install cnpm -g --registry=https://registry.npm.taobao.org

faner@MBP-FAN:~|⇒  cnpm -v
cnpm@6.0.0 (/usr/local/lib/node_modules/cnpm/lib/parse_argv.js)
npm@6.1.0 (/usr/local/lib/node_modules/cnpm/node_modules/_npm@6.1.0@npm/lib/npm.js)
node@10.2.1 (/usr/local/Cellar/node/10.2.1/bin/node)
npminstall@3.6.2 (/usr/local/lib/node_modules/cnpm/node_modules/_npminstall@3.6.2@npminstall/lib/index.js)
prefix=/usr/local
darwin x64 17.6.0
registry=https://registry.npm.taobao.org

cnpm install -g whistle
```

模块：`/usr/local/lib/node_modules/cnpm`  

[**npm extraneous error**](http://www.skyjia.com/2017/05/05/npm-error-extraneous/) ：由于 Homebrew 管理的 node 会经常升级更新，并且 cnpm 默认会将 package 安装到当前运行版本的 node 安装文件夹之中，这个默认行为会在 node 再次升级后导致已安装的全局 packag e失效。因此，我们需要手动修改 npm 的 prefix 设置。

### cnpm -h

```shell
faner@MBP-FAN:~|⇒  cnpm -h

  Usage: cnpm [options]

  Options:

    -h, --help                       output usage information
    -v, --version                    show full versions
    -r, --registry [registry]        registry url, default is https://registry.npm.taobao.org
    -w, --registryweb [registryweb]  web url, default is https://npm.taobao.org
    --disturl [disturl]              dist url for node-gyp, default is https://npm.taobao.org/mirrors/node
    -c, --cache [cache]              cache folder, default is /Users/faner/.cnpm
    -u, --userconfig [userconfig]    userconfig file, default is /Users/faner/.cnpmrc
    -y, --yes                        yes all confirm
    --ignore-custom-config           ignore custom .cnpmrc
    --proxy [proxy]                  set a http proxy, no default

Usage: cnpm [option] <command>
Help: http://cnpmjs.org/help/cnpm

  Extend command
    web                            open cnpm web (ex.: cnpm web)
    check [ingoreupdate]           check project dependencies, add ignoreupdate will not check modules' latest version(ex.: cnpm check, cnpm check -i)
    doc [moduleName]               open document page (ex.: cnpm doc urllib)
    sync [moduleName]              sync module from source npm (ex.: cnpm sync urllib)
    user [username]                open user profile page (ex.: cnpm user fengmk2)

  npm command use --registry=https://registry.npm.taobao.org
    where <command> is one of:
    add-user, adduser, apihelp, author, bin, bugs, c, cache,
    completion, config, ddp, dedupe, deprecate, docs, edit,
    explore, faq, find, find-dupes, get, help, help-search,
    home, i, info, init, install, isntall, la, link, list, ll,
    ln, login, ls, outdated, owner, pack, prefix, prune,
    publish, r, rb, rebuild, remove, restart, rm, root,
    run-script, s, se, search, set, show, shrinkwrap, star,
    start, stop, submodule, tag, test, tst, un, uninstall,
    unlink, unpublish, unstar, up, update, v, version, view,
    whoami
      npm <cmd> -h     quick help on <cmd>
      npm -l           display full usage info
      npm faq          commonly asked questions
      npm help <term>  search for help on <term>
      npm help npm     involved overview

      Specify configs in the ini-formatted file:
          /Users/faner/.cnpmrc
      or on the command line via: npm <command> --key value
      Config info can be viewed via: npm help config
```

配置：`/Users/faner/.cnpmrc`  
