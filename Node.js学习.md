# 1.初始node.js

node.js是一个基于 Chrome V8 引擎的 Javascript 运行环境

浏览器是 JavaScript 的前端运行环境

Node.js 是 JavaScript 的后端运行环境

Node.js 中无法调用 DOM 和 BOM 等浏览器内置 API

# 2.fs文件系统模块

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

# 3.path 路径模块

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

# 4.http模块

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

# 5.模块化的基本概念

**模块化**是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

# 6.Node.js 中的模块化

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

# 7.npm与包

Node.js 中的第三方模块又叫做包

在项目中安装包的命令：npm install 包的完整名称 ----简写：npm i 完整的包名称

安装指定版本的包：npm i moment@2.22.2

快速创建 package.json: npm init -y

一次性安装所有的包： npm i

卸载包：npm uninstall 具体的包名

查看当前的下包镜像源：npm config get registry

切换为淘宝镜像源：npm config set registry=http://registry.npm.taobao.org/

安装nrm: npm i nrm -g

查看所有可用的镜像源：nrm ls

切换为淘宝镜像源：nrm use taobao

# 8.模块的加载机制

模块在第一次加载后会被缓存。多次调用 require() 不会导致模块的代码被执行多次

注意：优先从缓存中加载，从而提高模块的加载速度

1.模块的加载机制

内置模块的加载优先级最高

2.自定义模块的加载机制

使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。在加载自定义模块时，没指定这样的标识符，则 node 会把它当作内置模块或第三方模块进行加载。

同时，如果省略了文件的扩展名，会按顺序分别尝试加载以下的文件：

①按照确切的文件名进行加载

②补全 .js 扩展名进行加载

③补全 .json 扩展名进行加载

④补全 .node 扩展名进行加载

⑤加载失败，终端报错

3.第三方模块的加载机制

从当前模块的父目录开始，尝试从 /node_module 文件夹中加载第三方模块

如果没有找到对应的第三方模块，则移动到再上一级父目录中，进行加载，直到文件系统的根目录

4.目录作为模块

①在被加载的目录下查找 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口

②如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则Node.js 会尝试加载目录下的 index.js 文件

③如果上两步都失败，则终端报错

# 9.Express

1.安装

npm i express@4.17.1

2.创建基本的 web 服务器

![image-20220505220052036](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505220052036.png)

3.监听GET请求

![image-20220505220127101](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505220127101.png)

4.监听POST请求

![image-20220505220149366](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505220149366.png)

5.把内容响应给客户端

![image-20220505220207940](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505220207940.png)

6.获取URL中携带的查询参数

![image-20220505220242037](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505220242037.png)

7.获取URL中的动态参数

![image-20220505220310004](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505220310004.png)

8.托管静态资源

express.static()

例：app.use(express.static('public'))

# 8.Express 路由

1.路由的概念

路由指的是客户端的请求与服务器处理函数之间的映射关系

由 3 部分组成，分别是请求的类型，请求的 url 地址，处理函数，格式如下

![image-20220505221652200](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505221652200.png)

2.模块化路由

①创建路由模块对应的 .js 文件

②调用 express.Router() 函数创建路由对象

③向路由对象上挂载具体的路由

④使用 module.exports 向外共享路由对象

⑤使用app.use() 函数注册路由模块

![image-20220505222012636](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505222012636.png)

![image-20220505222022434](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505222022434.png)

# 9.Express中间件

1.1中间件的概念

特指业务流程的中间处理环节

1.2调用流程

当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理

1.3格式

本质上就是一个 function 处理函数

1.4next函数的作用

next函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由

2.1定义中间件函数

![image-20220505222456795](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505222456795.png)

2.2全局生效的中间件

客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。

通过调用 app.use(中间件函数) , 即可定义一个全局生效的中间件

![image-20220505222656274](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505222656274.png)

2.3中间件的作用

多个中间件之间，共享一份 req 和 res 

2.4定义多个全局中间件

使用 app.use() 连续定义多个全局中间件。客户端请求到达服务器后，会按照中间件定义的先后顺序依次进行调用。

![image-20220505222900413](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505222900413.png)

2.5局部生效的中间件

不使用 app.use() 定义的中间件，叫做局部生效的中间件。

![image-20220505223109988](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505223109988.png)

2.5定义多个局部中间件

可以在路由中，通过如下两种等价的方式，使用多个局部生效的中间件

![image-20220505223233443](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505223233443.png)

2.6注意事项

①一定要在路由之前注册中间件

②客户端发送过来的请求，可以连续调用多个中间件进行处理

③执行完中间件的业务代码后，不要忘记调用next() 函数

④为了防止代码逻辑混乱，调用next() 函数后不要再写额外的代码

⑤连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象

3.1中间件的分类

①应用级别的中间件

②路由级别的中间件

③错误级别的中间件

④Express 内置的中间件

⑤第三方的中间件

3.2应用级别的中间件

通过 app.use() 或 app.get() app.post() ,绑定到 app  实例上的中间件，叫做应用级别的中间件

![image-20220505223728303](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505223728303.png)

3.3路由级别的中间件

绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件

![image-20220505223845066](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505223845066.png)

3.4错误级别的中间件

作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题

![image-20220505223946921](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220505223946921.png)

注意：错误级别的中间件，必须注册在所有路由的后面

3.5Express内置的中间件

内置了3个中间件

①express.static 快速托管静态资源的内置中间件

②express.json 解析JSON 格式的请求体数据

③express.urlencoded 解析URL-encoded 格式的请求体数据

3.6第三方的中间件

①运行 npm install 名称

②使用require 导入中间件

③调用 app.use() 注册并使用中间件