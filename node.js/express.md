# express

### 学习目标

- 学会使用express.static() 快速托管静态资源
- 学会使用express 路由精简项目结构
- 能使用expres 常见的express 中间件
- 能供使用express 创建API 接口
- 能在express 中启用cros 跨域资源共享

### 初始Express

- 官网：http://www.express.com.cn

#### 什么是Express

- 概念：Express 是基于Node.js平台快速 开放 极简 的web开发框架，通俗理解Express 的作用和node.js 内置的http模块类似 是专门来创建web服务器的

##### Express能做什么

- Web网站服务器
- API接口服务器

##### Express的基本使用

- 安装 npm install express

- 创建基本的Web 服务器

  ```js
  // 导入express
  const express = require('express')
  
  const app = express()
  
  app.listen(80, ()=> {
      console.log('express server runing')
  })
  
  ```

  ###### 监听GET请求

  - 通过app.get() 方法 可以监听客户端的get请求

    ```
    app.get('请求地址'，function(req,res) {
    	// req 请求对象  req.query可以获取客户端请求参数
    	// req.params 对象可以访问到URL中 通过:匹配动态参数
    	// res 响应对象
    })
    ```

  ###### 监听POST请求

  - 通过app.post() 方法 可以监听客户端的post请求

    ```js
    app.post('请求地址'，function(req,res) {
    	// req 请求对象 req.body可以获取客户端请求参数
    	// res 响应对象
    })
    ```

###### res.send() 返回数据

```
res.send()
```

###### express.static()  托管静态资源

- express.static() 通过他我们可以非常方便的创建一个静态资源服务器, 如果需要托管多个静态资源目多次调用express.static() 即可

- 挂载路径前缀

  ```js
  app.use(express.static('public'))
  app.use(express.static('public2'))
  
  // 挂载路径前缀 访问路径 http://127.0.0.1/public/img/xxx.png
  app.use('public', express.static('public') )
  
  
  ```

###### nodemon: nodemon(https://www.npmjs.com/package/nodemon) 这个工具能够监听项目文件的变动，当代码被修改后 nodemon会自动帮我们重启项目，方便开发

- 安装  npm install -g nodemon

- 使用 nodemon app.js

  



### Express路由

#### 路由的概念：广义上来讲 路由就是映射关系

#### Express 中的路由

- 在Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系
- Express 中的路由分为三部分 分别请求类型，请求的url 处理函数

#### 路由的匹配过程

- 当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后才会调用对应的处理函数

#### 模块化路由

-  tips ：app.use() 函数的作用 就是用来注册全局的中间件

- 为了方便对路由的进行模块化的管理，Express 不建议将路由直接挂载到app 上，而是推荐将路由抽离为单独的模块
- 1、创建路由模块对应的js 文件
- 2、调用express.Router() 函数 创建路由对象
- 3、向路由对象上挂载具体的路由
- 4、使用module.exports 向外共享路由对象
- 使用app.use() 函数注册路由模块
- 



### Express中间件

#### 什么是中间件



### 使用Express写接口

