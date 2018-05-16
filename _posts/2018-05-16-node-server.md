---
title: 'Node.js 搭建本地服务器'
excerpt: '用 Node.js 快速搭建本地服务器，用于 Web 测试'
---

参考链接：
- [廖雪峰 JavaScript 全栈教程](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014345015296018cac40c198b543fead5c549865b9bd4a000)
- [3 分钟快速搭建 nodejs 本地服务器运行测试 html/js](https://blog.csdn.net/u011456337/article/details/50704331)

```javascript
const fs = require('fs')
const url = require('url')
const path = require('path')
const http = require('http')

// MIME 类型
const mime = {
  css: 'text/css',
  gif: 'image/gif',
  html: 'text/html',
  ico: 'image/x-icon',
  jpeg: 'image/jpeg',
  jpg: 'image/jpeg',
  js: 'text/javascript',
  json: 'application/json',
  pdf: 'application/pdf',
  png: 'image/png',
  svg: 'image/svg+xml',
  swf: 'application/x-shockwave-flash',
  tiff: 'image/tiff',
  txt: 'text/plain',
  wav: 'audio/x-wav',
  wma: 'audio/x-ms-wma',
  wmv: 'video/x-ms-wmv',
  xml: 'text/xml'
}

// 从命令行参数获取root目录，默认是当前目录
const root = path.resolve(process.argv[2] || '.')
console.log(`Static root dir: ${root}`)

// 创建服务器
const hostname = 'localhost'
const port = 3000
const server = http.createServer((req, res) => {
  // console.log(`${req.method}: ${req.url}`)
  // 获得URL的path：/css/style.css
  let pathname = url.parse(req.url).pathname

  // 获得对应的本地文件路径：/srv/www/css/style.css
  let filepath = path.join(root, pathname)

  // 获得文件扩展名
  let ext = path.extname(filepath)
  ext = ext ? ext.slice(1) : 'unknown'

  // 获取文件状态
  fs.stat(filepath, (err, stat) => {
    if (err) {
      res.statusCode = 404
      res.end('404 Not Found')
      return
    }

    // 如果当前路径是一个文件
    if (stat.isFile()) {
      res.statusCode = 200
      res.setHeader('Content-Type', mime[ext] || 'text/plain')
      fs.createReadStream(filepath).pipe(res)
      return
    }

    // 如果当前路径是一个目录
    if (stat.isDirectory()) {
      fs.readdir(filepath, (err, f) => {
        let list = ''
        if (req.url != '/') {
          list += `<a href="${path.join(pathname, '..')}">../</a><br>`
        }
        for(let i in f) {
          list += `<a href="${path.join(pathname, f[i])}">${f[i]}</a><br>`
        }
        res.statusCode = 200
        res.setHeader('Content-Type', 'text/html')
        res.end(list)
        // if (files.includes('index.html')) {
        //   res.statusCode = 200
        //   fs.createReadStream(path.join(filepath, 'index.html'), 'utf-8').pipe(res)
        // } else {
        //   res.statusCode = 404
        //   res.end('404 Not Found')
        // }
      })
    }
  })
})

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}`)
})

```
