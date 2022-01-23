## 关于 Node.js

Node.js 是一个基于 Chrome [V8](https://developers.google.com/v8/) 引擎的 JavaScript 运行环境。

Node.js 将 JavaScript 脚本语言从浏览器的牢笼中解放出来，其提供的 node 运行环境使得我们可以像使用 python 等脚本语言一样基于 JavaScript 编写构建 server-side 应用程序。

## 安装 [Node.js](https://nodejs.org/)

在 macOS 终端中执行 `brew install node` 命令即可安装最新版 node。  

```shell
faner@MBP-FAN:~|⇒  node -v
v10.9.0
```

执行 `node -h` 可查看 Usage 帮助：

```shell
faner@MBP-FAN:~|⇒  node -h
Usage: node [options] [ -e script | script.js | - ] [arguments]
       node inspect script.js [arguments]

Options:
  -                          script read from stdin (default;
                             interactive mode if a tty)
  --                         indicate the end of node options
```

执行 `man node` 可查看 Manual 手册：

```shell
NODE(1)                   BSD General Commands Manual                  NODE(1)

NAME
     node -- server-side JavaScript runtime

SYNOPSIS
     node [options] [v8-options] [-e string | script.js | -] [--] [arguments ...]
     node debug [-e string | script.js | - | <host>:<port>] ...
     node [--v8-options]

DESCRIPTION
     Node.js is a set of libraries for JavaScript which allows it to be used outside
     of the browser.  It is primarily focused on creating simple, easy-to-build net-
     work clients and servers.
```

## node 交互（REPL）

安装 node 后，在终端敲下 `node` 即进入 node 交互控制台 —— REPL（Read-Eval-Print-Loop）。

bash shell 的前导符（primary prompt，PS1）为 <kbd>$</kbd>，python shell 前导符为3个大于号 `>>>`，node shell 的前导符则为一个大于号 <kbd>></kbd>，等待输入命令。  

```shell
faner@MBP-FAN:~|⇒  node
> console.log('hello world from Node.js')
hello world from Node.js
undefined
> exit
ReferenceError: exit is not defined
>
(To exit, press ^C again or type .exit)
> .exit
```

连按两次 `^C` 或输入 `.exit` 即可退出控制台。

### 基本命令

```shell

> .help
.break    Sometimes you get stuck, this gets you out
.clear    Alias for .break
.editor   Enter editor mode
.exit     Exit the repl
.help     Print this help message
.load     Load JS from a file into the REPL session
.save     Save all evaluated commands in this REPL session to a file

> .editor
// Entering editor mode (^D to finish, ^C to cancel)

>
(To exit, press ^C again or type .exit)
> exit
ReferenceError: exit is not defined
> .exit()
Invalid REPL keyword
> .exit
```

`.help`：显示所有基础命令。  
`.break`：多行书写中途放弃，返回到提示符。也可按两次 `^C`。  
`.clear`：清除 REPL 运行环境上下文中保存的所有对象（变量与函数）。  
`.editor`：进入编辑器模式。`^C` 放弃编辑，`^D` 执行编辑内容。  
`.exit`：退出 REPL 运行环境，也可按两次 `^C`。  
`.save`：保存 REPL 表达式到文件中。  
`.load`：加载文件中的表达式到 REPL。  

### 多行输入

Node REPL 会自动检测连续表达式，连续行首会有三个点号（`...`）标识：

```shell
> for (let i=0; i<5; i++) {
... console.log('i =', i)
... }
i = 0
i = 1
i = 2
i = 3
i = 4
```

### 运算结果

在 Node REPL 中，输入运算表达式，则按下回车键在下一命令行返显结果。  
如果输入一条定义或赋值语句，没有返回值，输出 `undefined`。  

```shell
> let x = 2018
undefined
> let y = 8102
undefined
> x+y
10120
```

#### 特殊变量（下划线）

Node REPL 使用下划线（`_`）变量存储上一个表达式的运行结果，类似 bc 中的 `last` 变量。

```shell
> 200+300
500
> _+400
900
```

### 与 python 对比

以下是 node 和 python 导入内置模块，然后获取打印系统相关信息的代码对照：

![node&python-code](./images/node&python-code.png)

1. 脚本首行 [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))

	- python：`#!/usr/bin/env python`  
	- node js：`#! /usr/bin/env node`  

2. 脚本 Usage 帮助

	- python：`python get-pip.py -h`  
	- node：`node whistle.js -h`  

3. 脚本运行：

	- python：`python3 get-pip.py`  
	- node：`node whistle.js`  

> 脚本首行的 shebang 已经指定解释器，当脚本文件具有可执行权限（`x`）时，可省掉前面的解释器命令。

![node&python-usage](./images/node&python-usage.png)

## NPM

Node.js 默认内置了模块管理工具 —— **NPM**（Node Package Manager）。  

```shell
faner@MBP-FAN:~|⇒  npm -v
6.4.0
```

执行 `npm -h` 可查看命令帮助。  
执行 `npm help install` 可查看子命令 install 的帮助。  
