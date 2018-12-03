
无论是 windows 还是 macOS，都建议安装 **nvm**，通过 nvm 来安装切换管理配置 node 版本。

[NVM](https://github.com/creationix/nvm): Node Version Manager

Manage multiple Node.js versions

## [nvm-windows](https://github.com/coreybutler/nvm-windows)

[Windows上安装nodejs版本管理器nvm](https://www.jianshu.com/p/324044f2f542)  

[Windows 下安装 nvm 管理 nodejs 版本](https://segmentfault.com/a/1190000007612011)  

**`nvm node_mirror [url]`**：设置node镜像，默认为 `https://nodejs.org/dist/`

> 建议设置为淘宝的镜像 `https://npm.taobao.org/mirrors/node/`

**`nvm npm_mirror [url]`**：设置npm镜像，默认为 `https://github.com/npm/npm/archive/`

> 建议设置为淘宝的镜像 `https://npm.taobao.org/mirrors/npm/`

## nvm（macOS）

`brew search nvm`: 搜索 nvm 包；  
`brew info nvm`: 查看 nvm 包信息；  
`brew install nvm`: 安装 nvm。  

### config

nvm 的 Caveats 信息：

```
==> Caveats
Please note that upstream has asked us to make explicit managing
nvm via Homebrew is unsupported by them and you should check any
problems against the standard nvm install method prior to reporting.

You should create NVM's working directory if it doesn't exist:

  mkdir ~/.nvm

Add the following to ~/.zshrc or your desired shell
configuration file:

  export NVM_DIR="$HOME/.nvm"
  . "/usr/local/opt/nvm/nvm.sh"

You can set $NVM_DIR to any location, but leaving it unchanged from
/usr/local/opt/nvm will destroy any nvm-installed Node installations
upon upgrade/reinstall.
```

根据 Caveats 信息，还得执行以下两步才能完成安装：

1. 执行 `mkdir ~/.nvm`，创建 `.nvm` 目录。  
2. 在 `~/.zshrc` 下添加以下两行：

```
export NVM_DIR="$HOME/.nvm"
. "/usr/local/opt/nvm/nvm.sh"
```

执行 `echo $NVM_DIR`：

```
> echo $NVM_DIR
/Users/faner/.nvm
```

执行 `nvm unload` 可从 shell 卸载 nvm（Unload `nvm` from shell）。

### mirrors

[nvm 设置下载 node 的镜像地址](https://github.com/xhlwill/blog/issues/7)

macOS 和 linux 版 nvm 没有 node_mirror/npm_mirror 这两个命令，设置 node 镜像地址的方式是：

```
export NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist
```

执行 `vim /usr/local/opt/nvm/nvm.sh` 查看 nvm.sh：

```shell
faner@MBP-FAN ~
0 % vim /usr/local/opt/nvm/nvm.sh
```

其中定义了 nvm_get_mirror 函数：

```shell
nvm_get_mirror() {
  case "${1}-${2}" in
    node-std) nvm_echo "${NVM_NODEJS_ORG_MIRROR:-https://nodejs.org/dist}" ;;
    iojs-std) nvm_echo "${NVM_IOJS_ORG_MIRROR:-https://iojs.org/dist}" ;;
    *)
      nvm_err 'unknown type of node.js or io.js release'
      return 1
    ;;
  esac
}
```

[Change NVM_NODEJS_ORG_MIRROR to NODEJS_ORG_MIRROR to solve npm install error](https://github.com/nodejs/node-gyp/issues/942)

[修改nvm镜像地址](https://www.cnblogs.com/lonny/p/NVM_NODEJS_ORG_MIRROR.html)  
[nvm 使用淘宝镜像](https://www.chenky.com/archives/746)  

```
export NODEJS_ORG_MIRROR=http://npm.taobao.org/mirrors/node
```

### uninstall

执行 `nvm -h` 查看帮助：

```
> nvm -h

Node Version Manager

Note:
  to remove, delete, or uninstall nvm - just remove the `$NVM_DIR` folder (usually `~/.nvm`)
```

要卸载 nvm 只需要简单的删除 `$NVM_DIR`(`~/.nvm`) 目录即可。

### usage

执行 `nvm -h`(``nvm --help``) 可查看 nvm 帮助。

相关命令中的 `<version>` 中的 `v` 一般可省略。

相关命令中的 `--lts` 表示 LTS (long-term support) 版本。

#### nvm ls-remote

```
nvm ls-remote                             List remote versions available for install
nvm ls-remote <version>                   List remote versions available for install, matching a given <version>
```

列出所有支持的 node 版本。

为了避免从 `0.*` 开始的早期版本罗列过长，可以指定只查看指定（主）版本的列表：

- `nvm ls-remote v10`：列举 node 10 的所有版本；  
- `nvm ls-remote 11`：列举 node 11 的所有版本。  

#### install

```
  nvm install [-s] <version>                Download and install a <version>, [-s] from source. Uses .nvmrc if available
    --reinstall-packages-from=<version>     When installing, reinstall packages installed in <node|iojs|node version number>
    --lts                                   When installing, only select from LTS (long-term support) versions
    --lts=<LTS name>                        When installing, only select from versions for a specific LTS line
    --skip-default-packages                 When installing, skip the default-packages file if it exists
    --latest-npm                            After installing, attempt to upgrade to the latest working npm on the given node version
```

**`nvm install <version>`**： 安装指定版本的 node。

- `nvm install 10.13.0` 安装 node 10.13.0。

```
 faner@MBP-FAN  ~  nvm install 10.13.0
Downloading and installing node v10.13.0...
Downloading http://npm.taobao.org/mirrors/node//v10.13.0/node-v10.13.0-darwin-x64.tar.xz...
######################################################################## 100.0%
Computing checksum with shasum -a 256
Checksums matched!
nvm is not compatible with the npm config "prefix" option: currently set to "/usr/local"
Run `npm config delete prefix` or `nvm use --delete-prefix v10.13.0` to unset it.
```

```
➜  ~  node -v
zsh: command not found: node

➜  ~  npm -v
env: node: No such file or directory

➜  ~  nvm ls
       v10.13.0
node -> stable (-> v10.13.0) (default)
stable -> 10.13 (-> v10.13.0) (default)
iojs -> N/A (default)
lts/* -> lts/dubnium (-> v10.13.0)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.14.4 (-> N/A)
lts/carbon -> v8.13.0 (-> N/A)
lts/dubnium -> v10.13.0

➜  ~  nvm use 10.13.0
nvm is not compatible with the npm config "prefix" option: currently set to "/usr/local"
Run `npm config delete prefix` or `nvm use --delete-prefix v10.13.0` to unset it.

➜  ~  npm config delete prefix
env: node: No such file or directory

➜  ~  nvm use --delete-prefix v10.13.0
Now using node v10.13.0 (npm v6.4.1)
```

原来后面三个值都为 `/usr/local`，现在变为了 `/Users/faner/.nvm/versions/node/v10.13.0`：

```
➜  ~  npm prefix
/Users/faner
➜  ~  npm prefix -g
/Users/faner/.nvm/versions/node/v10.13.0
➜  ~  npm config get prefix
/Users/faner/.nvm/versions/node/v10.13.0
➜  ~  npm config get prefix -g
/Users/faner/.nvm/versions/node/v10.13.0
```

```
➜  ~  node -v
v10.13.0
➜  ~  npm -v
6.4.1
```

#### installed & current

```
  nvm ls                                    List installed versions
  nvm ls <version>                          List versions matching a given <version>
  nvm use [--silent] <version>              Modify PATH to use <version>. Uses .nvmrc if available
  nvm current                               Display currently activated version
```

`nvm ls`：列出本地已经安装的 node 版本；  
`nvm use <version>`：激活指定版本的 node；  
`nvm current`：查看当前激活（use）的 node 版本；  

#### cache path

```
  nvm which [current | <version>]           Display path to installed node version. Uses .nvmrc if available
  nvm cache dir                             Display path to the cache directory for nvm
```

#### version resolve

```
  nvm version <version>                     Resolve the given description to a single local version
  nvm version-remote <version>              Resolve the given description to a single remote version
```

#### reinstall packages

```
  nvm install-latest-npm                    Attempt to upgrade to the latest working `npm` on the current node version
  nvm reinstall-packages <version>          Reinstall global `npm` packages contained in <version> to current version
```

#### uninstall

```
  nvm uninstall <version>                   Uninstall a version
```

## brew（macOS）

**macOS 下还是建议通过 brew 安装 nvm，再通过 nvm 来安装切换管理配置 node 版本**。

如果之前使用 brew 安装的 node 10.12.0，执行 `brew update` - `brew upgrade` 后将自动升级到最新的 v11.0.0。

node 11 由于 [clearTimeout blocks the process](https://github.com/nodejs/node/issues/23860) 引起 100% CPU usage 导致 whistle 假死。这时，得考虑暂时恢复使用 node10 旧版本，待完全稳定兼容后再升级回最新版本的 node。

以下提供3种参考方案。

### brew switch + pin

如果之前未执行过 `brew prune`，`/usr/local/Cellar/node/` 目录下可能还残存过往安装的历史版本，此时可通过 `brew switch node <version>` 切换 node 到指定历史版本。

为防止未来的几个不稳定版本在 upgrade 时自动升级，可以执行 `brew pin node` 阻止 node 更新，在短期内将 node 固定在 v10.12.0 版本。等到 node 更新到已解决问题的稳定版本 v11.1.0 或 v.11.2.0 时，再执行 `brew unpin node` 解除禁止更新限制。  

### brew install node@10

执行 `brew search node`，可以看到有 `node@6`、`node@8`、`node@10` 等历史版本可供选择安装。

执行 `brew install node@10` 可安装 node10 的最后一个 LTS 版本 —— node 10.13.0。

从 `brew info node@10` 和 `brew install node@10` 的 Caveats 信息可知，安装的 node@10 是 keg-only，没有自动 symlink 到 `/usr/local` 目录下。

按照 Caveats 说明，需要执行 `echo 'export PATH="/usr/local/opt/node@10/bin:$PATH"' >> ~/.zshrc` 将其写入 `.zshrc`（或 `.bash_profile`），这样每次启动 shell 都会 export PATH，node@10（`/usr/local/opt/node@10/bin`）添加到 PATH 靠前位置，这样 node@10 优先 node@11 被找到，从而实现替换。

### brew install node@9 ?

执行 `brew search node@9`，提示仓库中没有 node9：

```
~ » brew search node@9                                                                                  ~
No formula or cask found for "node@9".
```

那如何安装 node9，或 node10 更老的版本（例如 node 10.12.0）呢？

参考 **Homebrew 安装指定版本的软件**：[thrift](https://www.jianshu.com/p/aadb54eac0a8) / [gradle](http://jefferlau.me/2017/11/30/Homebrew-%E5%AE%89%E8%A3%85%E6%8C%87%E5%AE%9A%E7%89%88%E6%9C%AC%E7%9A%84%E8%BD%AF%E4%BB%B6/) / [ffmpeg](https://segmentfault.com/a/1190000015346120)  

> 从 `brew info` 的 From 中爬出指定版本提交的 commit ID 及其 rb，然后 brew install 从本地指定版本的 rb 安装。

## n

node 有一个模块叫 `n`，是专门用来管理 Node.js 版本的。

使用 (c)npm 安装 n 模块：`(c)npm install-g n`。

执行 `n --version` 查看 n 版本；执行 `n --help` 查看 n 命令帮助。
