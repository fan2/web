
## [steamer](https://github.com/steamerjs/steamerjs)

[steamerjs - npm](https://www.npmjs.com/package/steamerjs)

[steamerjs 前端开发体系](https://steamerjs.github.io/) - gitbook  

---

steamer 命令行及脚手架全面更新了。

后续有新项目的话，亦推荐使用 steamer 系列脚手架，有提供 react, vue 和无框架脚手架，目前已经全面升级支持 webpack 4.0。

omi 跟 vue 主要是针对某一个框架的；**steamer** 主要是围绕团队，打造开发体系的，团队的开发流程和体系都融入在里面了。

代码规范：[AlloyTeam ESLint 规则](https://alloyteam.github.io/eslint-config-alloy/)

## node_modules

目前前端项目主要引入了 browserutils、net 和 webpack-utils 三个 steamer 模块。

```shell
faner@MBP-FAN:~/desktop-m/node_modules|dev-checkpskey⚡
⇒  ls -d1 steam*
steamer-browserutils
steamer-net
steamer-webpack-utils
```

`/desktop-m/config/project.js`：

```json
        // webpack resolve.alias 包别名
        alias: {
            'utils': path.join(srcPath, '/js/common/utils'),
            'sutils': 'steamer-browserutils/index',
            'net': 'steamer-net',

        },
```

> 1. **utils** 简写替换 `/js/common/utils`，不必逐级索引相对目录。  
> 2. **sutils** 映射为 `steamer-browserutils/index`；  
> 3. **net** 映射为 `steamer-net`；  
