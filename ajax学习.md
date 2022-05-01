#### 1.jQuery 中封装的ajax请求：

$.get('url',[data],function(res){})
$.post('url',data,function(res){})
$.ajax({
method:'[get|post]',
url:'',
data:{},
success:function(res){})

#### 2.form表单的属性

form表单同步提交的缺点：
1.会跳转到action属性指定的url
2.页面之前的状态和数据会丢失
监听表单的提交事件:
$().submit(function(e){
e.preventDefault()    事件对象阻止表单默认提交行为
$(this).serialize()   可以快速获取表单的值
})
$()[0].reset()   可以将jQuery转为原生，并重置表单的值

#### 3.模板引擎

根据模板结构和数据，自动完成一个html页面

好处：减少字符串的拼接；

使代码结构更清晰；

使代码更易于阅读与维护

#### 4.art-template

1. 导入art-template
2. 定义数据
3. 定义模板
4. 调用template函数
5. 渲染html结构

标准语法：{{}}

输出：{{value}}

原文输出：{{@value}}

条件输出：{{if value}}内容{{/if}}     {{if value}} 内容1 {{else if value}} 内容2 {{/if}}

循环输出：{{each arr}}  {{$index}} {{$value}}  {{/each}}

过滤器：{{value | filterName}}

定义过滤器的基本语法：template.defaults.imports.filterName = function(value){}

#### 5.正则表达式

1.exec()函数用于检索字符串中正则表达式的匹配

RegExpObject.exec(string)

2.分组

（）包起来的内容表示一个分组，可以通过分组来提取想要的内容

var str = '<div>我是{{name}}</div>'

var pattern=/{{([a-zA-Z]+)}}/

pattern.exec(str) //得到的内容：["{{name}}","name"......]

3.字符串中的replace函数

var a="123456"

a.replace("123","abc")   //abc456

#### 6.XMLHttpRequest的基本使用

###### 1.xhr:浏览器提供的JavaScript对象，用来请求服务器上的数据资源

###### 2.使用xhr发起GET请求

​    ① 创建xhr对象：var xhr = new XMLHttpRequest

​    ② 调用 xhr.open() 函数 ： xhr.open( 'get', 'url**？id=1**' )  //查询字符串

​    ③ 调用 xhr.send() 函数：  xhr.send()

​    ④ 监听 xhr.onreadystatechange 事件 ： xhr.onreadystatechange=function(){}

​    xhr.readyState : xhr 对象的请求状态，xhr.status :与服务器响应的状态

###### 3.url编码与解码

​    使用英文字符去表示非英文字符

​    encodeURL() 编码的函数

​    decodeURL() 解码的函数

###### 4.使用xhr发起POST请求

​    ① 创建xhr对象：var xhr = new XMLHttpRequest

​    ② 调用 xhr.open() 函数 ： xhr.open( 'post', 'url' ) 

​    ③ 设置 Content-Type 属性 （固定写法）:xhr.setRequestHeader('**Content-Type**', '**application/x-              www-form-****urlencoded**')

​    ③ 调用 xhr.send() 函数：  xhr.send()，同时指定要发送的数据:xhr.send('bookname=水浒传&author=施耐庵&publisher=天津图书出版社')

​    ④ 监听 xhr.onreadystatechange 事件 ： xhr.onreadystatechange=function(){}

#### 7.数据交换格式

​    服务器端与客户端之间进行数据传输与交换的格式

######     1.xml

​    可扩展标记语言，格式臃肿，在JavaScript中解析麻烦

######     2.json

​    JavaScript 对象和数组的字符串表示，json的本质是字符串

```
{

  name: "zs",

  'age': 20,

  "gender": '男',

  "address": undefined,

  "hobby": ["吃饭", "睡觉", '打豆豆']

  say: function() {}

}
```

​    key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是数字、字符串、布尔值、null、数     组、对象6种类型。

###### 3.json与js对象的互转

​    json字符串转换为js对象：JSON.parse() ----- 反序列化

​    js对象转换为json字符串：JSON.stringify() ----- 序列化

#### 8.XMLHttpRquest Level2的新特性

​    ① 可以设置HTTP 请求的时限:

​         xhr.timeout = 3000 :timeout属性，设置HTTP请求的时限，超过，就自动停止HTTP请求

​    ② 可以使用 FormData 对象管理表单数据：

```
var fd = new FormData()
fd.append('uname','zs')

var form = document.querySelector('#form')
var fd = new FormData(form)
```

​    ③ 可以上传文件

```
获取到选择的文件列表
var files = document.queryselector('file1').files

向FormData 中追加文件
fd.append('avatar',files[0])

发起请求
xhr.send(fd)
```

​    ④ 可以获得数据传输的进度信息

```
通过监听xhr.upload.onprogress事件
xhr.upload.onprogress=function(e){
// e.lengthComputable 是一个布尔值，表示当前上传的资源是否具有可计算长度
if(e.lengthComputable){
// e.loaded 已传输的字节
// e.total 需传输的总字节
var percentComplete=Math.ceil(e.loaded/e.total*100)
}
}
```

#### 9.jQuery高级用法

###### 1.jQuery实现文件上传

```
$.ajax({
     method: 'POST',
     url: 'http://www.liulongbin.top:3006/api/upload/avatar',
     data: fd,
     // 不修改 Content-Type 属性，使用 FormData 默认的 Content-Type 值
     contentType: false,
     // 不对 FormData 中的数据进行 url 编码，而是将 FormData 数据原样发送到服务器
     processData: false,
     success: function(res) {
         console.log(res)
     }
 })

```

###### 2. ajaxStart(callback)

ajax 请求开始，执行 ajaxStart 函数

$(document).ajaxStart(function(){})

注意：$(document).ajaxStart() 函数**会监听当前文档内所有的** **Ajax** **请求**。

###### 3. ajaxStop(callback)

ajax 请求结束时，执行 ajaxStop 函数

#### 10.axios

###### 1.axios 发起 get请求的语法

axios.get('url',{params:{}}).then(callback)

###### 2.axios 发起post请求的语法

axios.post('url',{}).then(callback)

###### 3.直接使用axios发起请求

```
axios({
method:'请求类型',
url:'请求的URL地址',
data:{post数据},
params:{get参数}
}).then(callback)
```

#### 11.同源策略和跨域

###### 1.同源策略

同源：如果两个页面的协议，域名和端口都相同，则两个页面具有**相同的源**

同源策略：是浏览器提供的一个安全功能。同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。

###### 2.跨域

**同源**指的是两个 URL 的协议、域名、端口一致，反之，则是**跨域**。

出现跨域的根本原因：**浏览器的同源策略**不允许非同源的 URL 之间进行资源的交互。

实现啊跨域数据请求：JSONP 和 CORS

###### 3.JSONP

由于浏览器同源策略的限制，网页中无法通过 Ajax 请求非同源的接口数据。但是 <script> 标签不受浏览器同源策略的影响，可以通过 src 属性，请求非同源的 js 脚本。

因此，JSONP 的实现原理，就是通过 <script> 标签的 src 属性，请求跨域的数据接口，并通过**函数调用**的形式，接收跨域接口响应回来的数据。

由于 JSONP 是通过 <script> 标签的 src 属性，来实现跨域数据获取的，所以，JSONP 只支持 GET 数据请求，不支持 POST 请求。



注意：**JSONP** **和** **Ajax** **之间没有任何关系**，不能把 JSONP 请求数据的方式叫做 Ajax，因为 JSONP 没有用到 XMLHttpRequest 这个对象。

```
	jQuery 提供的 $.ajax() 函数，除了可以发起真正的 Ajax 数据请求之外，还能够发起 JSONP 数据请求，例如：
	$.ajax({
    url: 'http://ajax.frontend.itheima.net:3006/api/jsonp?name=zs&age=20',
    // 如果要使用 $.ajax() 发起 JSONP 请求，必须指定 datatype 为 jsonp
    dataType: 'jsonp',
    success: function(res) {
       console.log(res)
    }
 })

```

#### 12.防抖和节流**

##### 1.防抖

防抖策略是当事件被触发后，延迟 n秒后再执行回调，如果在n秒内事件又被触发，则重新计时

应用场景：用户在输入框中连续输入一串字符时，可以通过防抖策略，只在输入完后，才执行查询的请求，这样可以有效减少请求次数，节约请求资源；

```
实现输入框的防抖：
 var timer = null                    // 1. 防抖动的 timer

 function debounceSearch(keywords) { // 2. 定义防抖的函数
    timer = setTimeout(function() {
    // 发起 JSONP 请求
    getSuggestList(keywords)
    }, 500)
 }

 $('#ipt').on('keyup', function() {  // 3. 在触发 keyup 事件时，立即清空 timer
    clearTimeout(timer)
    // ...省略其他代码
    debounceSearch(keywords)
 })

```

##### 2.节流

节流策略，可以减少一段时间内事件的触发频率

应用场景：①鼠标连续不断地触发某事件（如点击），只在单位时间内只触发一次；

②懒加载时要监听计算滚动条的位置，但不必每次滑动都触发，可以降低计算的频率，而不必去浪费 CPU 资源；

```
$(function() {
  var angel = $('#angel')
  var timer = null // 1.预定义一个 timer 节流阀
  $(document).on('mousemove', function(e) {
    if (timer) { return } // 3.判断节流阀是否为空，如果不为空，则证明距离上次执行间隔不足16毫秒
    timer = setTimeout(function() {
      $(angel).css('left', e.pageX + 'px').css('top', e.pageY + 'px')
      timer = null // 2.当设置了鼠标跟随效果后，清空 timer 节流阀，方便下次开启延时器
    }, 16)
  })
})
```

##### 3.防抖和节流的区别

防抖：如果事件被频繁触发，防抖能保证只有最后一次触发生效，前面n多次的触发都会被忽略

节流：如果事件被频繁触发，节流能够减少事件触发的频率。

#### 13.HTTP协议

**1.HTTP** **协议**

即超文本传送协议 (HyperText Transfer Protocol) ，它规定了客户端与服务器之间进行网页内容传输时，所必须遵守的传输格式。

2.HTTP请求消息：

由于 HTTP 协议属于客户端浏览器和服务器之间的通信协议。因此，客户端发起的请求叫做 **HTTP** **请求**，客户端发送到服务器的消息，叫做 **HTTP** **请求消息**。

HTTP 请求消息由请求行（request line）、请求头部（ header ） 、空行 和 请求体 4 个部分组成。

![image-20220501171121673](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220501171121673.png)

**请求头部**用来描述客户端的基本信息，从而把客户端相关的信息告知服务器。比如：User-Agent 用来说明当前是什么类型的浏览器；Content-Type 用来描述发送到服务器的数据格式；Accept 用来描述客户端能够接收什么类型的返回内容；Accept-Language 用来描述客户端期望接收哪种人类语言的文本内容。

请求体中存放的，是要通过 POST 方式提交到服务器的数据。

**注意**：只有 POST 请求才有请求体，GET 请求没有请求体！

3.http响应消息

响应消息就是服务器响应给客户端的消息内容，也叫作响应报文。

HTTP响应消息由状态行、响应头部、空行 和 响应体 4 个部分组成，如下图所示：

![image-20220501171411094](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220501171411094.png)

4.http请求方法

HTTP 请求方法，属于 HTTP 协议中的一部分，请求方法的作用是：用来表明要对服务器上的资源执行的操作。最常用的请求方法是 GET 和 POST。

| **序号** | **方法** | **描述**                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| 1        | GET      | (查询)发送请求来获得服务器上的资源，请求体中不会包含请求数据，请求数据放在协议头中。 |
| 2        | POST     | (新增)向服务器提交资源（例如提交表单或上传文件）。数据被包含在请求体中提交给服务器。 |
| 3        | PUT      | (修改)向服务器提交资源，并使用提交的新资源，替换掉服务器对应的旧资源。 |
| 4        | DELETE   | (删除)请求服务器删除指定的资源。                             |
| 5        | HEAD     | HEAD 方法请求一个与 GET 请求的响应相同的响应，但没有响应体。 |
| 6        | OPTIONS  | 获取http服务器支持的http请求方法，允许客户端查看服务器的性能，比如ajax跨域时的预检等。 |
| 7        | CONNECT  | 建立一个到由目标资源标识的服务器的隧道。                     |
| 8        | TRACE    | 沿着到目标资源的路径执行一个消息环回测试，主要用于测试或诊断。 |
| 9        | PATCH    | 是对 PUT 方法的补充，用来对已知资源进行局部更新  。          |

5.HTTP响应状态码

**HTTP** **响应状态码**（HTTP Status Code），也属于 HTTP 协议的一部分，用来标识响应的状态。

响应状态码会随着响应消息一起被发送至客户端浏览器，浏览器根据服务器返回的响应状态码，就能知道这次 HTTP 请求的结果是成功还是失败了。

| 1**  | 信息，服务器收到请求，需要请求者继续执行操作（实际开发中很少遇到 1** 类型的状态码） |
| ---- | ------------------------------------------------------------ |
| 2**  | 成功，操作被成功接收并处理                                   |
| 3**  | 重定向，需要进一步的操作以完成请求                           |
| 4**  | 客户端错误，请求包含语法错误或无法完成请求                   |
| 5**  | 服务器错误，服务器在处理请求的过程中发生了错误               |

完整的 HTTP 响应状态码，可以参考 MDN 官方文档 https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status