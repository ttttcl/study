#### 1.初始node.js

node.js是一个基于 Chrome V8 引擎的 Javascript 运行环境

浏览器是 JavaScript 的前端运行环境

Node.js 是 JavaScript 的后端运行环境

Node.js 中无法调用 DOM 和 BOM 等浏览器内置 API

#### 2.fs文件系统模块

fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。例如：

fs.readFile() 方法，用来读取指定文件中的内容

fs.writeFile() 方法，用来向指定的文件中写入内容

注意：要在JavaScript 代码中，使用fs 模块来操作文件，则需要先导入它：

const fs = require('fs')

###### 1.读取指定文件中的内容

语法格式：

```
fs.readFile(path[,options],callback)
参数1：path 必选参数，字符串，表示文件的路径
参数2：options 可选参数，表示以什么编码格式来读取文件。一般为‘utf8’
参数3：callback 必选参数，文件读取完成后，通过回调函数拿到读取的结果

fs.readFile('./1.txt','utf8',function(err,result){})
文件读取失败 err为一个对象
文件读取成功 err为null
```

###### 2.向指定的文件中写入内容

语法格式：

```
fs.writeFile(file,data[,options],callback)
参数1：file 必选参数，需要指定一个文件路径的字符串，表示文件的存放路径
参数2：data 必选参数，表示要写入的内容
参数3：options 可选参数，表示以什么格式写入文件内容，默认值是 utf8
参数4：callback 必选参数，文件写入完成后的回调函数
```

###### 3.路径动态拼接的问题

如果提供的操作路径是相对路径，容易出现动态拼接错误的问题。

#### 3.path 路径模块

path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串

path.basename() 方法，用来从路径字符串中，将文件名解析出来

注意：在JavaScript 代码中，使用 path 模块来处理路径，则需要先导入它：

const path = require('path')

###### 1.path.join() 的语法格式

语法格式：

```
path.join([...paths])
...path<string> 路径片段的序列
返回值：<string>
```

###### 2.path.basename() 的语法格式

语法格式：

```
path.basename(path[,ext])
path<string> 必选参数，表示一个路径的字符串
ext <string> 可选参数，表示文件的扩展名
返回值: <string> 表示路径中的最后一部分
注意：加上ext参数只会返回文件名
```

###### 3.path.extname() 的语法格式

语法格式：

```
path.extname(path)
path <string> 必选参数，表示一个路径的字符串
返回值： <string> 返回得到的扩展名字符串
```

fs.writeFile() 方法只能用来创建文件，不能用来创建路径

重复调用 fs.writeFile() 写入同一个文件，新写入的内容会覆盖之前的旧内容

#### 4.http模块

http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块

注意：使用 http 模块创建 Web 服务器，则需要先导入它:

const http = require('http')

###### 1.创建 web 服务器的基本步骤

① 导入 http 模块

```
const http = require('http')
```

② 创建 web 服务器实例

```
const server = http.createServer()
```

③ 为服务器实例绑定 request 事件，监听客户端的需求

```
server.on('request',(req,res)=>{
//只要有客户端来请求，就会触发request 事件，从而调用这个事件处理函数

//req 是请求对象，它包含了与客户端相关的数据和属性，例如：
//req.url 是客户端请求的 URL 地址
//req.method 是客户端的 method 请求类型

//res 是响应对象，它包含了与服务器相关的数据和属性，例如：
const str='123'
//为了防止中文乱码的问题，需要设置请求头 Content-Type 的值为 text/html;charset=utf-8
res.setHeader('Content-Type','text/html;charset=utf-9')
//res.end() 方法的作用：
//向客户端发送指定的内容，并结束这次请求的处理过程
res.end(str)
})
```

④ 启动服务器

```
server.listen(80,()=>{

})
```

#### 5.模块化的基本概念

**模块化**是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

#### 6.Node.js 中的模块化

Node.js 中根据模块来源的不同，分为 3 大类，分别是：

- 内置模块（内置模块是由 Node.js 官方提供的，例如：fs、path、http等）
- 自定义模块（用户创建的每个 .js 文件，都是自定义模块）
- 第三方模块（由第三方开发出来的模块，不是官方提供的，也不是用户创建的，使用前需下载）

1.加载模块

使用 require() 方法

注意：使用 require() 方法加载其它模块时，会执行被加载模块中的代码

2.模块作用域

和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问权限，叫做模块作用域。

好处：防止了全局变量污染的问题

3.向外共享模块作用域中的成员

①module 对象

在每个 .js 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息。

②module.exports 对象

在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。

外界用 require() 方法导入自定义模块时，得到的就是 module.exports 所指向的对象

③共享成员时的注意点

使用 require() 方法导入模块时，导入的结果，永远以 module.exports 指向的对象为准

④exports 对象

默认情况下，exports 和 module.exports 指向同一个对象。

误区：require() 模块时，得到的永远是 module.exports 指向的对象

注意:为了防止混乱，不要在同一个模块中同时使用 exports 和 module.exports

4.Node.js 中的模块化规范

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖

CommonJs 规定：

①每个模块内部，module 变量代表当前模块。

②module 变量是一个对象，它的 exports 属性是对外的接口。

③加载某个模块，其实是加载该模块的 module.exports 属性。