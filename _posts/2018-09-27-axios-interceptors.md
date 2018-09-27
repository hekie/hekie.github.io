---
title: axios interceptors
excerpt: axios 封装：登录鉴权、统一报错处理、跳转、拦截
tags: axios vue
---

**http.js**

```javascript
import axios from 'axios'
// import qs from 'qs'
import router from '@/router'
import store from '@/store'

// 创建 axios 实例
const instance = axios.create({
  // url 请求前缀
  // 生产环境 api 地址待定
  baseURL: process.env.VUE_APP_HOST + '/api',
  // 超时时间
  timeout: process.env.VUE_APP_TIMEOUT,
  // 请求头信息，默认为 json 格式
  headers: {
    'Content-Type': 'application/json;charset=utf-8'
    // 'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8'
  }
})

// request 拦截器
instance.interceptors.request.use(
  config => {
    config.headers.language = store.state.lang

    if (store.state.token) {
      // 请求头中带上 token 信息
      config.headers.authorization = store.state.token
    }

    // 如果后台能直接接收 json 格式数据，就可以不用 qs 来序列化
    // if ('post' === config.method) {
    //   // 请求类型为 post 时用 qs 格式化请求数据
    //   config.data = qs.stringify(config.data)
    // }

    return config
  },
  err => Promise.reject(err)
)

// response 拦截器
instance.interceptors.response.use(
  res => {
    if (!res.data) {
      // ie9 中 response.data 是 undefined
      // 因此需要使用 response.request.responseText（Stringify 后的字符串）
      res.data = JSON.parse(res.request.responseText)
    }

    // 成功处理
    if (!res.data.err) return res.data.data
    
    // 错误处理 （例如：缺少参数等）
    if ('ERR_CODE' === res.data.err) {
      alert(res.data.msg)
      return Promise.reject()
    }

    // 未登录的情况
    if ('NOT_SIGN_IN' === res.data.err) {
      store.commit('signOut')
      alert(`请重新登录`)
      goSignIn()
    }
  },
  // 用来在调用 axios 的时候通过 catch 获取接口返回的错误信息
  err => {
    // 请求失败（例如：404、500）
    alert(err.message)
    return Promise.reject()
  }
)

// 跳转到登录页面
// 带上 sendUrl 参数，登录成功后跳转到该页面
function goSignIn() {
  if ('signin' !== router.currentRoute.name) {
    router.replace({
      name: 'signin',
      query: {
        sendUrl: router.currentRoute.fullPath
      }
    })
  }
}

// 导出为 vue 插件
export default {
  install: Vue =>
    Object.defineProperty(Vue.prototype, '$http', { value: instance })
}

```

**router.js**

```javascript
import Vue from 'vue'
import Router from 'vue-router'
import store from '@/store'

Vue.use(Router)

const routes = [
  {
    path: '/',
    name: 'index',
    component: () => import(/* webpackChunkName: 'index' */ '@/views/index.vue')
  },
  {
    path: '/user',
    name: 'user',
    meta: { auth: true },
    component: () => import(/* webpackChunkName: 'user' */ '@/views/user.vue')
  },
  {
    path: '/signin',
    name: 'signin',
    component: () => import(/* webpackChunkName: 'signin' */ '@/views/signin.vue')
  },
  {
    path: '/register',
    name: 'register',
    component: () =>
      import(/* webpackChunkName: 'register' */ '@/views/register.vue')
  },
  {
    path: '/404',
    alias: '*',
    component: () => import(/* webpackChunkName: '404' */ '@/views/404.vue')
  }
]

const router = new Router({
  mode: process.env.VUE_APP_MODE, // 'history' or  'hash'
  base: process.env.VUE_APP_BASE,
  routes
})

router.beforeEach((to, from, next) => {
  if (to.matched.some(r => r.meta && r.meta.auth)) {
    // 需要登录之后才能进入的页面
    if (!store.getters.isSignedIn) {
      next({
        name: 'signin',
        query: {
          sendUrl: to.fullPath
        }
      })
      return
    }
  }
  next()
})

// /* eslint-disable no-unused-vars */
// router.afterEach((to, from) => {
//   document.title = to.meta && to.meta.title
// })

export default router
```
