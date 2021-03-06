# fis-um

基于fex-team的fis3，一行命令实现传统网站页面的less解析+js压缩合并+静态资源hash等。

Based on fis3 of fex-team, one-line command realizes less parsing + JS compression and merging + static resource hash of traditional website pages.

适用于传统 HTML + CSS + JS 的开发方式。

It is suitable for the development of traditional HTML + CSS + JS.

#### 使用方法 / Usage

##### 安装 / Install

```bash
npm i -g fis-um
```

##### 命令 / Command

执行命令前务必进入path_src目录

Be sure to enter the path_src directory before executing the command

运行编译 / Build

```bash
fis-um release
```

运行前清除缓存 / Clean before build

```bash
fis-um release -c
```

开发(监听文件改变) / Development(watching)

```bash
fis-um release -w
```

##### 配置 / Configure

创建config.js，放入源代码的path_src目录下，前三个参数必须，后面的参数可以按需填写。

To create config.js and put it into the path_src directory of source code, the first three parameters must be filled in, and the latter parameters can be filled in as needed.

```javascript
module.exports = [{
    // 入口文件 *.html 或 /*/**/*.{html,shtml}
    entry_files: '*.html',
    // src文件夹
    path_src: 'rs',
    // dist文件夹
    path_dist: 'rd',
    // 部署文件夹
    path_deploy: '',
    // 是否启用amd
    amd: false,
    // 是否是相对路径
    relative: false,
    // 是否压缩
    minimum: false,
    // 是否加hash
    hash: true,
    // 资源域名
    domain: false,
    // 代码配置，会将该配置直接替换全局
    code_config: {
        //API请求默认服务器，例如//api.umsoft.cn
        host: '//adas.umdev.cn',
    },
    // 不生成mod的文件
    not_mod_files: ['{global,$lib}/**.js'],
    // 在html中附件全局资源
    loader_libs: {
        '*.html': ['/3rd/global/web.js']
    },
    // 自定义打包规则
    package: [{
        files: '/(*)/({_,$,})(*)/**.{js,htm,tpl}',
        to: '/$1/asset/$3.js'
    }, {
        files: '/(*)/({_,$,})(*)/**.{css,less}',
        to: '/$1/asset/$3.css'
    }, {
        files: '/3rd/**',
        to: false
    }],
    // 全局替换
    replace: [{
        files: '*.{html,js}',
        rules: [{search: /time/g, replace: 'time'}]
    }],
    // 发布目录
    release: [{
        files: '/(*)/({_,$})(**)',
        to: "/$1/$3"
    }]
}];
```
