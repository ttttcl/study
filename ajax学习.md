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