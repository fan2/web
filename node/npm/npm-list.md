
[npm-ls](https://docs.npmjs.com/cli/ls) - List installed packages

```javascript
npm ls [[<@scope>/]<pkg> ...]

aliases: list, la, ll
```

This command will print to stdout all the versions of packages that are installed, as well as their dependencies, in a tree-structure.

Positional arguments are **`name@version-range`** identifiers, which will limit the results to only the paths to the packages named. Note that nested packages will *also* show the paths to the specified packages.

It will print out `extraneous`, `missing`, and `invalid` packages.

When run as **`ll`** or **`la`**, it shows extended information by default.

## npm ls -g

npm ls 等效于 npm list。

```shell
# npm list -g --depth=0
faner@MBP-FAN:~|⇒  npm ls -g --depth=0
/usr/local/lib
├── cnpm@5.3.0
├── eslint@4.19.1
├── htmlhint@0.9.13
├── less@3.0.4
├── less-plugin-clean-css@1.5.1
├── npm@6.1.0
├── puppeteer@1.4.0
├── typed-we-app@1.7.0-update.2
├── typescript@2.8.3
└── whistle@1.10.2
```

## npm ll -g

npm ll 等效于 npm la，相比 npm ls 显示更具体的描述、git仓库地址 以及 主页信息。

```shell
# npm la -g --depth=0
faner@MBP-FAN:~|⇒  npm ll -g --depth=0

│ /usr/local/lib
│
├── cnpm@5.3.0
│   cnpm: npm client for cnpmjs.org
│   git://github.com/cnpm/cnpm.git
│   https://github.com/cnpm/cnpm
├── eslint@4.19.1
│   An AST-based pattern checker for JavaScript.
│   git+https://github.com/eslint/eslint.git
│   https://eslint.org
├── htmlhint@0.9.13
│   A Static Code Analysis Tool for HTML
│   git://github.com/yaniswang/HTMLHint.git
│   https://github.com/yaniswang/HTMLHint#readme
├── less@3.0.4
│   Leaner CSS
│   git+https://github.com/less/less.js.git
│   http://lesscss.org
├── less-plugin-clean-css@1.5.1
│   clean-css plugin for less.js
│   git+https://github.com/less/less-plugin-clean-css.git
│   http://lesscss.org
├── npm@6.1.0
│   a package manager for JavaScript
│   git+https://github.com/npm/npm.git
│   https://docs.npmjs.com/
├── puppeteer@1.4.0
│   A high-level API to control headless Chrome over the DevTools Protocol
│   git+https://github.com/GoogleChrome/puppeteer.git
│   https://github.com/GoogleChrome/puppeteer#readme
├── typed-we-app@1.7.0-update.2
│   typescript declaration for WeApp
│   git+https://github.com/Emeryao/typed-we-app.git
│   https://github.com/Emeryao/typed-we-app#readme
├── typescript@2.8.3
│   TypeScript is a language for application scale JavaScript development
│   git+https://github.com/Microsoft/TypeScript.git
│   http://typescriptlang.org/
└── whistle@1.10.2
    HTTP, HTTPS, Websocket debugging proxy
    git+https://github.com/avwo/whistle.git
    https://github.com/avwo/whistle
```

## specified package

```shell
faner@MBP-FAN:~|⇒  npm ls -g whistle
/usr/local/lib
└── whistle@1.10.2

faner@MBP-FAN:~|⇒  npm ll -g whistle

│ /usr/local/lib
│
└── whistle@1.10.2
    HTTP, HTTPS, Websocket debugging proxy
    git+https://github.com/avwo/whistle.git
    https://github.com/avwo/whistle
```

## UNMET DEPENDENCY npm 解决

执行 `npm list` 提示 `UNMET DEPENDENCY npm`：

```
faner@MBP-FAN:~|⇒  npm list
/Users/faner
├─┬ UNMET DEPENDENCY npm@6.1.0
│ ├── UNMET DEPENDENCY abbrev@1.1.1
│ ├── UNMET DEPENDENCY ansi-regex@3.0.0

│ └── UNMET DEPENDENCY write-file-atomic@2.3.0
└── typed-we-app@1.7.0-update.2

npm ERR! missing: npm@6.1.0, required by faner
npm ERR! missing: JSONStream@1.3.2, required by npm@6.1.0

npm ERR! extraneous: JSONStream@1.3.2 /Users/faner/node_modules/npm/node_modules/JSONStream
npm ERR! extraneous: abbrev@1.1.1 /Users/faner/node_modules/npm/node_modules/abbrev
```

执行 `npm uninstall npm` 卸载 npm：

```
faner@MBP-FAN:~|⇒  npm uninstall npm
npm WARN deprecated undefined@0.1.0: this package has been deprecated
npm WARN saveError ENOENT: no such file or directory, open '/Users/faner/package.json'
npm WARN enoent ENOENT: no such file or directory, open '/Users/faner/package.json'
npm WARN faner No description
npm WARN faner No repository field.
npm WARN faner No README data
npm WARN faner No license field.

added 1 package from 1 contributor and audited 2 packages in 16.362s
found 0 vulnerabilities
```

执行 `npm list`，有一项 undefined:？

```shell
faner@MBP-FAN:~|⇒  npm list
/Users/faner
├── typed-we-app@1.7.0-update.2
└── undefined@0.1.0
```

执行 `npm uninstall undefined` 卸载 undefined：

```shell
faner@MBP-FAN:~|⇒  npm uninstall undefined
npm WARN saveError ENOENT: no such file or directory, open '/Users/faner/package.json'
npm WARN enoent ENOENT: no such file or directory, open '/Users/faner/package.json'
npm WARN faner No description
npm WARN faner No repository field.
npm WARN faner No README data
npm WARN faner No license field.

removed 1 package and audited 1 package in 0.997s
found 0 vulnerabilities
```

重新执行 `npm list`：

```shell
# npm list --depth=0
faner@MBP-FAN:~|⇒  npm list
/Users/faner
└── typed-we-app@1.7.0-update.2
```
