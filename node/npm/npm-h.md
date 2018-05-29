## npm

```shell
faner@MBP-FAN:~|⇒  npm -v
6.1.0
```

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

## cnpm

```shell
faner@MBP-FAN:~|⇒  cnpm -v
cnpm@5.3.0 (/usr/local/lib/node_modules/cnpm/lib/parse_argv.js)
npm@5.10.0 (/usr/local/lib/node_modules/cnpm/node_modules/npm/lib/npm.js)
node@10.2.1 (/usr/local/Cellar/node/10.2.1/bin/node)
npminstall@3.6.2 (/usr/local/lib/node_modules/cnpm/node_modules/npminstall/lib/index.js)
prefix=/usr/local
darwin x64 17.6.0
registry=https://registry.npm.taobao.org
```

模块：`/usr/local/lib/node_modules/cnpm`  

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
