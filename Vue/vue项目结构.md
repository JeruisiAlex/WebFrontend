# Vue 项目结构

本篇讨论的 Vue 项目结构均是基于 vue cli 构建的项目结构。

## vue cli

在开始讨论项目结构之前，首先来了解 vue cli 的工作原理。

vue cli 的工作运行中包含了四个主要的部分 vue cli, Babel, Webpack, Node.js，先对这四项进行简单介绍。
- vue cli：主要起两方面作用，一个是提供 vue 语法模版的支持，另一个是将 vue 模版编译为常规的 javascript 代码。
- Babel：将现代的 javascript 进行转化为向后兼容的版本，使一些旧版本的浏览器也可以兼容运行。
- Webpack：将 html, css, javascript 文件进行打包，生成一个或多个 bundle 文件，这样可以减少 http 请求的数量，提高运行效率。(bundle并不一种文件类型，而是对形如这类文件的统称：app.bundle.js)
- Node.js：提供运行环境的支持，在开发环境下将打包好的文件运行起来生成一个本地运行的服务，这样就可以通过浏览器访问本地运行的服务来进行测试。

通过 vue cli 构建的项目的一般结构如下：
```
项目文件夹
├── babel.config.js
├── vue.config.js
├── jsconfig.json
├── package.json
├── package-lock.json
├── node_modules
├── public
├   ├── index.html
├   └── favicon.ico
└── src
    ├── assets
    ├── components
    ├── router
    ├── store
    ├── views
    └── App.vue
```

首先介绍日常开发中开发中最常用的 src 文件夹，这个文件夹里面的内容就是我们的代码文件。
- assets 文件夹中存放图片等静态资源。
- components 文件夹中存放不是单独占据路由的组件。
- router 路由管理文件夹，如果安装了官方 router 插件就会有。
- store 全局状态管理文件夹，如果安装了官方 vuex 插件就会有。
- views 文件夹中存放会单独占据路由的组件。
- 当然这是官方默认的文件结构，也可以自行安排，这一点比较随意，但一定要符合软件工程的基本原则。

然后是 public 文件夹，你会注意到这个文件夹下有整个项目中唯一一个 html 文件，没错 vue 作为一个单页面框架，这个 html 文件就是那个唯一的页面，虽然一般不需要修改因此非常重要。一般来说默认的 index.html 文件内容大致如下：
``` html
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <!-- 网站的图标，这里指向了同目录下的 favicon.ico 文件 -->
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
    <!-- 这里有一个雷点，body标签自带了 8px 的 margin 属性，不需要的话需要设置为 0 -->
  <body> 
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <!-- App.vue 以及所有的组件都会被挂载到这个标签下 -->
    <div id="app"></div> 
    <!-- built files will be auto injected -->
  </body>
</html>
```

## babel.config.js
与 Babel 相关的就是 babel.config.js文件，这是 Babel 的配置文件，告诉 Babel 应该如何去工作。Babel 在工作的时候会读取这个文件。也可以在这里为 Babel 去添加一些配置满足个性化需求。

以下是默认内容：
``` js
// 导出一个对象
module.exports = {
  presets: [ // 预定义设置，这里添加了 vue cli 作为预定义配置
    '@vue/cli-plugin-babel/preset'
  ]
}
```

## vue.config.js
与 vue cli 和 Webpack 相关的配置文件。

以下是默认内容：
``` js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({ // 定义一个外部导出的配置
  transpileDependencies: true // 这一行是用来让 vue cli 告诉 Babel 需要把 node_modules 里面的依赖也进行转化，虽然会增加编译时间但是可以增强兼容性
})

```
以下是可以手动添加的配置选项
``` js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({ // 定义一个外部导出的配置
  transpileDependencies: true, // 这一行是用来让 vue cli 告诉 Babel 需要把 node_modules 里面的依赖也进行转化，虽然会增加编译时间但是可以增强兼容性
    outputDir: 'dist', // 生产环境打包目录
    assetsDir: 'static', // 静态资源存放路径，相对于 outputDir
    indexPath: 'index.html', // index.html 存放路径，相对于 outputDir
    configureWebpack: { // 给 Webpack 添加配置
        plugins: [ // 给 Webpack 添加插件

        ], 
    }
})

```

## package
与依赖包相关的一共有两个文件和一个文件夹，package.json, package-lock.json, node_modules。其中 pack-lock.json 是通过 package.json 和 node_modules 自动生成，不需要手动修改，node_modules 则是根据 package.json 中指定的依赖项安装的依赖包。每次通过 npm install 的时候都会自动向 package.json 和 package-lock.json 中写入依赖项。

下面将会详细介绍 package.json 中的结构。
``` json
{
  "name": "pkh", // 项目的名称，可以手动设置
  "version": "0.1.0", // 项目的版本
  "private": true, // 是否是私有
  "scripts": { 
    // npm run 执行的脚本，比如 serve 就是 npm run serve
    // 可以通过这里添加自定义的脚本
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build"
  },
  "dependencies": { // 项目运行时的依赖包
    "axios": "^1.7.7",
    "core-js": "^3.8.3",
    "element-plus": "^2.8.6",
    "vue": "^3.2.13",
    "vue-router": "^4.0.3",
    "vuex": "^4.0.0"
  },
  "devDependencies": { // 项目开发中的依赖包
    "@vue/cli-plugin-babel": "~5.0.0",
    "@vue/cli-plugin-router": "~5.0.0",
    "@vue/cli-plugin-vuex": "~5.0.0",
    "@vue/cli-service": "~5.0.0"
  }
}
```

## jsconfig.json
这个文件的作用是配置 vscode 编译器行为，以下是默认配置
``` json
{
  "compilerOptions": {
    "target": "es5", // 设定 ECMAScript 的目标版本为 es5
    "module": "esnext", // 这一条允许使用最新的 ECMAScript 模块标准
    "baseUrl": "./", // 设定根目录
    "moduleResolution": "node", // 指定模块解析策略为 node 风格
    "paths": { // 配置路径的别名
      "@/*": [
        "src/*"
      ]
    },
    "lib": [ // 指定需要包含的库
      "esnext",
      "dom",
      "dom.iterable",
      "scripthost"
    ]
  }
}
```
