## NVM

[NVM](https://github.com/creationix/nvm): Node Version Manager

Manage multiple Node.js versions

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

`nvm ls-remote v10`：列举 node 10 的所有版本；  
`nvm ls-remote 11`：列举 node 11 的所有版本。  

#### install

```
  nvm install [-s] <version>                Download and install a <version>, [-s] from source. Uses .nvmrc if available
    --reinstall-packages-from=<version>     When installing, reinstall packages installed in <node|iojs|node version number>
    --lts                                   When installing, only select from LTS (long-term support) versions
    --lts=<LTS name>                        When installing, only select from versions for a specific LTS line
    --skip-default-packages                 When installing, skip the default-packages file if it exists
    --latest-npm                            After installing, attempt to upgrade to the latest working npm on the given node version
```

`nvm install <version>`： 安装指定版本的 node。

#### installed & current

```
  nvm ls                                    List installed versions
  nvm ls <version>                          List versions matching a given <version>
  nvm use [--silent] <version>              Modify PATH to use <version>. Uses .nvmrc if available
  nvm current                               Display currently activated version
```

`nvm ls`：列出本地已经安装的 node 版本；  
`nvm use <version>`：激活指定版本的 node；  
`nvm current`：查看当前激活（正在使用）的 node 版本；  

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

## brew(macOS)

**macOS 下建议通过 brew 安装 nvm，再通过 nvm 来安装切换管理配置 node 版本**。

如果之前直接使用 brew 安装的 node，当前 node 版本为 v10.12.0，执行 `brew update` - `brew upgrade` 后将升级到 v11.0.0。

node 11 由于 [clearTimeout blocks the process](https://github.com/nodejs/node/issues/23860) 引起 100% CPU usage 导致 whistle 假死。

此时，可考虑使用 brew 的 switch 命令来切换到残存的历史版本。

### brew switch

macOS 下可调用 `brew switch` 命令切换已安装的 node 版本。

执行 `brew switch -h` 查看 switch 命令简介：

```
➜  ~  brew switch -h
brew switch formula version:
    Symlink all of the specific version of formula's install to Homebrew prefix.
```

执行 `tree -L 1 /usr/local/Cellar/node` 可查看 `/usr/local/Cellar/node` 下尚未删除的 node 缓存历史版本。

```
~ tree -L 1 /usr/local/Cellar/node
/usr/local/Cellar/node
├── 10.10.0
├── 10.11.0
├── 10.12.0
└── 11.0.0

4 directories, 0 files
```

执行 `brew switch node 10.12.0` 切换到 node 10 最后一个版本。

```
~ brew switch node 10.12.0
Cleaning /usr/local/Cellar/node/10.11.0
Cleaning /usr/local/Cellar/node/10.12.0
Cleaning /usr/local/Cellar/node/11.0.0
Cleaning /usr/local/Cellar/node/10.10.0
7 links created for /usr/local/Cellar/node/10.12.0
```

重新执行 `node -v`，可以看到 node 已切回 v10.12.0 版本：

```
~ node -v
v10.12.0
```

### brew pin/unpin

为防止未来的几个不稳定版本在 upgrade 时自动升级，可以执行 `brew pin node` 阻止 node 更新，在短期内将 node 固定在 v10.12.0 版本。  
等到 node 更新到已解决问题的稳定版本 v11.1.0 或 v.11.2.0 时，可再执行 `brew unpin node` 解除禁止更新限制。  

## [nvm-windows](https://github.com/coreybutler/nvm-windows)

[Windows上安装nodejs版本管理器nvm](https://www.jianshu.com/p/324044f2f542)  

[Windows 下安装 nvm 管理 nodejs 版本](https://segmentfault.com/a/1190000007612011)  

**`nvm node_mirror [url]`**：设置node镜像，默认为 `https://nodejs.org/dist/`

> 建议设置为淘宝的镜像 `https://npm.taobao.org/mirrors/node/`

**`nvm npm_mirror [url]`**：设置npm镜像，默认为 `https://github.com/npm/npm/archive/`

> 建议设置为淘宝的镜像 `https://npm.taobao.org/mirrors/npm/`

## n

node 有一个模块叫 `n`，是专门用来管理 Node.js 版本的。

使用 (c)npm 安装 n 模块：`(c)npm install-g n`。

执行 `n --version` 查看 n 版本；执行 `n --help` 查看 n 命令帮助。
