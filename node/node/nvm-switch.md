
## Latest LTS

从 `nvm ls-remote --lts | grep 'Latest'` 结果可知，当前的 Latest LTS 版本为 v10.16.3。

```
╭─faner at FAN-MB1 in ~
╰─○ nvm ls-remote --lts | grep 'Latest'
         v4.9.1   (Latest LTS: Argon)
        v6.17.1   (Latest LTS: Boron)
        v8.16.1   (Latest LTS: Carbon)
       v10.16.3   (Latest LTS: Dubnium)
```

### install

安装最新 lts 版本 10.16.3：

```
╭─faner at FAN-MB1 in ~
╰─○ nvm install 10.16.3
Downloading and installing node v10.16.3...
Downloading https://nodejs.org/dist/v10.16.3/node-v10.16.3-darwin-x64.tar.xz...
######################################################################## 100.0%
Computing checksum with shasum -a 256
Checksums matched!
Now node v10.16.3 (npm v6.9.0)
Creating default alias: default -> 10.16.3 (-> v10.16.3)
```

ubuntu 和 macOS 下，安装完自动use切换到新版本；Windows 下每次安装完新版本的 node，还需要执行 `nvm use <version>` 切换版本。

执行 `nvm current` 或 `nvm version` 查看当前版本：

```
╭─faner at FAN-MB1 in ~
╰─○ nvm current
v10.16.3
╭─faner at FAN-MB1 in ~
╰─○ nvm version
v10.16.3
```

### NVM_BIN

nvm install 安装的 node 实际是按版本存放在 `NVM_DIR/versions/node` 目录下。
可执行 `echo $NVM_BIN` 查看当前 node 版本的 bin 目录。

执行 `nvm which current` 可以查看目录：

```
╭─faner at FAN-MB1 in ~
╰─○ nvm which current
/Users/faner/.nvm/versions/node/v10.16.3/bin/node
╭─faner at FAN-MB1 in ~
╰─○ nvm cache dir
/Users/faner/.nvm/.cache
```

### node/npm

执行 `node -v` 和 `npm -v` 可以查看 node/npm 的版本：

```
╭─faner at FAN-MB1 in ~
╰─○ node -v
v10.16.3
╭─faner at FAN-MB1 in ~
╰─○ npm -v
6.9.0
```

## Latest dev

同时，也可以考虑安装最新的 v11 试验版本：

```
╭─faner at FAN-MB1 in ~
╰─○ nvm ls-remote 11↵
        v11.0.0
        v11.1.0
        v11.2.0
        v11.3.0
        v11.4.0
        v11.5.0
        v11.6.0
        v11.7.0
        v11.8.0
        v11.9.0
       v11.10.0
       v11.10.1
       v11.11.0
       v11.12.0
       v11.13.0
       v11.14.0
       v11.15.0
```

### install

执行 `nvm install v11.15.0` 安装最新的 v11.15.0 版本：

```
╭─faner at FAN-MB1 in ~
╰─○ nvm install v11.15.0
Downloading and installing node v11.15.0...
Downloading https://nodejs.org/dist/v11.15.0/node-v11.15.0-darwin-x64.tar.xz...
######################################################################## 100.0%
Computing checksum with shasum -a 256
Checksums matched!
Now node v11.15.0 (npm v6.7.0)
```

> macOS zsh 中，安装完已自动切换到该版本。

执行 `nvm current` 或 `nvm version` 查看当前版本：

```
╭─faner at FAN-MB1 in ~
╰─○ nvm current↵
v11.15.0
╭─faner at FAN-MB1 in ~
╰─○ nvm version
v11.15.0
```

### NVM_BIN

nvm install 安装的 node 实际是按版本存放在 `NVM_DIR/versions/node` 目录下。
可执行 `echo $NVM_BIN` 查看当前 node 版本的 bin 目录。

执行 `nvm which current` 可以查看目录：

```
╭─faner at FAN-MB1 in ~
╰─○ nvm which current
/Users/faner/.nvm/versions/node/v10.16.3/bin/node
```

### node/npm

执行 `node -v` 和 `npm -v` 可以查看 node/npm 的版本：

```
╭─faner at FAN-MB1 in ~
╰─○ node -v
v11.15.0
╭─faner at FAN-MB1 in ~
╰─○ npm -v
6.7.0
```

#### npm prefix

`npm prefix` 为当前目录，其他三项为 nvm_symlink：

```
╭─faner at FAN-MB1 in ~ using
╰─○ npm prefix
/Users/faner
╭─faner at FAN-MB1 in ~ using
╰─○ npm prefix -g
/Users/faner/.nvm/versions/node/v11.15.0

╭─faner at FAN-MB1 in ~ using
╰─○ npm config get prefix
/Users/faner/.nvm/versions/node/v11.15.0
╭─faner at FAN-MB1 in ~ using
╰─○ npm config get prefix -g
/Users/faner/.nvm/versions/node/v11.15.0
```

#### npm root

`npm root` 为 npm install 安装的 node_modules 目录：

```
╭─faner at FAN-MB1 in ~ using
╰─○ npm root
/Users/faner/node_modules
╭─faner at FAN-MB1 in ~ using
╰─○ npm root -g
/Users/faner/.nvm/versions/node/v11.15.0/lib/node_modules
```

## alias default

执行 `nvm ls` 查看本地已安装的 nodejs 版本列表。

```
╭─faner at FAN-MB1 in ~
╰─○ nvm ls
       v10.16.3
->     v11.15.0
default -> 10.16.3 (-> v10.16.3)
node -> stable (-> v11.15.0) (default)
stable -> 11.15 (-> v11.15.0) (default)
iojs -> N/A (default)
unstable -> N/A (default)
lts/* -> lts/dubnium (-> v10.16.3)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.16.1 (-> N/A)
lts/dubnium -> v10.16.3
```

考虑执行 `nvm alias default node`，后续所有新开的终端zsh中，都将采用最新的 nodejs 作为默认版本。

```
nvm alias default node                Always default to the latest available node version on a shell
```

```
➜  ~ nvm alias default node
default -> node (-> v10.16.3)

➜  ~ nvm ls
       v10.16.3
->     v10.16.3
default -> node (-> v10.16.3)
node -> stable (-> v10.16.3) (default)
stable -> 10.14 (-> v10.16.3) (default)
iojs -> N/A (default)
lts/* -> lts/dubnium (-> v10.16.3)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.15.1 (-> N/A)
lts/carbon -> v8.14.0 (-> N/A)
lts/dubnium -> v10.16.3
```

### pin default

nvm use/switch to old version

如有需要，也可再次执行 `nvm use 10.16.3`，将当前 zsh 中的 node 版本临时切换回旧的 10.16.3 版本。但新开 zsh 窗口，将重新使用 alias default 版本。

由于最新版本可能存在一些兼容性问题，建议执行 `nvm alias default 10.16.3` 固定某个版本为默认版本。

## reinstall-packages

nvm reinstall-packages

执行 `nvm use 10.16.3` 切换 node 版本为 10.16.3 后，Windows 下需要**重新手动**安装之前安装的 npm 包：

Linux/macOS 下的 nvm 支持 `nvm install` 安装新版 node 时，指定 `--reinstall-packages-from=<version>` 选项，顺便安装指定旧版本 node/npm 安装过 的软件包。

```
  nvm install [-s] <version>                Download and install a <version>, [-s] from source. Uses .nvmrc if available
    --reinstall-packages-from=<version>     When installing, reinstall packages installed in <node|iojs|node version number>
```

如果 `nvm install` 安装新版 node 时，未指定 `--reinstall-packages-from=<version>` 选项，也可后期再执行 `nvm reinstall-packages <version>`，重新安装指定旧版本 node/npm 包。

```
nvm reinstall-packages <version>          Reinstall global `npm` packages contained in <version> to current version
```
