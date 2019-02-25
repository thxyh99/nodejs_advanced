## 全局对象与全局变量

### __filename
/web/com/runoob/nodejs/main.js

### __dirname
/web/com/runoob/nodejs

### util.inherits
util.inherits(constructor, superConstructor)是一个实现对象间原型继承 的函数。

JavaScript 的面向对象特性是基于原型的，与常见的基于类的不同。JavaScript 没有 提供对象继承的语言级别特性，而是通过原型复制来实现的

### util.inspect
util.inspect(object,[showHidden],[depth],[colors])是一个将任意对象转换 为字符串的方法，通常用于调试和错误输出。它至少接受一个参数 object，即要转换的对象

## Web 应用架构

大多数 web 服务器都支持服务端的脚本语言（`php、python、ruby`）等，并通过脚本语言从数据库获取数据，将结果返回给客户端浏览器。

目前最主流的三个Web服务器是`Apache、Nginx、IIS`。

![](https://i.imgur.com/WHrPcfv.jpg)

**Client** - 客户端，一般指浏览器，浏览器可以通过 HTTP 协议向服务器请求数据。

**Server** - 服务端，一般指 Web 服务器，可以接收客户端请求，并向客户端发送响应数据。

**Business** - 业务层， 通过 Web 服务器处理应用程序，如与数据库交互，逻辑运算，调用外部程序等。

**Data** - 数据层，一般由数据库组成。

## 安装 Express

安装 Express 并将其保存到依赖列表中：

    $ cnpm install express --save

以上命令会将 Express 框架安装在当前目录的 node_modules 目录中， node_modules 目录下会自动创建 express 目录。以下几个重要的模块是需要与 express 框架一起安装的：

**body-parser** - node.js 中间件，用于处理 JSON, Raw, Text 和 URL 编码的数据。

**cookie-parser** - 这就是一个解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象。

**multer** - node.js 中间件，用于处理 enctype="multipart/form-data"（设置表单的MIME编码）的表单数据。

    $ cnpm install body-parser --save
    $ cnpm install cookie-parser --save
    $ cnpm install multer --save

安装完后，我们可以查看下 express 使用的版本号：

    $ cnpm list express
    /data/www/node
    └── express@4.15.2  -> /Users/tianqixin/www/node/node_modules/.4.15.2@express

请求和响应

Express 应用使用回调函数的参数： request 和 response 对象来处理请求和响应的数据。

**Request** 对象 - request 对象表示 HTTP 请求，包含了请求查询字符串，参数，内容，HTTP 头部等属性。常见属性有：

1. req.app：当callback为外部文件时，用req.app访问express的实例
1. req.baseUrl：获取路由当前安装的URL路径
1. req.body / req.cookies：获得「请求主体」/ Cookies
1. req.fresh / req.stale：判断请求是否还「新鲜」
1. req.hostname / req.ip：获取主机名和IP地址
1. req.originalUrl：获取原始请求URL
1. req.params：获取路由的parameters
1. req.path：获取请求路径
1. req.protocol：获取协议类型
1. req.query：获取URL的查询参数串
1. req.route：获取当前匹配的路由
1. req.subdomains：获取子域名
1. req.accepts()：检查可接受的请求的文档类型
1. req.acceptsCharsets / req.acceptsEncodings / req.acceptsLanguages：返回指定字符集的第一个可接受字符编码
1. req.get()：获取指定的HTTP请求头
1. req.is()：判断请求头Content-Type的MIME类型

**Response** 对象 - response 对象表示 HTTP 响应，即在接收到请求时向客户端发送的 HTTP 响应数据。常见属性有：

1. res.app：同req.app一样
1. res.append()：追加指定HTTP头
1. res.set()在res.append()后将重置之前设置的头
1. res.cookie(name，value [，option])：设置Cookie
1. opition: domain / expires / httpOnly / maxAge / path / secure / signed
1. res.clearCookie()：清除Cookie
1. res.download()：传送指定路径的文件
1. res.get()：返回指定的HTTP头
1. res.json()：传送JSON响应
1. res.jsonp()：传送JSONP响应
1. res.location()：只设置响应的Location HTTP头，不设置状态码或者close response
1. res.redirect()：设置响应的Location HTTP头，并且设置状态码302
1. res.render(view,[locals],callback)：渲染一个view，同时向callback传递渲染后的字符串，如果在渲染过程中有错误发生next(err)将会被自动调用。callback将会被传入一个可能发生的错误以及渲染后的页面，这样就不会自动输出了。
1. res.send()：传送HTTP响应
1. res.sendFile(path [，options] [，fn])：传送指定路径的文件 -会自动根据文件extension设定Content-Type
1. res.set()：设置HTTP头，传入object可以一次设置多个头
1. res.status()：设置HTTP状态码
1. res.type()：设置Content-Type的MIME类型

## Node.js JXcore 打包

Node.js 是一个开放源代码、跨平台的、用于服务器端和网络应用的运行环境。

JXcore 是一个支持多线程的 Node.js 发行版本，基本不需要对你现有的代码做任何改动就可以直接线程安全地以多线程运行。

**下载** JXcore 安装包 `https://github.com/jxcore/jxcore-release`，你需要根据你自己的系统环境来下载安装包。

**包代码**

我们的 Node.js 项目包含以下几个文件，其中 index.js 是主文件：

接下来我们使用 jx 命令打包以上项目，并指定 index.js 为 Node.js 项目的主文件：

    $ jx package index.js index

以上命令执行成功，会生成以下两个文件：

`index.jxp` 这是一个中间件文件，包含了需要编译的完整项目信息。

`index.jx` 这是一个完整包信息的二进制文件，可运行在客户端上。

**载入 JX 文件**

Node.js 的项目运行：

    $ node index.js command_line_arguments

使用 JXcore 编译后，我们可以使用以下命令来执行生成的 jx 二进制文件：

    $ jx index.jx command_line_arguments

更多 JXcore 安装参考：[https://github.com/jxcore/jxcore/blob/master/doc/INSTALLATION.md](https://github.com/jxcore/jxcore/blob/master/doc/INSTALLATION.md)。