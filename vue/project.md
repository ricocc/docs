# Vue 项目学习记录



####  1. 什么是路由?

路由就是根据网址的不同, 返回不同的内容给用户

#### 2. 什么是`<router-view/>`

显示的是当前路由地址所对应的内容

#### 3. `@` 指的是src目录,css文件中引入加`~`

````
import HelloWorld from '@/components/HelloWorld'
````

在css中引入其他的css文件,前面需要加`~`, 完整的就是`~@/路径`



#### style标签添加 scoped

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

```
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



配置index.js文件中`  proxyTable: {},`

在本地环境和其他环境数据获取地址

功能是 Webpack-dev-server 提供

```
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
