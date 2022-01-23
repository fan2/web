
## npm

查看默认的 npm 软件源 registry：

```
faner@MBP-FAN:~|⇒  npm config get registry
https://registry.npmjs.org/
```

npm 默认的镜像源站点 registry.npmjs.org 在国外，国内的访问速度特别慢。

## cnpm

[中国 NPM 镜像](https://npmmirror.com/)（前身为淘宝 [cnpm](https://npm.taobao.org/)）是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。

以下介绍三种使用 cnpm 的方式。

### --registry

在执行 npm install 命令时，通过 `--registry` 参数临时指定从 cnpm 镜像源安装：

```shell
# or specify mirror install directly：
npm install whistle -g --registry=https://registry.npmmirror.com
```

### alias

或者通过添加 npm 参数 alias 一个新命令 cnpm（仅在当前 zsh 窗口生效）:

```Shell
$ alias cnpm="npm --registry=https://registry.npmmirror.com \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npmmirror.com/dist \
--userconfig=$HOME/.cnpmrc"
```

也可考虑将该 alias 命令写入 .zshrc，每次打开终端窗口加载 zsh 都生效：

```
# Or alias it in .bashrc or .zshrc
$ echo '\n#alias for cnpm\nalias cnpm="npm --registry=https://registry.npmmirror.com \
  --cache=$HOME/.npm/.cache/cnpm \
  --disturl=https://npmmirror.com/dist \
  --userconfig=$HOME/.cnpmrc"' >> ~/.zshrc && source ~/.zshrc
```

### registry

也可以通过 npm config 命令全局替换默认的镜像源为 cnpm：

```
npm config set registry="https://registry.npmmirror.com"
```

### command

也可考虑用 npm 命令从指定像源安装 cnpm 替代 npm 使用。

```shell
npm install cnpm -g --registry=https://registry.npmmirror.com
```

cnpm 配置文件位置为 `~/.cnpmrc`，执行 `cnpm -v` 可查看版本信息，执行 `cnpm -h` 可查看帮助。

之后日常即可用 cnpm 替代 npm，以下使用 cnpm 安装 whistle：

```shell
[c]npm install -g whistle
```

## tnpm

也可考虑腾讯云搭建的 [tnpm](https://mirrors.cloud.tencent.com/help/npm.html)，可选使用方式参考 cnpm。

1. 可以修改npm软件源的registry：

```
npm config set registry https://mirrors.tencent.com/npm/
```

2. 如果希望保留默认外网能力，不修改 registry，也可以做一个 alias 命令，仅通过它使用 tnpm 软件源。

```
alias tnpm="npm --registry https://mirrors.tencent.com/npm/"
```

> 建议将该 alias 命令写入 ~/.zshrc 配置文件，这样每次启动zsh就已经准备好关联替身。

## refs

In China, you can install whistle npm mirror of taobao to speed up installing progress and avoid failure：

> [tnpm /cnpm 安装报错](https://segmentfault.com/q/1010000009008062)  
> [nodejs linux 环境设置 tnpm 安装](https://blog.csdn.net/lilei_ndsc/article/details/52190010)  

模块：`/usr/local/lib/node_modules/cnpm`  

[**npm extraneous error**](http://www.skyjia.com/2017/05/05/npm-error-extraneous/) ：由于 Homebrew 管理的 node 会经常升级更新，并且 cnpm 默认会将 package 安装到当前运行版本的 node 安装文件夹之中，这个默认行为会在 node 再次升级后导致已安装的全局 packag e失效。因此，我们需要手动修改 npm 的 prefix 设置。
