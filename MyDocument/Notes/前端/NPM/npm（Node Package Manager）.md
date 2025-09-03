# 介绍
NPM（Node Package Manager）是一个 JavaScript 包管理工具，也是 Node.js 的默认包管理器。
NPM 允许开发者轻松地下载、安装、共享、管理项目的依赖库和工具。
NPM 是 Node.js 自带的包管理工具，因此，通常你只需安装 Node.js，NPM 就会自动安装在系统中。
# 主要功能：
包管理：NPM 可以帮助你安装并管理项目所需的各种第三方库（包）。例如，可以通过简单的命令来安装、更新、或删除依赖。
版本管理：NPM 支持版本控制，允许你锁定某个特定版本的依赖，或根据需求选择最新的版本。
包发布：NPM 允许开发者将自己的库发布到 NPM 仓库中，其他开发者可以通过 NPM 下载并使用这些库。
命令行工具：NPM 提供了强大的命令行工具，可以用于安装包、运行脚本、初始化项目等多种操作。
由于新版的 Node.js 已经集成了 NPM，所以我们可以直接通过输入 npm -v 来测试是否成功安装，出现版本提示表示安装成功:
`$ npm -v`
`2.3.0`
如果你安装的是旧版本的 npm，可以很容易得通过 npm 命令来升级，命令如下：
`$ sudo npm install npm -g`
`/usr/local/bin/npm -> /usr/local/lib/node_modules/npm/bin/npm-cli.js`
`npm@2.14.2 /usr/local/lib/node_modules/npm`
如果是 Window 系统使用以下命令即可：
`npm install npm -g`
参考文档：[NPM 使用介绍 | 菜鸟教程](https://www.runoob.com/nodejs/nodejs-npm.html#taobaonpm)