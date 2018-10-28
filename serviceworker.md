
# service worker 
近两年前端比较热的话题之一就是PWA（Progressive Web APP）——渐进式网页，是谷歌推出的webapp实现方案；致力于实现与原生APP相似的交互体验。

* menifest实现手机主界面的web app图标、标题、开屏icon等
* service worker实现离线缓存请求、更新缓存、删除缓存；iOS safari在11.3系统已支持。
* push/notification实现消息推送及接收

看标题就知道，我们主要来说说service worker（以下简称SW）的实现方式

## service worker 是什么
在说SW之前，先来回顾下js的单线程问题。

众所周知，js在浏览器中是单线程运行的；主要是为了准确操作DOM。但单线程存在的问题是，UI线程和js线程需要抢占资源，在js执行耗时逻辑时，容易造成页面假死，用户体验较差。

由此出现了异步操作，可不影响主界面的响应。如ajax、promise等。
除此之外，还有html5开放的web worker可以在浏览器后台挂载新线程。它无法直接操作DOM，无法访问window、document、parent对象

SW是web worker的一种，也是挂载在浏览器后台的线程。它同样无访问window、document、parent对象；并且由于可以代理网页的请求并缓存返回结果的强大能力，浏览器要求必须是在https中使用。

在SW装载成功后，它作用域下的请求都可以代理缓存

## service worker可以解决的问题
* 用户多次访问网站时加快访问速度
* 离线缓存接口请求及文件，更新、清除缓存内容
* 可以在客户端通过 indexedDB API 保存持久化信息

## 生命周期
### 注册

### 安装

### 激活

### 运行

### 安装失败

### 进程销毁

## 使用方法


## debug

## 应用框架workbox
