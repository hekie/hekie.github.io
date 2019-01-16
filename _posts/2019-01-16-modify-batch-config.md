---
title: modify batch config
excerpt: node.js 批量修改配置文件
tags: node batch
---

#### node.js 批量修改配置文件

```javascript
const fs = require('fs')
const path = require('path')
const bse = path.resolve(process.argv[2] || '.')
// console.log(`base: ${base}`)

const srcs = ['product1', 'product2']
const vers = ['debug', 'release']

loopConfig()

function loopConfig() {
  srcs.forEach(src => {
    src = path.join(base, src)
    fs.readdir(src, { withFileTypes: true }, (err, files) => {
      if(err) {
        console.log(err)
        return
      }
      files.forEach(file => {
        if(file.isDirectory()) {
          vers.forEach(ver => {
            modifyConfig(path.join(src, file.name, 'actual path', `config_${file.name}_${ver}`), `config_${file.name}_${ver}`)
          })
        }
      })
    })
  })
}

function modifyConfig(fpath, fname) {
  // console.log((fpath)
  fs.readFile(fpath, { encoding: 'utf-8' }, (err, data) => {
    if(err) {
      console.log(err)
      return
    }
    // console.log(data)
    let newData = data.replace('old', 'new')
    fs.writeFile(fpath, newData, 'utf-8', err => {
      if(err) throw err
      console.log(`${fname}: success`)
    })
  })
}
```
