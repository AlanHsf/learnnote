### node.js 简介

- node.js 是一个基于chrome v8 引擎的javascript 运行环境
  - v8引擎
  - fs  文件读取模块
  - path 路径
  - http
  - js内置对象
  - querystring
  - etc
- node.js 可以做什么
  - 基于Express 框架 快速构建Web应用
  - 基于Electron 框架可以构建跨平台桌面应用
  - 基于restify 可以快速构建API 接口项目
  - 读写操作数据库


#### fs文件系统模块

- fs模块是Node.js 官方提供的用来操作文件的模块，它提供了一系列方法和属性

  ```javascript
  // 引用fs 模块
  const fs = require('fs') 
  
  // 读取文件的中的内容
  
  // 参数的解读
  
  ```

##### 读取文件中的内容

- 参数使用中括号包裹起来的就是可选参数

- fs.readFile(path，option， callback) 

  - 参数1：必填参数 字符串 表示文件的路径

  - 参数2：可选参数，表示以什么编码格式来读取文件

  - 参数3：必填参数，读取文件之后通过回调函数来读取结果

  - 示例代码

  - ```javascript
    const fs = require('fs')
    
    fs.readFile('./file/test.text', 'utf8',function(err,dataStr) {
        console.log(err)
        // 判断文件是否读取文件成功， 判断err 是否存在，存在则读取失败
        console.log(dataStr)
        if(err) {
            return console.log("文件读取失败" + err.message)
        }else {
            console.log('文件读取成功')
        }
    })
    ```

- 向指定文件中写入内容 fs.writeFile() 的语法格式

  - 使用fs.writeFile()方法，可以向指定文件中写人内容

  - 参数1：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径

  - 参数2：必选参数，表示写入的内容

  - 参数3：可选参数，表示以什么格式写入文件内容，默认是utf8

  - 参数4：必选参数。写入完成之后的回调路径

    ```javascript
    let fs =require('fs')
    
    fs.writeFile('D:/test.txt','abcd','utf8', function(err) {
        console.log(err)
        if(err) {
         // 写入失败   
          return  console.log('写入失败' + err.message)
        }else {
         // 写入成功
          console.log('文件写入成功')
        }
    })  
    ```

    

- 练习：成绩整理

  ```javascript
  const fs = requir('fs')
  
  fs.readFile('../素材/成绩txt', 'uft8', function(err,dataStr) {
      if(err) {
          return console.log('读取失败')
      }
      // 成绩数据 小红=90 小明=100
      // 先将成绩数据按照空格分隔
      const arrOld = dataStr.split(' ')
      let arrNew = []
      arrOld.forEach(item => {
          arrNew.push(item.replace('=', ':'))
      })
      // 把新数组中的每一项进行合并，得到一个新的字符串
     let newStr = arrNew.join('\r\n')
     
     // 使用fs.writeFile() 方法
     fs.writeFile('../素材/成绩-ok.txt', newStr, 'utf8', 			function(err) {
         if(err) {
             return console.log('写入失败'+ err.message)
         }else {
             console.log('写入成功')
         }
     })
      
  })
  ```

  

- fs 模块-路径动态拼接的问题

  - 使用fs 模块操作文件的时候，如果提供操作的路径是 ./ 或者 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题

  - 原因：代码运行的时候，会以执行node 命令时所处的目录，动态拼接出被操作的文件完整的路径

  - 解决方案：不适用相对路径，直接提供一个完整存放路径 ，弊端：移植性非常差，不利于维护

  - __dirname，表示当前文件所处的目录

    

    

##### path 路径模块

- 什么是path 路径模块
  - path 模块是node.js 官方提供的，用来处理路径的模块，它提供了一系列的方法和属性，用来满足用户对路径的处理需求
  - path.join() 方法 ，用来将多个路径片段拼接成一个完整的路径字符串
  - path.basename() 方法 用来从路径字符串，将文件名解析出来

- path.join() 的语法格式

  - 使用path.join 方法，可以把多个路径片段拼接为完整的路径字符串，

  - path.join([...paths])

  - ...paths<string> 路径片段序列

  - 返回值<string>

    ```javascript
    const path = require('path')
    const  fs = require('fs')
    // ../ 会抵消前面的路径
    let pathStr = path('a', '/b/c', '../', './d', 'e')
    
    console.log(pathStr) // \a\b\d\e
    
    fs.readFile(path.join(__dirname, '/files/1.text'),'utf8', function() {
        if(err) {
            return console.log(err.message)
        }
    })
    
    
    ```

    

- 获取路径中文件名 path.basename()
  - 使用path.basename() 方法 可以从一个文件路径中获取文件的名称部分

```javascript
const path = require('path')

const fpath = 'a/b/c/index.html'

const fullName = path.basename(fpath)

const nameWithOutExt = path.basename(fpath, 'html')
```





- path.extname() 获取文件中文件的扩展名

  ```javascript
  const path = require('path')
  
  const fpaht = 'a/b/c/index.html'
  
  const fext = path.extname(fpath)
  
  ```

###### 综合练习

- 案例实现步骤
  - 创建两个正则表达式，分别来匹配<style> 和 <script>标签
  - 使用fs 模块 读取需要被处理的HTML 文件
  - 自定义resolveCSS 方法 来写入index.css 样式文件
  - 自定义resolveJS 方法 来写入index.js 脚本文件
  - 自定义 resolve HTML方法 来写入index.html 文件



```javascript
const fs =require('fs')

const path = require('path')

// 匹配<style></style> 标签的正则
// \s 表示空白字符 \S 表示非空白字符 * 表示匹配任意次
const regStyle = /<style>[\s\S]*<\/style>/

const regScript = /<script>[\s\S]*<\/script>/

fs.readFile(path.join(__dirname, '../素材/index.html'), 'utf8', function(err, dataStr) {
    if(err) {
        return console.log(err.message)
    }
    // 读取成功后，调对应的三个方法
    resolveCSS(dataStr)
    resolveJS(dataStr)
    resolveHtml(dataStr)
})


function resolveCSS(htmlStr) {
    let r1 = regStyle.exec(htmlStr)
    // 将提取出来的样式字符串进行字符串的replace 替换操作
    let newCSS = r1[0].replace('<style>', '').replace('</style>', '')
    
    fs.readFilr(path.join(__dirname, '/clock/index.css'), newCSS, 'utf8', function(err){
        if(err) {
            return console.log('写入样式文件失败'+ err.message)
        }
        console.log('写人样式文件成功')
    })
    
    
}

function resolveJS(htmlStr) {
    let r1 = regScript.exec(htmlStr)
    // 将提取出来的样式字符串进行字符串的replace 替换操作
    let newJS = r1[0].replace('<script>', '').replace('</script>', '')
    
    fs.readFilr(path.join(__dirname, '/clock/index.js'), newJS, 'utf8', function(err){
        if(err) {
            return console.log('写入JS文件失败'+ err.message)
        }
        console.log('写人JS文件成功')
    })
    
    
}


function resolveHTML(htmlStr) {
    // 将提取出来的样式字符串进行字符串的replace 替换操作
    let newHtml = htmlStr.repalce(regStyle, '<link rel="stylesheet" href="./index.css">').replace(regScript, '<script scr="./index.js"></script>')
    
    fs.readFilr(path.join(__dirname, '/clock/index.html'), newHtml, 'utf8', function(err){
        if(err) {
            return console.log('写入HTML文件失败'+ err.message)
        }
        console.log('写人HTML文件成功')
    })
}
```



##### http 模块

- 什么是客户端，什么是服务端
  - 在网络节点中，负责消费资源的电脑叫做客户端，负责对外提供网络资源的电脑叫做服务器
- http 模块是node.js 官方提供的用来创建web服务器的模块，通过http模块提供的http.createServer() 方法就能方便的把一台普通的电脑变成一台web 服务器，从而对外界提供web资源服务
- 服务器和普通电脑的区别就是服务器上安装了web服务器软件，比如IIS Apache 等，通过安装服务器软件就能把一台普通的电脑变成一台web服务器
- IP地址：IP地址就是互联网上每台计算机的唯一地址，因此IP地址具有唯一性，ip地址的格式，通常用点分十进制，（a.b.c.d）的形式，其中a b c d都是0-255之间的十进制整数，例如 192.168.1.1

- 域名和域名服务器：IP地址能够唯一的标记网络上的计算机，但是IP地址是一长串数字，不直观，而且不便于记忆，于是人们发明了另外一套字符型的地址方案，域名地址，IP地址和域名是一一对应的关系，这份对应的关系存放在一种叫做域名服务器（DNS Domain name server）的电脑中，使用者只需要通过好记忆的域名访问对应的服务器即可，对应的转换工作由域名服务器实现，因此域名服务器就是提供IP地址和域名之间转换的服务器
- 端口号：计算机中端口号，就好像是现实生活中的门牌号一样，通过门牌号，外卖小哥可以在整栋大楼众多房间中准确把外卖送到你手中，同样的道理在一台服务器中可以运行成百上千的web服务，每一web服务都对应一个唯一的端口号，客户端发送过来的网络请求通过端口号可以准确的交给对应的web 服务进行处理
  - 每个端口号不能被多个web服务占用
  - 在实际应用中，url中的80端口可以被省略

###### 创建最基本的web服务器

- 创建web服务器实例

  - 导入http 模块 const http = require('http')

  - 创建web服务器实例 调用http.createServer() 方法，即可创建一个web服务器 const server = http.createServer()

  - 为服务器实例绑定request事件:为服务器实例绑定request 事件，即可监听客户端发送过来的网络请求 server.on('request', (req,res) => {

    })

  - 启动服务器：server.listen(80, () =>{})

```javascript
// server.js
const http = require('http')

const server = http.createdServer()

server.on('request', function(req,res) {
    console.log('visit our web server')
})

server.listen(7337, function() {
    console.log('server runing at http://127.0.0.1:7337')
})

```

- req 请求的对象 ：只要服务器接收到了客户端的请求，就会调用通过server.on() 为服务器绑定的request 事件处理函数，如果想在事件的处理函数中 访问与客户端相关的数据与属性

  ```javascript
  // server.js
  const http = require('http')
  
  const server = http.createdServer()
  
  server.on('request', function(req,res) {
      // 请求的地址路径
      const url = req.url
      // 请求的方法
      const method = req.method
      console.log('visit our web server')
  })
  
  server.listen(7337, function() {
      console.log('server runing at http://127.0.0.1:7337')
  })
  
  
  ```

- res 响应对象：在服务器的request 事件处理函数中，如果想访问与服务器相关的数据与属性，可以使用如下的方式

  ```javascript
  // server.js
  const http = require('http')
  
  const server = http.createdServer()
  
  server.on('request', function(req,res) {
      // 请求的地址路径
      const url = req.url
      // 请求的方法
      const method = req.method
      console.log('visit our web server')
      let str = `Your request url is ${url}, and request method is ${method}`
      // res.end()方法，向客户端响应一些内容
      res.end(str)
  })
  
  server.listen(7337, function() {
      console.log('server runing at http://127.0.0.1:7337')
  })
  ```

  

- 解决中文乱码的问题 res.setHeader('Content-type','text/html; charset=utf-8')

```javascript
server.on('request', function(req,res) {
    // 请求的地址路径
    const url = req.url
    // 请求的方法
    const method = req.method
    console.log('visit our web server')
    let str = `你请求的地址是 ${url},请求方法是 ${method}`
    // 调用res.setHeader()方法解决中文乱码的问题
    res.setHeader('Content-type','text/html; charset=utf-8')
    // res.end()方法，向客户端响应一些内容
    
    res.end(str)
})

```

- 请求不同的url 返回不同的数据

  - 获取请求的url地址

  - 设置默认响应的内容为404 not Found

  - 判断用户请求的是否为/ 或者 /index.html 首页

  - 判断用户请求的是否为/about.html

  -  设置content-type 响应头 防止中文乱码

  - 使用res.end() 把内容响应给客户端

    
