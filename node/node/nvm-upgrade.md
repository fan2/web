# upgrade from v10.14.1 to v10.15.3

## 查看可用 lts 版本

查看当前 node/npm 版本号：

```
faner on MBP-FAN in ~
$ node -v
v10.14.1
faner on MBP-FAN in ~
$ npm -v
6.4.1
```

查看当前最新的 lts 版本：

```
#$ nvm ls-remote v10 --lts
faner on MBP-FAN in ~
$ nvm ls-remote --lts | grep 'Latest'
         v4.9.1   (Latest LTS: Argon)
        v6.17.0   (Latest LTS: Boron)
        v8.15.1   (Latest LTS: Carbon)
->     v10.15.3   (Latest LTS: Dubnium)

# 暂时没有 Node 11
faner on MBP-FAN in ~
$ nvm ls-remote v11 --lts
            N/A
```

执行 `nvm install 10.15.3 --latest-npm --reinstall-packages-from=v10.14.1` 升级最新 node/npm，并重装 v10.14.1 的安装包。

下面分解为三步执行：

1. `nvm install 10.15.3`；  
2. `nvm install-latest-npm`；  
3. `nvm reinstall-packages v10.14.1`；  

## 安装最新的 node 10.15.3

```
faner on MBP-FAN in ~
$ nvm install 10.15.3
Downloading and installing node v10.15.3...
Downloading https://nodejs.org/dist/v10.15.3/node-v10.15.3-darwin-x64.tar.xz...
######################################################################## 100.0%
Computing checksum with shasum -a 256
Checksums matched!
Now using node v10.15.3 (npm v6.4.1)

faner on MBP-FAN in ~
$ node -v
v10.15.3
```

## 安装最新的 npm 6.9.0

```
faner on MBP-FAN in ~
$ nvm install-latest-npm
Attempting to upgrade to the latest working version of npm...
* Installing latest `npm`; if this does not work on your node version, please report a bug!
/Users/faner/.nvm/versions/node/v10.15.3/bin/npm -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/npm/bin/npm-cli.js
/Users/faner/.nvm/versions/node/v10.15.3/bin/npx -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/npm/bin/npx-cli.js
+ npm@6.9.0
added 54 packages from 9 contributors, removed 15 packages and updated 47 packages in 5.742s
* npm upgraded to: v6.9.0

faner on MBP-FAN in ~
$ npm -v
6.9.0
```

## 重新安装 npm packages

```
$ nvm reinstall-packages v10.14.1
Reinstalling global packages from v10.14.1...
npm WARN deprecated socks@1.1.10: If using 2.x branch, please upgrade to at least 2.1.6 to avoid a serious bug with socket data flow and an import issue introduced in 2.1.0
/Users/faner/.nvm/versions/node/v10.15.3/bin/cnpm -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/cnpm/bin/cnpm
/Users/faner/.nvm/versions/node/v10.15.3/bin/eslint -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/eslint/bin/eslint.js
/Users/faner/.nvm/versions/node/v10.15.3/bin/tslint -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/tslint/bin/tslint
/Users/faner/.nvm/versions/node/v10.15.3/bin/tsc -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/typescript/bin/tsc
/Users/faner/.nvm/versions/node/v10.15.3/bin/tsserver -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/typescript/bin/tsserver
/Users/faner/.nvm/versions/node/v10.15.3/bin/w2 -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/whistle/bin/whistle.js
/Users/faner/.nvm/versions/node/v10.15.3/bin/wproxy -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/whistle/bin/whistle.js
/Users/faner/.nvm/versions/node/v10.15.3/bin/whistle -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/whistle/bin/whistle.js
+ cnpm@6.0.0
+ tslint@5.11.0
+ eslint@5.9.0
+ whistle@1.13.5
+ typescript@3.2.1
added 980 packages from 1036 contributors in 17.805s
Linking global packages from v10.14.1...
No linked global packages found...

faner on MBP-FAN in ~
$ npm ls -g --depth=0
/Users/faner/.nvm/versions/node/v10.15.3/lib
├── cnpm@6.0.0
├── eslint@5.9.0
├── npm@6.4.1
├── tslint@5.11.0
├── typescript@3.2.1
└── whistle@1.13.5
```

## npm ERR! Cannot read property 'length' of undefined

升级 node/npm 后，执行 `npm outdated -g` 报错 `npm ERR! Cannot read property 'length' of undefined`：

```
faner on MBP-FAN in ~
$ npm outdated -g
npm ERR! Cannot read property 'length' of undefined

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/faner/.npm/_logs/2019-04-01T23_13_37_951Z-debug.log
```

打开日志文件 `2019-04-01T23_13_37_951Z-debug.log` 中的 verbose stack 显示 `~/.nvm/versions/node/v10.15.3/lib/node_modules/npm/node_modules/text-table/index.js` 中的 dotindex、reduce、forEach 等函数引用了传参未定义的 length 属性。

参考 [npm outdated error Cannot read property 'length' of undefined](https://stackoverflow.com/questions/55440912/npm-outdated-error-cannot-read-property-length-of-undefined)，执行 `npm -g i npm@next` 安装 npm 实验版本解决问题：

```
faner on MBP-FAN in ~
$ npm -g i npm@next
/Users/faner/.nvm/versions/node/v10.15.3/bin/npm -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/npm/bin/npm-cli.js
/Users/faner/.nvm/versions/node/v10.15.3/bin/npx -> /Users/faner/.nvm/versions/node/v10.15.3/lib/node_modules/npm/bin/npx-cli.js
+ npm@6.9.1-next.0
removed 2 packages and updated 4 packages in 5.592s

faner on MBP-FAN in ~
$ npm -v
6.9.1-next.0
```

重新输入 `npm outdated -g` 显示正常：

```
faner on MBP-FAN in ~
$ npm outdated -g
Package          Current        Wanted   Latest  Location
eslint             5.9.0        5.16.0   5.16.0  global
npm         6.9.1-next.0  6.9.1-next.0    6.9.0  global
tslint            5.11.0        5.15.0   5.15.0  global
typescript         3.2.1         3.4.1    3.4.1  global
whistle           1.13.5       1.13.25  1.13.25  global
```

执行 `npm up -g` 升级所有的全局安装包。

**相关参考**：

- [Error: EPERM: operation not permitted,TypeError: Cannot read property 'get' of undefined](https://blog.csdn.net/lgysjfs/article/details/83007010)  
- [npm ERR! Cannot read property 'match' of undefined](https://blog.csdn.net/Jane_96/article/details/81451759)  
- [NPM ERR! Cannot read property 'length' of undefined #19265](https://github.com/npm/npm/issues/19265)  
- [npm outdated -g fail with Cannot read property ‘length’ of undefined](https://npm.community/t/npm-outdated-g-fail-with-cannot-read-property-length-of-undefined/5988)  
