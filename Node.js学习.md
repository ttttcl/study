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