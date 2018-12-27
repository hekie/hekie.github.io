---
title: some small tips
excerpt: 工作中遇到的一些小问题及解决方法
tags: svn 
---

### SVN 常用命令

```bash
# 更新代码到本地
svn up

# svn checkout 的缩写，从服务器检出代码到指定路径（target 可选，默认同远程仓库文件夹名字）
svn co url [target]

# 查看最近的 num 条 svn 日志（参数可选，svn log 默认查看所有日志）
svn log [-l num]
```

### Linux 相关

```bash
# 文件读写权限管理
chmod 777 file

# 查看文件内容
cat file

# 查看网络配置
ifconfig
```


### Luci 学习

#### 要在 html 文件中嵌入 Lua 代码，请用 <%%> 包裹

```lua
-- 注释（支持多行）
<%# comments goes here -%>

-- 国际化（两端多余的空格会被保留）
<%: i18n key %>

-- 可执行的 Lua 代码（支持多行）
<% local a = '123' %>

-- 变量获取（两端空是格可选的）
<%= dataInfo %>

-- 包含公用文件（不能包含空格）
<%+header%>
```

#### 清除 Luci 缓存

```bash
rm -rf /tmp/luci-modulecache
```

#### 禁用 Luci 缓存

```bash
vi /etc/config/luci
配置项 ccache 的 enable 属性改为 '0'
```

### 其它

#### IE 下 placeholder 样式修改无效：把相关的样式定义分开写

```css
::-webkit-input-placeholder { color: #ccc; }
::-moz-placeholder { color: #ccc; }
:-ms-input-placeholder { color: #ccc; }
```

#### Chorme 自动填充背景色去除

```css
input:-webkit-autofill {
  box-shadow: 0 0 0 1000px #fff inset !important;
}
```

#### Linux shell 主机名变成 -bash-4.1$，不显示只能广场的用户名和主机名

原因：对应用户根目录下缺失了配置文件

```bash
＃ .bashrc
if [-f /etc/bashrc]; then
  . /etc/bashrc
fi


＃ .bash_profile
if [-f ~/.bashrc]; then
  . ~/.bashrc
fi

PATH=$PATH:$HOME/.local/bin:$HOME/bin
export PATH
```
