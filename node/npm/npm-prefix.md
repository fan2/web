
## [npm-prefix](https://docs.npmjs.com/cli/prefix)

`npm prefix [-g]` - Print the local prefix to standard out. 

This is the closest parent directory to contain a `package.json` file unless **-g** is also specified.  
If **-g** is specified, this will be the value of the global prefix.  

参考 [prefix Configuration](https://docs.npmjs.com/files/folders#prefix-configuration)

> [How to get the npm global path prefix](https://stackoverflow.com/questions/18383476/how-to-get-the-npm-global-path-prefix)  
> [How to change the npm prefix without config?](https://stackoverflow.com/questions/40178366/how-to-change-the-npm-prefix-without-config)  
> [`npm config get prefix` takes incredibly long](https://github.com/npm/npm/issues/14458)  

### npm

```shell
faner@MBP-FAN:~|⇒  npm prefix
/Users/faner
faner@MBP-FAN:~|⇒  npm prefix -g
/usr/local
```

```shell
faner@MBP-FAN:~|⇒  npm config get prefix
/usr/local
faner@MBP-FAN:~|⇒  npm config get prefix -g
/usr/local
```

### cnpm

```shell
faner@MBP-FAN:~|⇒  cnpm prefix
/Users/faner
faner@MBP-FAN:~|⇒  cnpm prefix -g
/usr/local/Cellar/node/10.2.1
```

```shell
faner@MBP-FAN:~|⇒  cnpm config get prefix
/usr/local
faner@MBP-FAN:~|⇒  cnpm config get prefix -g
/usr/local
```

#### cnpm 修正 prefix

[**npm extraneous error 经历**](http://www.skyjia.com/2017/05/05/npm-error-extraneous/)  

```shell
faner@MBP-FAN:~|⇒  cnpm config set prefix "/usr/local"
```

该配置会写入 cnpm 的 userconfig 文件（`~/.cnpmrc`）：

```shell
faner@MBP-FAN:~|⇒  cat .cnpmrc
prefix=/usr/local
```

```shell
faner@MBP-FAN:~|⇒  cnpm config get prefix
/usr/local
faner@MBP-FAN:~|⇒  cnpm config get prefix -g
/usr/local
```

修正后，cnpm 的 `globalconfig` 和 `globalignorefile` 这两项与标准 npm 对齐。  
`npm list --depth=0` 和 `cnpm list --depth=0` 的输出相同；`npm list -g --depth=0` 和 `cnpm list -g --depth=0` 的输出相同。  

## [npm-root](https://docs.npmjs.com/cli/root)

`npm root [-g]` - Print the effective **node_modules** folder to standard out.

参考 [Node Modules](https://docs.npmjs.com/files/folders#node-modules)

> [npm: How to reset the node_modules prefix](https://stackoverflow.com/questions/37239120/npm-how-to-reset-the-node-modules-prefix)  
> [How to find search/find npm packages](https://stackoverflow.com/questions/10568512/how-to-find-search-find-npm-packages)  
> [How to list npm user-installed packages?](https://stackoverflow.com/questions/17937960/how-to-list-npm-user-installed-packages)  

### npm

```shell
faner@MBP-FAN:~|⇒  npm root
/Users/faner/node_modules
faner@MBP-FAN:~|⇒  npm root -g
/usr/local/lib/node_modules
```

- 执行 `npm install` 的当前用户安装路径：`~/node_modules`；  
- 执行 `npm install -g` 的全局安装路径：`/usr/local/lib/node_modules`；  

具体某个包的依赖包路径：

* `/usr/local/lib/node_modules/npm/node_modules`
* `/usr/local/lib/node_modules/cnpm/node_modules`
* `/usr/local/lib/node_modules/whistle/node_modules`

### cnpm

```shell
faner@MBP-FAN:~|⇒  cnpm root
/Users/faner/node_modules
faner@MBP-FAN:~|⇒  cnpm root -g
/usr/local/Cellar/node/10.2.1/lib/node_modules
```

cnpm 修正 prefix 后，`cnpm root -g` 位置同 `npm root -g`：

```shell
faner@MBP-FAN:~|⇒  cat .cnpmrc
prefix=/usr/local
faner@MBP-FAN:~|⇒  cnpm root -g
/usr/local/lib/node_modules
```

## [npm-bin](https://docs.npmjs.com/cli/bin)

`npm bin [-g|--global]` - Print the folder where npm will install executables.

### npm

```shell
faner@MBP-FAN:~|⇒  npm bin
/Users/faner/node_modules/.bin

faner@MBP-FAN:~|⇒  npm bin -g
/usr/local/bin
```

### cnpm

```shell
faner@MBP-FAN:~|⇒  cnpm bin
/Users/faner/node_modules/.bin

faner@MBP-FAN:~|⇒  cnpm bin -g
/usr/local/Cellar/node/10.2.1/bin
(not in PATH env variable)
```

cnpm 修正 prefix 后，`cnpm bin -g` 位置同 `npm bin -g`：

```shell
faner@MBP-FAN:~|⇒  cat .cnpmrc
prefix=/usr/local
faner@MBP-FAN:~|⇒  cnpm bin -g
/usr/local/bin
```
