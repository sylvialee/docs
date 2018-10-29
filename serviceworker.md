
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

SW是web worker的一种，也是挂载在浏览器后台运行的线程。主要用于代理网页请求，可缓存请求结果；可实现离线缓存功能。也拥有单独的作用域范围和运行环境

### sw使用限制
- 同源策略，缓存及拦截的请求必须与主线程同源
- 无法直接操作DOM对象，也无法访问window、document、parent对象。可以访问location、navigator
- 可代理的页面作用域限制。默认是sw.js所在文件目录及子目录的请求可代理，可在注册时手动设置作用域范围
- 必须在https中使用，允许开发调试的localhost使用

### SW兼容性
图片

## service worker可以解决的问题
* 用户多次访问网站时加快访问速度
* 离线缓存接口请求及文件，更新、清除缓存内容
* 可以在客户端通过 indexedDB API 保存持久化信息


## 生命周期
生命周期由5步：注册、安装成功（安装失败）、激活、运行、销毁
事件：install、activate、message、fetch、push、async

### 注册
在主线程中调起注册方法register

    if('serviceWorker' in navigator){
        navigator.serviceWorker
            .register('./sw.js', {scope: '/'})
            .then(reg => {
                console.log('注册成功')
            })
            .catch(error => {
                console.log('注册失败')
            })
    }else{
        console.log('当前浏览器不支持SW')
    }

### 安装
在服务线程中添加安装监听及对应需缓存的资源文件

    const CACHE_NAME = 'sylvia_cache'
    let filesToCache = [
        '/src/css/test.css',
        '/src/js/test.js'
    ]
    
    self.addEventListener('install', function(event){
        event.waitUntil(
            caches.open(CACHE_NAME).then(cache => {
                cache.addAll(filesToCache)
            })
        )
    })

### 激活
第一次注册并安装成功后，会触发activate事件

    self.addEventListener('activate', event => {
        console.log('安装成功，即将监听作用域下的所有页面')
    })

### 运行
安装并激活成功后，就可以对页面实行fetch监控啦。

- 可以过滤使用已缓存的请求，若无缓存，由fetch发起新的请求，并返回给页面



    self.addEventListener('activate', event => {
        event.
    })



- 也可连续将请求缓存到内存里
### 进程销毁

## 使用方法


## debug

## 应用框架workbox


