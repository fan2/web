[npm-config](https://docs.npmjs.com/misc/config)  / [misc](https://docs.npmjs.com/misc/config)  

```shell
npm config set <key> <value> [-g|--global]
npm config get <key>
npm config delete <key>
npm config list [-l] [--json]
npm config edit
npm get <key>
npm set <key> <value> [-g|--global]

aliases: c
```

npm gets its config settings from the command line, environment variables, **`npmrc`** files, and in some cases, the **`package.json`** file.

The **`npm config`** command can be used to update and edit the contents of the user and global npmrc files.

## npmrc

The four relevant files are:

1. per-project config file (`/path/to/my/project/.npmrc`)  
2. per-user config file (`~/.npmrc`)  
3. global config file (`$PREFIX/etc/npmrc`)  
4. npm builtin config file (`/path/to/npm/npmrc`)  

All npm config files are an ini-formatted list of key = value parameters. Environment variables can be replaced using `${VARIABLE_NAME}`. For example:

```ini
prefix = ${HOME}/.npm-packages
```

## npm proxy

`npm config set proxy http://proxy.company.com:8080` 设置代理会写入 `~/.npmrc`：

```shell
ifan@FAN-MC1:~|⇒  cat .npmrc
proxy=http://proxy.company.com:8080
```

## npm registry

执行 `npm config get registry` 查看默认的 registry：

```
faner@MBP-FAN:~|⇒  npm config get registry
https://registry.npmjs.org/
```

npm 默认的镜像源站点 `https://registry.npmjs.org/` 在国外，国内的访问速度特别慢。
建议修改默认的镜像源为淘宝 cnpm：

```
npm config set registry="https://registry.npm.taobao.org/"
```

也可考虑安装 cnpm 命令，替代 npm。