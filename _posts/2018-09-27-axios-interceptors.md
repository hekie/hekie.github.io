---
title: axios interceptors
excerpt: axios 封装：登录鉴权、统一报错处理、跳转、拦截
tags: axios vue
---

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

    // 出错处理（例如：缺少参数等）
    if (1 === Number(res.data.err)) {
      alert(window._vm.$i18n.t(res.data.msg))
      return Promise.reject()
    }

    // 未登录
    if (2 === Number(res.data.err)) {
      store.commit('signOut')
      alert(`请重新登录`)
      goSignIn()
    }
  },
  // 用来在调用 axios 的时候通过 catch 获取接口返回的错误信息
  err => {
    // 请求失败（404，500，超时等）
    alert(err.message)
    return Promise.reject()
  }
)

// 跳转到登录页面
// 带上 sendUrl 参数，登录成功后跳转到该页面
function goSignIn() {
  if ('login' !== router.currentRoute.name) {
    router.replace({
      name: 'login',
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
