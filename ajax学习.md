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