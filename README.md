# 操作日志

## 前言

使用 Vue + Vue-router + Element-ui 搭建的一个最小可运行的dashboard

涉及的技术如下：

* Vue

* Vue-router

* Element-ui

* webpack

* Normalize.css

* vue-awesome

* babel

## ## 一、初始化
1.安装vue-cli：
```bash
npm install vue-cli -g
```

2.用vue-cli构建一个项目：
```bash
vue init webpack vue-el-dashboard
```

3.安装cnpm：
```bash
npm install cnpm -g --registry=https://registry.npm.taobao.org
```

4.运行项目：
```bash
cd my-vue-project 

npm run dev
```

## 二、项目文件解读
```bash

├── node_modules                    # 项目依赖包文件夹
├── build                           # 编译配置文件，一般不用管
│   ├── build.js
│   ├── check-versions.js
│   ├── logo.png
│   ├── utils.js
│   ├── vue-loader.conf.js
│   ├── webpack.base.conf.js
│   ├── webpack.dev.conf.js
│   └── webpack.prod.conf.js
├── config                           # 项目基本设置文件夹
│   ├── dev.env.js                   # 开发配置文件
│   ├── index.js                     # 配置主文件
│   └── prod.env.js                  # 编译配置文件
├── src                              # 项目源码编写文件
│   ├── App.vue                      # APP入口文件
│   ├── assets                       # 初始项目资源目录，回头删掉
│   │   └── logo.png
│   ├── components                   # 组件目录
│   │   └── Hello.vue                # 测试组件，回头删除
│   ├── main.js                      # 主配置文件
│   └── router                       # 路由配置文件夹
│       └── index.js                 # 路由配置文件
└── static                           # 资源放置目录
├── index.html                       # 项目入口html模板
├── package.json                     # 项目依赖包配置文件
├── .babelrc                         # babel 配置
├── .postcssrc.js                    # postcss 配置
├── .editorconfig                    # editor 配置
└── README.md                        # 项目说明文档
```

## 三、配置src和static目录
src目录：
```bash
├── api                           // 接口调用工具文件夹
│   └── index.js                   
├── components                    // 组件文件夹
│    ├── header.vue                
│    └── footer.vue                  
├── page                          // 页面文件夹
│   ├── content.vue               // 内容页面
│   └── index.vue                 // 首页列表
├── router                        // 路由配置文件夹
│   └── index.js                
├── store                         // vuex状态管理目录    
├── style                         // scss 样式存放目录
│   └── style.scss                // 主样式文件，可以按分类创建多个文件夹
└── utils                         // 常用工具文件夹
│   └── index.js                    
├── App.vue                       // APP入口文件
└── main.js                       // 项目配置文件
```

static目录：
```bash
├── css               # 放第三方的样式文件
├── font              # 放字体图标文件
├── image             # 放图片文件，里面可以根据图片种类创建文件夹
└── js                # 放第三方的JS文件，比如datepicker
```

## 四、安装初始化页面布局
1.安装并使用Element UI：
```bash
cnpm i element-ui -S
```

2.修改 /src/main.js 为：
```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import router from './router'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'

import App from './App'

Vue.config.productionTip = false

Vue.use(ElementUI)

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})

```

3.修改/src/App.vue文件为：
```html
<template>
  <div id="app">
    <el-container>
      <el-aside width="200px">Aside</el-aside>
      <el-container>
        <el-header>Header</el-header>
        <el-main>Main</el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
</style>

```

## 五、安装侧边菜单栏
1.在components文件夹下新建NavMenu.vue：
```html
<template>
  <el-row class="tac">
    <el-col :span="12">
      <h5>默认颜色</h5>
      <el-menu default-active="2" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose">
        <el-submenu index="1">
          <template slot="title">
            <i class="el-icon-location"></i>
            <span>导航一</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="1-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="1-4">
            <template slot="title">选项4</template>
            <el-menu-item index="1-4-1">选项1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-menu-item index="2">
          <i class="el-icon-menu"></i>
          <span slot="title">导航二</span>
        </el-menu-item>
        <el-menu-item index="3">
          <i class="el-icon-setting"></i>
          <span slot="title">导航三</span>
        </el-menu-item>
      </el-menu>
    </el-col>
    <el-col :span="12">
      <h5>自定义颜色</h5>
      <el-menu default-active="2" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose" background-color="#545c64" text-color="#fff" active-text-color="#ffd04b">
        <el-submenu index="1">
          <template slot="title">
            <i class="el-icon-location"></i>
            <span>导航一</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="1-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="1-4">
            <template slot="title">选项4</template>
            <el-menu-item index="1-4-1">选项1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-menu-item index="2">
          <i class="el-icon-menu"></i>
          <span slot="title">导航二</span>
        </el-menu-item>
        <el-menu-item index="3">
          <i class="el-icon-setting"></i>
          <span slot="title">导航三</span>
        </el-menu-item>
      </el-menu>
    </el-col>
  </el-row>
</template>

<style>
</style>

<script>
export default {
  methods: {
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    }
  }
}
</script>

```

2.将NavMenu组件导入到App.vue中, 修改App.vue：
```html
<template>
  <div id="app">
    <el-container>
      <el-aside width="200px">
        <navmenu></navmenu>
      </el-aside>
      <el-container>
        <el-header>Header</el-header>
        <el-main>Main</el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import NavMenu from '@/components/NavMenu'

export default {
  name: 'App',
  components: {
    'navmenu': NavMenu
  }
}
</script>

<style>
</style>

```

3.修改NavMenu.vue文件,只保留右边的菜单：

其中有两个参数需要注意：

* unique-opened: 是否只保持一个子菜单的展开

* router: 是否使用 vue-router 的模式，启用该模式会在激活导航时以 index 作为 path 进行路由跳转

```html
<template>
  <el-row class="tac">
    <el-col :span="24">
      <el-menu default-active="2" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose" unique-opened router background-color="#545c64" text-color="#fff" active-text-color="#ffd04b">
        <el-submenu index="1">
          <template slot="title">
            <i class="el-icon-location"></i>
            <span>导航一</span>
          </template>
          <el-menu-item-group>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
            <el-menu-item index="1-3">选项3</el-menu-item>
            <el-menu-item index="1-4">选项4</el-menu-item>
          </el-menu-item-group>
        </el-submenu>
        <el-submenu index="2">
          <template slot="title">
            <i class="el-icon-location"></i>
            <span>导航二</span>
          </template>
          <el-menu-item-group>
            <el-menu-item index="2-1">选项1</el-menu-item>
            <el-menu-item index="2-2">选项2</el-menu-item>
            <el-menu-item index="2-3">选项3</el-menu-item>
            <el-menu-item index="2-4">选项4</el-menu-item>
          </el-menu-item-group>
        </el-submenu>
      </el-menu>
    </el-col>
  </el-row>
</template>

<style>
</style>

<script>
export default {
  methods: {
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    }
  }
}
</script>

```

4.通过配置文件渲染侧边菜单栏

在src目录下创建一个config目录，目录下创建一个menu-config.js 文件：

外层的数组代表一级菜单，内层sub数组代表二级菜单。
```javascript
module.exports = [{
  name: '基础',
  id: 'basic',
  sub: [{
    name: 'Layout 布局',
    componentName: 'BasicLayout'
  }, {
    name: 'Container 布局容器',
    componentName: 'BasicContainer'
  }]
}, {
  name: 'Form',
  id: 'form',
  sub: [{
    name: 'Radio 单选框',
    componentName: 'FormRadio'
  }, {
    name: 'Checkbox 多选框',
    componentName: 'FormCheckbox'
  }]
}]

```

修改NavMenu.vue如下：
```html
<template>
  <el-row class="tac">
    <el-col :span="24">
      <el-menu default-active="2" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose" unique-opened router background-color="#545c64" text-color="#fff" active-text-color="#ffd04b">
        <el-submenu v-for="item in menu" :index="item.id" :key="item.id">
          <template slot="title">
            <span v-text="item.name"></span>
          </template>
          <el-menu-item-group class="over-hide" v-for="sub in item.sub" :key="sub.componentName">
            <el-menu-item :index="sub.componentName" v-text="sub.name">
            </el-menu-item>
          </el-menu-item-group>
        </el-submenu>
      </el-menu>
    </el-col>
  </el-row>
</template>

<style scoped>
  .over-hide{
    overflow: hidden;
  }
</style>

<script>
import menu from '@/config/menu-config'

export default {
  data () {
    return {
      menu: menu
    }
  },
  methods: {
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    }
  }
}
</script>

```

## 六、安装头部
1.在componets文件夹下创建一个Header.vue, 并在App.vue中引入

Header.vue
```html
<template>
  <el-row>
    <el-col :span="24">
      <div class="head-wrap">Element</div>
    </el-col>
  </el-row>
</template>

<style scoped>
.head-wrap{

}
</style>

<script>
export default {
}
</script>

```

App.vue
```html
<template>
  <div id="app">
    <el-container>
      <el-aside width="200px">
        <navmenu></navmenu>
      </el-aside>
      <el-container>
        <el-header class="header">
          <vheader />
      </el-header>
        <el-main>Main</el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import NavMenu from '@/components/NavMenu'
import Header from '@/components/Header'

export default {
  name: 'App',
  components: {
    'navmenu': NavMenu,
    'vheader': Header
  }
}
</script>

<style>
.header {
  background-color: #409EFF;
  color: #fff;
  line-height: 60px;
}
</style>

```

**打开浏览器查看：http://localhost:8080/#/**

发现body有边框，我们将进一步美化。

## 七、美化

* 使用[css reset Normalize.css](http://necolas.github.io/normalize.css/)

* 使用[font-awesome vue-awesome图标库](https://github.com/Justineo/vue-awesome)

1.安装Normalize.css, vue-awesome
```bash
cnpm i normalize.css -D
cnpm i vue-awesome -D
```

2.修改main.js
```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import NormailizeCss from 'normalize.css'
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'

import App from './App'
import router from './router'

Vue.config.productionTip = false

Vue.use(ElementUI)
Vue.component('icon', Icon)

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})

```

3.修改menu-config.js
```javascript
module.exports = [{
  name: '基础',
  id: 'basic',
  icon: 'th-large',
  sub: [{
    name: 'Layout 布局',
    componentName: 'BasicLayout'
  }, {
    name: 'Container 布局容器',
    componentName: 'BasicContainer'
  }]
}, {
  name: 'Form',
  id: 'form',
  icon: 'align-left',
  sub: [{
    name: 'Radio 单选框',
    componentName: 'FormRadio'
  }, {
    name: 'Checkbox 多选框',
    componentName: 'FormCheckbox'
  }]
}]

```

4.修改NavMenu.vue
```html
<template>
  <el-row class="tac">
    <el-col :span="24">
      <el-menu
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose"
      unique-opened
      router
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b">
        <el-submenu v-for="item in menu" :index="item.id" :key="item.id">
          <template slot="title">
            <icon :name="item.icon"></icon>
            <span v-text="item.name"></span>
          </template>
          <el-menu-item-group class="over-hide" v-for="sub in item.sub" :key="sub.componentName">
            <el-menu-item :index="sub.componentName" v-text="sub.name">
            </el-menu-item>
          </el-menu-item-group>
        </el-submenu>
      </el-menu>
    </el-col>
  </el-row>
</template>

<style scoped>
  .over-hide{
    overflow: hidden
  }
</style>

<script>
import menu from '@/config/menu-config'

export default {
  data () {
    return {
      menu: menu
    }
  },
  methods: {
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    }
  }
}
</script>

```

5.修改Header.vue
```html
<template>
  <el-row>
    <el-col :span="24">
      <div class="head-wrap"><icon name="cogs"></icon> Element</div>
    </el-col>
  </el-row>
</template>

<style scoped>
.head-wrap{

}
</style>

<script>
export default {
}
</script>

```

## 八、组件路由与懒加载

1.在components新增四个文件：

BasicContainer.vue
```html
<template>
  <div>
    这是：Container 布局容器
  </div>
</template>
```

BasicLayout.vue
```html
<template>
  <div>
    这是：Layout 布局
  </div>
</template>
```

FormCheckbox.vue
```html
<template>
  <div>
    这是：Checkbox 多选框
  </div>
</template>
```

FormRadio.vue
```html
<template>
  <div>
    这是：Radio 单选框
  </div>
</template>
```

2.安装syntax-dynamic-import插件：
```bash
cnpm install --save-dev babel-plugin-syntax-dynamic-import
```

3.修改router/index.js文件：
```javascript
import Vue from 'vue'
import Router from 'vue-router'
import menus from '@/config/menu-config'

Vue.use(Router)

var routes = []

menus.forEach((item) => {
  item.sub.forEach((sub) => {
    routes.push({
      path: `/${sub.componentName}`,
      name: sub.componentName,
      component: () => import(`@/components/${sub.componentName}`)
    })
  })
})

export default new Router({ routes })

```

4.App.vue文件需要加上 <router-view>
```html
<el-main>
  <router-view></router-view>
</el-main>
```

## 总结
以上为使用 Vue + Vue-router + Element-ui 搭建的一个最小可运行的dashboard，如有疑问，欢迎探讨交流。