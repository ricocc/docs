# Vue 项目学习记录

学习项目地址：

[Vue2.5-2.6-3.0]: https://coding.imooc.com/class/203.html

**环境参数：**

- nodejs >=6.2.2
- npm >=3.9
- vue >=2.5.2
- 路由 vue-router 3.0.1
- babel 6.22.1
- stylus 0.54.5
- webpack 3.6.0
- IDE Sublime text / vscode

####  1. 什么是路由?

路由就是根据网址的不同, 返回不同的内容给用户

#### 2. 什么是`<router-view/>`

显示的是当前路由地址所对应的内容

#### 3. `@` 指的是src目录,css文件中引入加`~`

````
import HelloWorld from '@/components/HelloWorld'
````

在css中引入其他的css文件,前面需要加`~`, 完整的就是`~@/路径`

**style标签添加 scoped**

只对当前组件生效

```stylus
.wrapper >>>.swiper-pagination-bullet-active
		background #fff
```

`>>>` 样式穿透 



引入文件, 设置变量

```
@import '~styles/varibles.styl'
$TextColor = #333;
color:$TextColor;
```



#### 4. alias定义路径变量

文件位置: `build/wbebpack.base.conf.js`

代码位置: line 34

```
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      '@': resolve('src'),
      //示例
      'styles': resolve('src/assets/styles'),
    }
  },
```

当修改webpack配置项时,需要重启服务,不然会报错.

```
npm run start
```

#### 5. Ajax 使用 axios 实现传值 

实现跨平台的数据请求

安装

```
npm install axios --save
```

借助生命周期函数`mounted`来进行数据的获取

```js
import axios from 'axios'
export default {
  name: 'Home',
  components: {
     HomeHeader,
     HomeSwiper,
     HomeIcons,
     HomeRecommend,
     HomeWeekend
  },
  methods: {
    getHomeInfo () {
      axios.get('/api/index.json')
        .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc (res) {
      console.log(res)
    }
  },
  mounted () {
    this.getHomeInfo()
  }
}
```

或者是 获取动态路由参数

```js
methods: {
  getDetailInfo () {
    axios.get('/api/detail.json?id=' + this.$route.params.id)
  }
},
mounted () {
  this.getDetailInfo()
}
```

配置index.js文件中`  proxyTable: {},`

在本地环境和其他环境数据获取地址

功能是 Webpack-dev-server 提供

```js
    // Paths
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {
      '/api': {
        target: 'http://localhost:8183',
        pathRewrite: {
          '^/api': '/static/mock'
        }
      }
    },
```

#### 6. Vuex的使用

vuex 单项数据的改变流程

**核心概念**

  - State
  - Getters
  - Mutations
  - Actions
  - Modules

#### 7. vouter的使用
```js
this.$router.push('/')
```

#### 8. localStorage

本地存储
建议在外层加try catch 
不然当用户使用隐身模式，或者关闭本地存储的话，会报错
```js
let defaultCity = '广州'
try {
    if (localStorage.city) {
        defaultCity = localStorage.city
    }
} catch (e) {}
export default {
    // city: localStorage.city || '广州'
    city: defaultCity
}

```

#### 9. mapState

```js
import {mapState} from 'vuex'

computed: {
  ...mapState({
    currentCity: 'city'
  })
}

```


#### 【讨论题】对前端数据管理框架，你有怎样的理解？
当系统比较复杂，跨页面和跨多级组件传值情况出现较多时，就需要数据管理框架来帮助我们管理通用数据，比如 VueX，Redux，Mbox 等等。你对这些数据管理框架，设计和使用的经验有多少，对其底层实现原理又有多少了解呢？

关键提炼：

<ol>
<li>VueX 的实现原理是什么？</li>
<li>为什么说我们其实可以通过 Vue 实例来自己实现一个 VueX？</li>
<li>为什么 VueX，Redux 这样的数据框架，要求数据转化必须遵守一定标准的流程？</li>
<li>所有的数据都存放在数据管理框架中，有什么好处？有什么坏处？</li>
<li>在你的项目中，倾向于把所有数据存储在数据管理框架中，还是仅仅把通用数据放在数据管理框架中？</li>
</ol>


#### 10. Keepalive 提升性能

每一次路由发生切换的时候，ajax都重新启动加载。
mouted 钩子重新启动
keep-alive  vue内置，再加载时从内存调用

```
  <keep-alive>
    <router-view/>
  </keep-alive>
```
使用keepalive，会多出一个生命周期函数`activated `
当页面重新显示时，`activated `执行

```js
  mounted () {
    this.lastCity = this.city
    this.getHomeInfo()
  },
  activated () {
    if (this.lastCity !== this.city) {
      this.lastCity = this.city
      this.getHomeInfo()
    }
  }
```

`exclude="Detail"` exclude 选择对应的页面不缓存

```vue
    <keep-alive exclude="Detail">
      <router-view/>
    </keep-alive>
```

每次进入页面`mounted`钩子都会重新执行

```
  mounted () {==
    this.getHomeInfo()
  }
```

`exclude` 去掉缓存之后 ，`activated` 和 `deactivated` 生命周期钩子会失效，因此要换成 `mounted` 和 `destroyed`

```js
	mounted () {
		window.addEventListener('scroll', this.handleScroll)
	},
	destroyed () {
		window.removeEventListener('scroll', this.handleScroll)
	}
```





#### 11. CSS 解决300ms问题

**触摸动作**也经常用于完全解决由支持双击缩放手势引起的点击事件的延迟。

```css
html {
  touch-action: manipulation;
}
```

**touch-action**

CSS属性 **`touch-action`** 用于设置触摸屏用户如何操纵元素的区域(例如，浏览器内置的缩放功能)。

```css
/* Keyword values */
touch-action: auto;
touch-action: none;
touch-action: pan-x;
touch-action: pan-left;
touch-action: pan-right;
touch-action: pan-y;
touch-action: pan-up;
touch-action: pan-down;
touch-action: pinch-zoom;
touch-action: manipulation;

/* Global values */
touch-action: inherit;
touch-action: initial;
touch-action: unset;
```

```
touch-action: auto | 浏览器会根据其支持的触控添加交互。比如x轴滚动、y轴滚动、双指缩放和双击。
touch-action: none | 浏览器禁用触摸交互。
touch-action: pan-x | 允许浏览器水平滚动，禁用垂直滚动及手势。
touch-action: pan-y | 允许浏览器垂直滚动，禁用水平滚动及手势。
touch-action: manipulation | 允许浏览器双方向滚动，也允许双指缩放；但忽略其他手势。
```

**[touch-action](https://developer.mozilla.org/zh-CN/docs/Web/CSS/touch-action)**



#### 12. vue组件

例如一个主文件Detail和组件文件夹components

```
export default {
    name: 'Detail',
}
```

name的用途，递归组件会用到，页面想对某个页面取消缓存，以及对应组件名字



主文件Detail.vue

```vue
<template>
    <div>
       <detail-banner></detail-banner>
    </div>
</template>
<script>
import DetailBanner from './components/Banner'
export default {
    name: 'Detail',
    components: {
      DetailBanner
    }
}
</script>
<style lang="stylus" scoped>
  @import '~styles/mixins.styl'
</style>

```

components/Banner.vue

```vue
<template>
    <div>
        <div class="banner" @click="handleBannerClick">
            <img class="banner-img" src="https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/1/3/16812ae616c420f4~tplv-t2oaga2asx-watermark.awebp" alt="">
            <div class="banner-info">
                <div class="banner-title">aasda</div>
                <div class="banner-number"><span class="iconfont banner-icon">&#xe607;</span>99</div>
            </div>

        </div>
        <common-gallary
            :imgs="imgs"
            v-show="showGallary"
            @close="handleGallaryClose"></common-gallary>
    </div>
</template>
<script>
import CommonGallary from 'common/gallary/Gallary'
export default {
    name: 'DetailBanner',
    data () {
        return {
            showGallary: false,
            imgs: ['https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bd07aa48b85d40bb9518da9dae0d63ea~tplv-k3u1fbpfcp-zoom-crop-mark:1304:1304:1304:734.awebp', 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/54b9552d07e3448c807df981f265eda1~tplv-k3u1fbpfcp-zoom-crop-mark:1304:1304:1304:734.awebp']
        }
    },
    components: {
        CommonGallary
    },
    methods: {
        handleBannerClick () {
            this.showGallary = true
        },
        handleGallaryClose () {
            this.showGallary = false
        }
    }
}
</script>
<style lang="stylus" scoped>
  @import '~styles/mixins.styl'
</style>
```



#### 13. 滚动行为

页面的滑动会影响到其他页面，解决方法是将滚动行为添加在index.js文件中

```
    scrollBehavior (to, from, savadPosition) {
      return { x: 0, y: 0 }
    }
```

意思是每次做路由切换时，新显示的页面x和y轴初始位置为0



#### 14. scrollTop 在某些浏览器会失效，因此需要修复兼容性

```
const top = document.documentElement.scrollTop || document.body.scrollTop || window.pageYOffset;
```



#### 15.Vue 项目的接口联调

Vue项目的联调测试上线 - 项目的前后端联调

调用本地mock 模拟数据

`config.index.js`

```js
'use strict'
// Template version: 1.3.1
// see http://vuejs-templates.github.io/webpack for documentation.

const path = require('path')

module.exports = {
  dev: {

    // Paths -- Webpack-dev-server
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {
      '/api': {
        target: 'http://localhost:8181',
        pathRewrite: {
          '^/api': '/static/mock'
        }
      }
    },

    // Various Dev Server settings
    host: 'localhost', // can be overwritten by process.env.HOST
    port: 8181, // can be overwritten by process.env.PORT, if port is in use, a free one will be determined
    autoOpenBrowser: false,
    errorOverlay: true,
    notifyOnErrors: true,
    poll: false, // https://webpack.js.org/configuration/dev-server/#devserver-watchoptions-

    // Use Eslint Loader?
    // If true, your code will be linted during bundling and
    // linting errors and warnings will be shown in the console.
    useEslint: true,
    // If true, eslint errors and warnings will also be shown in the error overlay
    // in the browser.
    showEslintErrorsInOverlay: false,

    /**
     * Source Maps
     */

    // https://webpack.js.org/configuration/devtool/#development
    devtool: 'cheap-module-eval-source-map',

    // If you have problems debugging vue-files in devtools,
    // set this to false - it *may* help
    // https://vue-loader.vuejs.org/en/options.html#cachebusting
    cacheBusting: true,

    cssSourceMap: true
  },

  build: {
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',

    /**
     * Source Maps
     */

    productionSourceMap: true,
    // https://webpack.js.org/configuration/devtool/#production
    devtool: '#source-map',

    // Gzip off by default as many popular static hosts such as
    // Surge or Netlify already gzip all static assets for you.
    // Before setting to `true`, make sure to:
    // npm install --save-dev compression-webpack-plugin
    productionGzip: false,
    productionGzipExtensions: ['js', 'css'],

    // Run the build command with an extra argument to
    // View the bundle analyzer report after build finishes:
    // `npm run build --report`
    // Set to `true` or `false` to always turn it on or off
    bundleAnalyzerReport: process.env.npm_config_report
  }
}
```

联调接口时，去掉rewrite代码即可。

```
pathRewrite: {
'^/api': '/static/mock'
}
```

再重启前端服务器即可。





#### 【思考】你是如何进行代码调试的？

<ol>
<li>当控制台报错时，你解决问题的思路是什么？</li>
<li>当某个页面展示不出来时，你的处理思路是什么？</li>
<li>当某些具体逻辑执行结果不对时，你的处理思路是什么？</li>
<li>console.log 输出调试问题还是 debug 断点调试，你更喜欢那种方式，为什么？</li>
</ol>



#### 16. 真机测试

`ipconfig` 获取IP

如果想通过IP地址访问

需要在`package.json` 文件中在webpack启动增加host服务

原代码

```json
  "scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "lint": "eslint --ext .js,.vue src",
    "build": "node build/build.js"
  },
```

在`"dev"`启动项中增加`--host 0.0.0.0`

```json
"dev": "webpack-dev-server --host 0.0.0.0 --inline --progress --config build/webpack.dev.conf.js",
```

然后`npm run dev`重启服务器



#### 17. 修复不同设备可能不支持`promise` 安装包

`index.js` 引入 import 'babel-polyfill'

```bash
 npm install babel-polyfill --save
```



#### 18. Vue项目的打包上线

打包编译代码，默认存放到生成的`dist`文件夹。

```bash
npm run build
```

如果想修改打包生成的目录名，则是修改`index.js`的`build`配置

修改`assetsPublicPath: '/',`的配置即可，比如需要存到project文件夹下，如下：

`assetsPublicPath: '/project',`

生成`dist`文件夹的话，再修改成`project`放到环境下跑即可。

默认配置文件：

```js
  build: {
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',

    /**
     * Source Maps
     */

    productionSourceMap: true,
    // https://webpack.js.org/configuration/devtool/#production
    devtool: '#source-map',

    // Gzip off by default as many popular static hosts such as
    // Surge or Netlify already gzip all static assets for you.
    // Before setting to `true`, make sure to:
    // npm install --save-dev compression-webpack-plugin
    productionGzip: false,
    productionGzipExtensions: ['js', 'css'],

    // Run the build command with an extra argument to
    // View the bundle analyzer report after build finishes:
    // `npm run build --report`
    // Set to `true` or `false` to always turn it on or off
    bundleAnalyzerReport: process.env.npm_config_report
  }
```



#### 19. 异步组件实现按需加载

```js
Vue.use(Router)
export default new Router({
  routes: [{
      path: '/',
      name: 'Home',
      component: () => import('@/pages/home/Home')
    }, {
      path: '/city',
      name: 'City',
      component: () => import('@/pages/city/City')
    }, {
      path: '/detail/:id',
      name: 'Detail',
      component: () => import('@/pages/detail/Detail')
    }],
    scrollBehavior (to, from, savadPosition) {
      return { x: 0, y: 0 }
    }
})

```

`HomeHeader: () => import('./components/Header.vue'),`

使用箭头函数来按需加载组件。

当项目庞大时才使用，会增加https请求。



#### 20. 总结

学习思路

边缘知识熟悉

生态系统

- `vue-router`
- `vuex`
- vue服务器端渲染

资源列表

- 常用插件

Vue源码

webpack

babel

ES6

