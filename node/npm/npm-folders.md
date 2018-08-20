# [npm-folders](https://docs.npmjs.com/files/folders)

npm-folders : Folder Structures Used by npm

- Local install (default): puts stuff in `./node_modules` of the current package root.  
- Global install (with **-g**): puts stuff in `/usr/local` or wherever node is installed.  
- Install it **locally** if you're going to `require()` it.  
- Install it **globally** if you're going to run it on the command line.  
- If you need both, then install it in both places, or use **npm link**.  

`npm help 5 folders`

## [prefix Configuration](https://docs.npmjs.com/files/folders#prefix-configuration)

The **prefix** config defaults to the location where node is installed.  

- On most systems, this is **`/usr/local`**. On Windows, it's **`%AppData%\npm`**.  
- On Unix systems, it's one level up, since node is typically installed at **`{prefix}/bin/node`** rather than **`{prefix}/node.exe`**.

When the **global** flag is set, npm installs things into this <u>prefix</u>. When it is not set, it uses the root of the ***current*** package, or the ***current*** working directory if not in a package already.

## [Node Modules](https://docs.npmjs.com/files/folders#node-modules)

Packages are dropped into the **`node_modules`** folder under the <u>prefix</u>. When installing locally, this means that you can `require("packagename")` to load its main module, or `require("packagename/lib/path/to/sub/module")` to load other modules.

Global installs on Unix systems go to **`{prefix}/lib/node_modules`**. Global installs on Windows go to **`{prefix}/node_modules`** (that is, no **lib** folder.)

Scoped packages are installed the same way, except they are grouped together in a sub-folder of the relevant **node_modules** folder with the name of that scope prefix by the @ symbol, e.g. **`npm install @myorg/package`** would place the package in `{prefix}/node_modules/@myorg/package`. See [scope](https://docs.npmjs.com/misc/scope) for more details.

If you wish to `require()` a package, then install it locally.

## Executables

When in global mode, executables are linked into **`{prefix}/bin`** on Unix, or directly into **`{prefix}`** on Windows.

When in local mode, executables are linked into `./node_modules/.bin` so that they can be made available to scripts run through npm. (For example, so that a test runner will be in the path when you run **`npm test`**.)
