
## cnpm prefix

```shell
faner@MBP-FAN:~|⇒  cnpm prefix
/Users/faner

faner@MBP-FAN:~|⇒  cnpm prefix -g
/usr/local

faner@MBP-FAN:~|⇒  cnpm config get prefix
/usr/local

faner@MBP-FAN:~|⇒  cnpm config get prefix -g
/usr/local
```

## npm prefix

```shell
faner@MBP-FAN:~|⇒  npm prefix
/Users/faner

faner@MBP-FAN:~|⇒  npm prefix -g
/usr/local/Cellar/node/10.8.0

faner@MBP-FAN:~|⇒  npm config get prefix
/usr/local/Cellar/node/10.8.0

faner@MBP-FAN:~|⇒  npm config get prefix -g
/usr/local/Cellar/node/10.8.0
```

### problem

下载 whistle_tmp 拷贝到了 `npm prefix -g`（`/usr/local/Cellar/node/10.8.0/`）下的 `lib/node_modules/whistle` 中。

```shell
faner@MBP-FAN:⇒  cnpm outdated -g
Package  Current  Wanted  Latest  Location
whistle   1.11.3  1.12.0  1.12.0

faner@MBP-FAN:⇒  cnpm i -g whistle
Downloading whistle to /usr/local/Cellar/node/10.8.0/lib/node_modules/whistle_tmp
Copying /usr/local/Cellar/node/10.8.0/lib/node_modules/whistle_tmp/_whistle@1.12.0@whistle to /usr/local/Cellar/node/10.8.0/lib/node_modules/whistle
Installing whistle's dependencies to /usr/local/Cellar/node/10.8.0/lib/node_modules/whistle/node_modules
[1/28] adm-zip@0.4.11 installed at node_modules/_adm-zip@0.4.11@adm-zip
[2/28] cookie@^0.3.1 installed at node_modules/_cookie@0.3.1@cookie
[3/28] extend@^3.0.1 installed at node_modules/_extend@3.0.2@extend
[4/28] colors@1.1.2 installed at node_modules/_colors@1.1.2@colors
[5/28] basic-auth@1.0.0 installed at node_modules/_basic-auth@1.0.0@basic-auth
[6/28] hparser@^0.1.2 installed at node_modules/_hparser@0.1.2@hparser
[7/28] mime@^1.4.1 installed at node_modules/_mime@1.6.0@mime
[8/28] hagent@^0.3.0 installed at node_modules/_hagent@0.3.0@hagent
[9/28] lru-cache@^4.1.1 installed at node_modules/_lru-cache@4.1.3@lru-cache
[10/28] iconv-lite@0.4.7 installed at node_modules/_iconv-lite@0.4.7@iconv-lite
[11/28] node-native-zip2@^1.0.0 installed at node_modules/_node-native-zip2@1.0.0@node-native-zip2
[12/28] q@1.4.1 existed at node_modules/_q@1.4.1@q
[13/28] safe-buffer@^5.1.2 existed at node_modules/_safe-buffer@5.1.2@safe-buffer
[14/28] parseurl@^1.3.1 installed at node_modules/_parseurl@1.3.2@parseurl
[15/28] node-pac@^0.4.0 installed at node_modules/_node-pac@0.4.0@node-pac
[16/28] pipestream@^0.1.0 installed at node_modules/_pipestream@0.1.0@pipestream
[17/28] sni@1.0.0 installed at node_modules/_sni@1.0.0@sni
[18/28] body-parser@1.12.0 installed at node_modules/_body-parser@1.12.0@body-parser
[19/28] pfork@^0.1.6 installed at node_modules/_pfork@0.1.8@pfork
[20/28] ws-parser@^0.2.0 installed at node_modules/_ws-parser@0.2.0@ws-parser
[21/28] socksv5@0.0.6 installed at node_modules/_socksv5@0.0.6@socksv5
[22/28] node-forge@0.7.5 installed at node_modules/_node-forge@0.7.5@node-forge
[23/28] fs-extra2@^1.0.0 installed at node_modules/_fs-extra2@1.0.0@fs-extra2
[24/28] starting@^4.0.1 installed at node_modules/_starting@4.0.3@starting
[25/28] multer@1.2.1 installed at node_modules/_multer@1.2.1@multer
[26/28] express@4.12.3 installed at node_modules/_express@4.12.3@express
[27/28] xml2js@0.4.17 installed at node_modules/_xml2js@0.4.17@xml2js
[28/28] weinre2@^1.1.0 installed at node_modules/_weinre2@1.1.0@weinre2
All packages installed (124 packages installed from npm registry, used 2s(network 2s), speed 2.65MB/s, json 104(896.32kB), tarball 4.1MB)
[whistle@1.12.0] link /usr/local/Cellar/node/10.8.0/bin/whistle@ -> /usr/local/Cellar/node/10.8.0/lib/node_modules/whistle/bin/whistle.js
[whistle@1.12.0] link /usr/local/Cellar/node/10.8.0/bin/w2@ -> /usr/local/Cellar/node/10.8.0/lib/node_modules/whistle/bin/whistle.js
[whistle@1.12.0] link /usr/local/Cellar/node/10.8.0/bin/wproxy@ -> /usr/local/Cellar/node/10.8.0/lib/node_modules/whistle/bin/whistle.js

# 还是旧版本！
faner@MBP-FAN:⇒  w2 -V
1.11.3

```

### npm set prefix

```shell
faner@MBP-FAN:~|⇒  npm config set prefix "/usr/local"
```

### npm prefix

设置修复后，`npm prefix -g` 的值同 `cnpm prefix -g`：

```shell
faner@MBP-FAN:~|⇒  npm prefix
/Users/faner

faner@MBP-FAN:~|⇒  npm prefix -g
/usr/local

faner@MBP-FAN:~|⇒  npm config get prefix
/usr/local

faner@MBP-FAN:~|⇒  npm config get prefix -g
/usr/local
```

### npm root

```shell
faner@MBP-FAN:~|⇒  npm root
/Users/faner/node_modules

faner@MBP-FAN:~|⇒  npm root -g
/usr/local/lib/node_modules

# 同 npm root
faner@MBP-FAN:~|⇒  cnpm root
/Users/faner/node_modules

# 同 npm root -g
faner@MBP-FAN:~|⇒  cnpm root -g
/usr/local/lib/node_modules
```

### resolved

下载 whistle_tmp 拷贝到了 `cnpm root -g`（`/usr/local/lib/node_modules/`） 中：

```javascript
faner@MBP-FAN:~|⇒  cnpm outdated -g
Package  Current  Wanted  Latest  Location
whistle   1.11.3  1.12.0  1.12.0
faner@MBP-FAN:~|⇒  cnpm i whistle -g
Downloading whistle to /usr/local/lib/node_modules/whistle_tmp
Copying /usr/local/lib/node_modules/whistle_tmp/_whistle@1.12.0@whistle to /usr/local/lib/node_modules/whistle
Installing whistle's dependencies to /usr/local/lib/node_modules/whistle/node_modules
[1/28] adm-zip@0.4.11 installed at node_modules/_adm-zip@0.4.11@adm-zip
[2/28] basic-auth@1.0.0 installed at node_modules/_basic-auth@1.0.0@basic-auth
[3/28] cookie@^0.3.1 installed at node_modules/_cookie@0.3.1@cookie
[4/28] extend@^3.0.1 installed at node_modules/_extend@3.0.2@extend
[5/28] colors@1.1.2 installed at node_modules/_colors@1.1.2@colors
[6/28] hparser@^0.1.2 installed at node_modules/_hparser@0.1.2@hparser
[7/28] mime@^1.4.1 installed at node_modules/_mime@1.6.0@mime
[8/28] hagent@^0.3.0 installed at node_modules/_hagent@0.3.0@hagent
[9/28] lru-cache@^4.1.1 installed at node_modules/_lru-cache@4.1.3@lru-cache
[10/28] iconv-lite@0.4.7 installed at node_modules/_iconv-lite@0.4.7@iconv-lite
[11/28] node-native-zip2@^1.0.0 installed at node_modules/_node-native-zip2@1.0.0@node-native-zip2
[12/28] q@1.4.1 existed at node_modules/_q@1.4.1@q
[13/28] safe-buffer@^5.1.2 existed at node_modules/_safe-buffer@5.1.2@safe-buffer
[14/28] parseurl@^1.3.1 existed at node_modules/_parseurl@1.3.2@parseurl
[15/28] sni@1.0.0 installed at node_modules/_sni@1.0.0@sni
[16/28] pipestream@^0.1.0 installed at node_modules/_pipestream@0.1.0@pipestream
[17/28] node-pac@^0.4.0 installed at node_modules/_node-pac@0.4.0@node-pac
[18/28] body-parser@1.12.0 installed at node_modules/_body-parser@1.12.0@body-parser
[19/28] pfork@^0.1.6 installed at node_modules/_pfork@0.1.8@pfork
[20/28] node-forge@0.7.5 installed at node_modules/_node-forge@0.7.5@node-forge
[21/28] ws-parser@^0.2.0 installed at node_modules/_ws-parser@0.2.0@ws-parser
[22/28] express@4.12.3 installed at node_modules/_express@4.12.3@express
[23/28] socksv5@0.0.6 installed at node_modules/_socksv5@0.0.6@socksv5
[24/28] fs-extra2@^1.0.0 installed at node_modules/_fs-extra2@1.0.0@fs-extra2
[25/28] starting@^4.0.1 installed at node_modules/_starting@4.0.3@starting
[26/28] multer@1.2.1 installed at node_modules/_multer@1.2.1@multer
[27/28] xml2js@0.4.17 installed at node_modules/_xml2js@0.4.17@xml2js
[28/28] weinre2@^1.1.0 installed at node_modules/_weinre2@1.1.0@weinre2
All packages installed (124 packages installed from npm registry, used 2s(network 2s), speed 2.49MB/s, json 104(697.09kB), tarball 4.1MB)
[whistle@1.12.0] link /usr/local/bin/whistle@ -> /usr/local/lib/node_modules/whistle/bin/whistle.js
[whistle@1.12.0] link /usr/local/bin/w2@ -> /usr/local/lib/node_modules/whistle/bin/whistle.js
[whistle@1.12.0] link /usr/local/bin/wproxy@ -> /usr/local/lib/node_modules/whistle/bin/whistle.js

# 已是最新版本
faner@MBP-FAN:~|⇒  w2 -V
1.12.0
```