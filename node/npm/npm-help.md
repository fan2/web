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

## npm help

```shell
# cnpm help
faner@MBP-FAN:~|⇒  npm help

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
    /Users/faner/.cnpmrc
or on the command line via: npm <command> --key value
Config info can be viewed via: npm help config

npm@6.2.0 /usr/local/lib/node_modules/cnpm/node_modules/_npm@6.2.0@npm
```

模块：`/usr/local/lib/node_modules/npm`  
配置：`/Users/faner/.npmrc`  

### help command

执行 `npm help <command>` 可查看具体子命令的帮助说明。

执行 `npm help config` 查看 npm config 命令帮助：

```shell
NAME
       npm-config - Manage the npm configuration files

SYNOPSIS
         npm config set <key> <value> [-g|--global]
         npm config get <key>
         npm config delete <key>
         npm config list [-l] [--json]
         npm config edit
         npm get <key>
         npm set <key> <value> [-g|--global]

         aliases: c

SEE ALSO
       o npm help 5 folders
       o npm help 7 config
       o npm help 5 package.json
       o npm help 5 npmrc
       o npm help npm
```

> 根据 `SEE ALSO` 部分的提示可以查看更多详细帮助。

执行 `npm help list` 查看 npm list 命令帮助：

```shell
NAME
       npm-ls - List installed packages

SYNOPSIS
         npm ls [[<@scope>/]<pkg> ...]

         aliases: list, la, ll


SEE ALSO
       o npm help config
       o npm help 7 config
       o npm help 5 npmrc
       o npm help 5 folders
       o npm help install
       o npm help link
       o npm help prune
       o npm help outdated
       o npm help update
```

> 根据 `SEE ALSO` 部分的提示可以查看更多详细帮助。

### command alias

- `config` = c  
- `dedupe` = ddp  
- `install` = i  
- `link` = ln  
- `list` = ls,la/ll  
- `update` = up  
- `uninstall` = un/unlink  
- `remove` = r/rm，等效于 uninstall 命令  
