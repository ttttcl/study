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

# 10.使用Express写接口

1.1创建基本的服务器

```
const express=require('express')
const app=express()

app.listen(80,()=>{
console.log('http://127.0.0.1')
})
```

1.2创建API路由模块

```
const express=require('express')
const apiRouter=express.Router()

module.exports=apiRouter
------------------------------------------
const apiRouter=require('./apiRouter.js')
app.use('/api',apiRouter)
```

1.3编写GET接口

```
apiRouter.get('/get',(req,res)=>{
const query=req.query
res.send({
status:0,
msg:'GET请求成功',
data:query
})
})
```

1.4编写POST接口

```
apiRouter.post('/post',(req,res)=>{
const body=req.body
res.send({
status:0,
msg:'POST请求成功',
data:body
})
})
```

注意：如果要获取 URL-encoded格式的请求体数据，必须配置中间件 app.use(express.urlencoded({extend:false}))

2.CORS跨域资源共享

2.1接口的跨域问题

解决接口跨域问题的方案：

①CORS

②JSONP

2.2使用CORS中间件解决跨域问题

cors是Express的一个第三方中间件。

使用步骤：

①运行 npm install cors 安装中间件

②使用 const cors=express('cors') 导入中间件

在路由之前调用 app.use(cors()) 配置中间件

2.3什么是cors

cors由一系列HTTP响应头组成，这些HTTP响应头决定浏览器是否阻止前端JS代码跨域获取资源

浏览器的同源安全策略默认会阻止网页跨域获取资源。但如果接口服务器配置了cors 相关的http响应头，就可以接触浏览器端的跨域访问限制

2.4cors的注意事项

①cors 主要在服务器端进行配置。客户端浏览器无须做任何的额外配置，即可请求开启了 cors 的接口

②cors 在浏览器中有兼容性。只有支持XMLHttpRequest Level2 的浏览器，才能正常访问开启了cors 的服务器端接口。

2.5cors 响应头部

响应头部中可以携带一个 Access-Control-Allow-Origin 字段，其语法如下：

Access-Control-Allow-Origin：<origin>|*

其中，origin 参数的值指定了允许访问该资源的外域 URL

例如：

![image-20220506211347327](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220506211347327.png)

如果值为通配符*，表示允许来自任何域的请求

2.6**CORS** **响应头部** **- Access-Control-Allow-****Headers**

默认情况下，CORS **仅**支持客户端向服务器发送如下的 9 个请求头：

Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

![image-20220506211502418](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220506211502418.png)

2.7**CORS** **响应头部** **- Access-Control-Allow-****Methods**

默认情况下，cors仅支持客户端发起 GET、POST、HEAD 请求。

如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来指明实际请求所允许使用的 HTTP 方法。

![image-20220506211644444](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220506211644444.png)

2.8简单请求

满足一下两大条件的请求，就属于简单请求：

①请求方式：GET、POST、HEAD三者之一

②HTTP 头部信息不超过一下几个字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain）

2.9预检请求

只要满足以下任何一个条件的请求，都要进行预检请求：

①请求方式为GET、POST、HEAD之外的请求 Method 类型

②请求头中包含自定义头部字段

③向服务器发送了 application/json 格式的数据

在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。

2.10简单请求和预检请求的区别

简单请求的特点：客户端与服务器之间只会发生一次请求。

预检请求的特点：客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求

3.1JSONP接口

1.概念与特点

概念：浏览器通过<script>标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做JSONP

特点：

①JSONP不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象

②JSONP 仅支持 GET请求，不支持 POST、PUT、DELETE 等请求。

2.创建 JSONP 接口的注意事项

如果项目中已经配置了 cors 跨域资源共享，为了防止冲突，必须在配置 cors 中间件之前声明 JSONP 的接口。否则JSONP接口会被处理成开启了 cors 的接口

3。事项JSONP接口的步骤

①获取客户端发送过来的回调函数的名字

②得到要通过 JSONP 形式发送给客户的数据

③根据前两步得到的数据，拼接出一个函数调用的字符串

④把上一步拼接得到的字符串，响应给客户端的 <script> 标签进行解析执行

![image-20220506213340323](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220506213340323.png)

# 11.数据库的基本概念

1.1什么是数据库

数据库是用来组织、存储和管理数据的仓库

1.2常见的数据库及分类

市面上的数据库有很多种，最常见的数据库有如下几个：

l MySQL 数据库（目前使用最广泛、流行度最高的开源免费数据库；Community + Enterprise）

l Oracle 数据库（收费）

l SQL Server 数据库（收费）

l Mongodb 数据库（Community + Enterprise）

l

其中，MySQL、Oracle、SQL Server 属于**传统型数据库**（又叫做：关系型数据库 或 SQL 数据库），这三者的设计理念相同，用法比较类似。

而 Mongodb 属于**新型数据库**（又叫做：非关系型数据库 或 NoSQL 数据库），它在一定程度上弥补了传统型数据库的缺陷。

2.1sql 的select 语句

用于从表中查询数据。执行的结果被存储在一个结果集中。

SELECT * FROM 表名称

SELECT 列名称 FROM 表名称

2.2sql 的 insert into 语句

用于向数据表中插入新的数据行

INSERT INTO table_name （列1，列2...) VALUES (值1，值2...)

2.3sql 的 UPDATE 语句

用于修改表中的数据

UPDATE 表名称 SET 列名称=新值 WHERE 列名称=某值

2.4sql 的 DELETE 语句

用于删除表中的行

DELETE FROM 表名称 WHERE 列名称=值

3.1sql 的 WHERE 子句

用于限定选择的标准。在 SELECT、UPDATE、DELETE语句中，都可以使用 WHERE子句来限定选择的标准

3.2sql 的 AND 和 OR 运算符

用于WHERE 子语句中把两个或多个条件结合起来

AND 表示必须同时满足多个条件

OR 表示满足任意一个条件即可

3.3sql 的 ORDER BY 子句

用于根据指定的列对结果集进行排序

默认按照升序

降序使用 DESC

3.4sql 的COUNT(*) 函数

用于返回查询结果的总数据条数

SELECT COUNT(*) FROM 表名称

可以使用 AS 给查询出来的列名称设置别名

SELECT COUNT(*) AS 别名 FROM 表名称