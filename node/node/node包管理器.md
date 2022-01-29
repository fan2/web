## NPM

Node.js 默认内置了模块管理工具 —— **NPM**（Node Package Manager）。  

[An introduction to the npm package manager](https://nodejs.dev/learn/an-introduction-to-the-npm-package-manager)

It started as a way to download and manage dependencies of Node.js packages, but it has since become a tool used also in frontend JavaScript.

> [Yarn](https://yarnpkg.com/en/) and [pnpm](https://pnpm.js.org/) are alternatives to npm cli. You can check them out as well.

`npm` manages downloads of dependencies of your project.  

If a project has a `package.json` file, by running `npm install`.  
it will install everything the project needs, in the `node_modules` folder, creating it if it's not existing already.  

```shell
faner@MBP-FAN:~|⇒  npm -v
6.4.0
```

执行 `npm -h` 可查看命令帮助。  
执行 `npm help install` 可查看子命令 install 的帮助。  
基本使用可参考 [nodejs-npm模块管理器](https://www.cnblogs.com/mtl-key/p/6426197.html)。

[NPM - Node Package Manager](https://www.tutorialsteacher.com/nodejs/what-is-node-package-manager)

Node Package Manager (NPM) is a command line tool that installs, updates or uninstalls Node.js packages in your application. It is also an online repository for open-source Node.js packages. The node community around the world creates useful modules and publishes them as packages in this repository.

- [Using npm Packages](https://guide.meteor.com/using-npm-packages.html)  
- [How to Get npm Packages](https://docs.cocos.com/creator/manual/en/scripting/modules/config.html)  

日常可在 https://www.npmjs.com/ 搜索一些有用的工具包，[40 Useful NPM Packages for Node.js Apps in 2021](https://leanylabs.com/blog/npm-packages-for-nodejs/)。  

- Web Frameworks  
- Utility Functions  
- Working With File System  
- Improving Development Process  
- Better Command Line Interface  
- Other Specialized Packages  
- Conclusion  
