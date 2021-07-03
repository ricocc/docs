### 简介

**Vue** (读音 /vjuː/，类似于 view) 

　　中文文档：https://cn.vuejs.org/v2/guide/ 
　　官方网站：[https://cn.vuejs.org](https://cn.vuejs.org/)

**Node.js**

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。 

Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。 

Node.js 的包管理器 npm，是全球最大的开源库生态系统。
中文文档：http://nodejs.cn/api/
官方网站：http://nodejs.cn/



#### 1. 起步

```html
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

或者：

```html
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js">可以手动指定版本号</script>
```



#### 2. 安装和运行（2.x版本）

```bash
//安装 2.x 
npm install vue
//全局安装 vue-cli, 速度慢就换成cnpm
 npm install -g vue-cli

//创建一个基于 webpack 模板的新项目
 vue init webpack 项目名称


//安装依赖
cd /project
npm run dev 
```

辅助操作

```bash
//查看Vue 版本
vue -V
//模板列表
vue list
//查看版本
npm list vue
//查看具体操作
vue --help
```

npm速度慢就换cnpm 

```bash
//npm 速度慢的话就安装淘宝镜像 cnpm来替代npm
npm install -g cnpm –registry=http://registry.npm.taobao.org
```

初始化项目，想要一个一个选就去掉 ' **--yes** '

```bash
npm init --yes
```

**package.json** 文件

```json
{
  // 项目/模块名称，长度必须小于等于 214 个字符，不能以"."(点)或者"_"(下划线)开头，不能包含大写字母
  "name": "myvue",
  // 项目版本
  "version": "1.0.0",
  // 项目描述
  "description": "project",
  // 作者
  "author": "Demo_Null",
  // 是否私有，设置为 true 时，npm 拒绝发布
  "private": true,
  // 执行 npm 脚本命令简写，执行前面的简写就代表执行后面的命令
  "scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "e2e": "node test/e2e/runner.js",
    "test": "npm run unit && npm run e2e",
    "lint": "eslint --ext .js,.vue src test/unit test/e2e/specs",
    "build": "node build/build.js"
  },
  // 生产环境下，项目运行所需依赖
  "dependencies": {
    "vue": "^2.5.2",
    "vue-router": "^3.0.1"
  },
  // 开发环境下，项目所需依赖
  "devDependencies": {
    "autoprefixer": "^7.1.2",
    "babel-core": "^6.22.1",
    "babel-eslint": "^8.2.1",
    "babel-helper-vue-jsx-merge-props": "^2.0.3",
    "babel-jest": "^21.0.2",
    "babel-loader": "^7.1.1",
    "vue-style-loader": "^3.0.1",
    "vue-template-compiler": "^2.5.2",
    "webpack": "^3.6.0",
    "webpack-bundle-analyzer": "^2.9.0",
    "webpack-dev-server": "^2.9.1",
    "webpack-merge": "^4.1.0"
  },
  // 项目运行的平台
  "engines": {
    "node": ">= 6.0.0",
    "npm": ">= 3.0.0"
  },
  // 供浏览器使用的版本列表
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "not ie <= 8"
  ]
}
#参考 https://cloud.tencent.com/developer/article/1707926
```

**卸载框架或插件**：

```bash
//安装bootstrap框架 （node.js 8版本以后不需要再写 '--save'）
npm install bootstrap --save
//卸载jQuery框架 （'--save'与'--save-Dev'的区别）
npm uninstall jQuery
//指定版本号
npm install bootstrap@3 --save
```

#### 3. 2.x和3.x版本

##### **1）安装node & vue**

```bash
查看版本：     npm -v
升级版本：     cnpm install npm -g
安装vue：     npm install vue
查看版本：     npm list vue
```

##### **2）安装vue-cli**

```bash
安装2.x【vue-cli版本】： npm install -g vue-cli
安装3.x【vue-cli版本】： npm install -g @vue/cli

查看版本：     vue -V
卸载旧版本： npm uninstall vue-cli -g
```

##### 3）初始化项目-新建项目

```bash
2.x版本： vue init webpack 项目名称
3.x版本： vue create 项目名称
图形化安装： vue ui
    
3.x版本可以通过以下使用2.x版本安装方式新建项目
	首先：  npm install -g @vue/cli-init
	就可以： vue init webpack 项目名称
```

##### 4）项目中基本命令-切到项目目录

```bash
可视化管理： vue ui
编译运行：
    2.x方式运行： npm run dev
    3.x方式运行： npm run serve
    打包： npm run build

【选填】在项目中添加插件： vue add 插件名
```

##### 5）配置文件

```html
2.x方式： config/index.js
3.x方式： 详见-https://cli.vuejs.org/zh/config/#publicpath
```

##### 6）模块的安装和卸载

```bash
npm install juqery --save
//删除下载的模块
npm uninstall jquery --save
//指明下载版本
npm install jquery@3 --save
```



