﻿http://www.conans.top/abc/logo.png?p=1#dasd
发送的GET请求是

GET /abc/logo.png?p=1 HTTP/1.1
host:www.conans.top//一台服务器可能对应很多网站
User-Agent:可以是任何字
i-made-this://可以自己造头部

HTTP Response

HTTP/1.1 200 OK
Date Tue mar 2012 04:33:33 GMT
Server:Apache/2.2.3
Content-Type:text/html
Content-Length:1579


<form action="http://www.google.com/search">
<input name="q">
<input type="submit">
</form>

只有函数语句中的花括号才能创建作用域lexical scope(词法作用域)

内联元素想要居中对齐有hack方法哟
position:absolute;
left:50%;
margin-left:-自身宽度的一般(注意是自身宽度一半的负值哦)

我的天啊,今天在找程序的bug过程中,发现一个变量申明忘了用var,结果老是提示变量未定义,害我找了40分钟的bug,改着改那的,简直教训!!!!!!!!!!!!


面向对象的JavaScript编程
this指向调用该函数的对象
如果调用这个函数的时候没有指明对象,则默认this绑定在全局对象上
fn.call(obj,v1,v2)//obj为要绑定的对象,目的就是使得即使没有绑定obj对象的函数的this指代obj.
.call重写方法,指向制定的对象.
回调函数的参数控制问题
JSX语法糖最开始的标签与最后的标签应该同一个标签,最外层要有一个大包.
ReactDOM.render(
JSX expression,
where to render)

class是JavaScript的关键字,JSX中用className来代替class,语法糖被渲染之后className变为class

JSX中自闭合标签要有结束标签

JSX标签之间不具有JavaScript表达式性质,但是加了花括号之后就有表达式性质了

JSX中事件监听驼峰写法小写on开头

JSX中间,不允许有if语句,但是语句可以包含JSX哦

JSX中可以用三元操作符

{myvar$$<li>sadsda</li>},与操作符,花括号内,要么显示<li>内容,要么不现实

var React = require('react');
var ReactDOM = require('react-dom')
React.createClass();//创建React组件

组件名称首字母大写+驼峰写法哦

当前组件输出变量
//greetings.js
module.exports = Greeting;
require('./greeting.js')//引入方法和nodejs一样哦

被引用js申明了module.exports = func//只输出被引用js文件的func方法

内联样式的双花括号,第一层表示JSX语法,第二层表示这是一个JavaScript对象.

React.js中样式属性用驼峰标记法














nodejs中进程由process表示

fs模块是nodejs内置文件读写系统.
同时有同步与异步方法.

读取文件: 

1.异步读取文件
fs = require('fs'); fs.readFile('123.txt','utf-8',function(err,data){
	if(err){         
	//处理错误     
	}     
	else{         
	//处理数据     
} })

2.同步读取文件
data=fs.readFileSync('123.txt','utf-8');
直接返回的就是读取到的数据

当读取二进制文件时,不传入文件编码,回调函数返回的将是一个Buffer对象,在nodejs中Buffer对象就是类数组.
Buffer与string可以互相转换

data.toString('utf-8');

new Buffer(string,'utf-8');

写入文件:
1.异步写入文件
fs = require('fs');
fs.writeFile('1234.txt',data,function(err){
	if(err){
	//处理错误
}else{
	//处理成功
}
})
传入data为字符串,默认按照utf-8编码写入,如果出路参数是Buffer,则写入的是二进制文件.
2.同步写入文件
fs.writeFileSync('1235.txt',data)

获取文件信息:
fs.stat(),返回一个stat对象,告诉我们文件或目录的详细信息

var fs = require('fs');

fs.stat('123.txt',function(err,stat){
	if(err){
	//处理错误
}else{
	stat.isFile();//是否是文件
	stat.isDirectory();//是否是目录
	stat.birthtime();//创建时间
	stat.mtime();//修改时间
}
})
2.同步方法
var stat = fs.stat('123.txt')
stat.isFile();
stat.isDirectory();
...

Stream,nodejs中的流,用来描述数据与输出的一个对象.
data事件表示数据可以读取了,end事件表示数据到末尾了,error事件表示出错了.
从一个文件流读取文本内容:
var fs = require('fs');
var rs = fs.createReadStream('666.txt','utf-8');
rs.on('data',function(chunk){
	console.log(chunk);
});
rs.on('end',function(){
	console.log('End');
});
rs.on('error',function(err){
	console.log('err: '+err);
});
数据流写入文件
var fs = require('fs');
var wfs = fs.createWriteStream('ouput.txt','utf-8');
wfs.write(string1);
wfs.write(string2);
wfs.end();
不要utf-8也可以直接写入Buffer数据

所有可以读取数据的流都继承自stream.Readable
所有可以写入的流都继承自stream.Writable

pipe,将读取流与写入流串联起来

var fs = require('fs');
var rs = fs.createReadStream('../node.txt');
var ws = fs.createWriteStream('123.txt');

rs.pipe(ws)
这相当于读取node.txt的文件,然后写入到123.txt文件中

HTTP
// 创建http server ,并传入回调函数
var http = require('http');
var server = http.createServer(function(request,response){
	// 回调函数接受request和response对象
	// 获取http请求的method和url
	console.log(request.method+":"+request.url)
	response.writeHead(200,{'Content-Type':'text/html'});
	response.end('<h1>Hello conan</h1>')
})
server.listen(8080);
console.log('server now is running at localhost:8080');

文件服务器:

var url = require('url');

url.parse();//将一个url解析为url对象
处理本地文件目录用node.js的path模块
var path = require('path');
var nowdir = path.resolve('.');//解析当前目录

实现一个文件服务器
'use strict';

var fs = require('fs'),
    url = require('url'),
    path = require('path'),
    http = require('http');
var root = path.resolve(process.argv[2]||'.');
console.log('Static root dir: '+root);
var server = http.createServer(function(request,response){
	var pathname = url.parse(request.url).pathname;
	var filepath = path.join(root,pathname);
	fs.stat(filepath,function(err,stats){
		if(!err&&stats.isFile()){
			console.log('200'+request.url);
			response.writeHead(200);
			fs.createReadStream(filepath).pipe(response);
		}
		else if(!err&&stats.isDirectory()){
			var filepath1 =filepath+'\index.html';
			fs.stat(filepath1,function(err,stats){
				if(!err){
					response.writeHead(200);
					fs.createReadStream(filepath1).pipe(response);
				}else{
                    console.log('not index');
                    var filepath2 = filepath+'\default.html';
                    console.log(filepath2);
					fs.stat(filepath2,function(err,stats){
						if(!err){
							response.writeHead(200);
							fs.createReadStream(filepath2).pipe(response);
						};
					});
				};
			});
		}else{
			console.log('404'+request.url);
			response.writeHead(400);
			response.end('404 Not Found');
		}
	});
});
server.listen(8080);
console.log('server now is running at http://127.0.0.1:8080');

crypto模块提供通用的加密和哈希算法
MD5
MD5是一种常用的哈希算法,用于给任意数据一个签名,这个签名一般用一个十六进制字符串表示

const crypto = require('crypto');

const hash = crypto.createHash('md5');

hash.update('hello');
console.log(hash.digest('hex'));
update()方法默认字符串编码为utf-8

Hmac算法也是一种哈希算法,它还需要一个密钥

const crypto = require('crypto');

const hmac = crypto.createHmac('sha256','s-key');

hmac.update('hello');
密钥发生变化,输入数据也会得到不同的签名

npm ls -g --depth 0//查看一层全局安装模块

闭包和时间监听程序
arr=[1,2,3]
for(var a=0;a<arr.length;a++){
 a.addEventListener('click',function(){
 alert(a)//这样每次alert的都是3
})
}
换一种写法,闭包保存状态IIFE(immediately-invoked Function Expression)
arr=[1,2,3]
for(var a=0;a<arr.length;a++){
 a.addEventListener('click',(function(acopy){
 return function(){
alert(a)//依次alert 1 2 3 

}

})(a))
}

*******
浏览器计算的像素值(DIP--device independent pixels)与
硬件像素(我们所说的1920*1080分辨率之流)计算值不同
不是所谓的像素值

视口(viewport)和分辨率的关系
DPR(device pixels rate)硬件像素与视口像素(CSS像素)之比

视口宽度等于硬件像素除以DPR
1.设置meta标签
<meta name="viewport" content="width=device-width,initial-scale=1" />
2.宽度用百分比
img,embed,object,video{
    max-width:100%;
}
3.按钮,或者其他要点击的地方,至少48px*48px的CSS像素,至少间隔40px像素以便按下
button{
    min-width:48px;
    min-height:48px;
}
4.media query 
media query 应用的三种方式:
1).
<link rel="stylesheet" media="screen and (min-width:500px)" href="css/over500.css" />
2).
@media screen and (min-width:500px) and (max-width:600px){
    //CSS styles
}
3).//考虑性能因素,很少使用这种方法
@import url('over400.css') only screen and (min-width:400px);

要权衡的是1)与2)
1)有很多小文件,http请求
2)文件会大些

display:flex
flex-wrap:wrap

每一行45~90个字符比较合理(English)
网页中一般是65个
字体最少16px，1.2em

命令行学习小结
在短短的一课里我们学习了不少的内容！我们来复习一下本课学习到的命令：

ls : 列出目录内容
cd : 前往其他目录
pwd : 显示当前目录（也就是工作目录）
open : 打开一个文件（在 Mac 电脑上）
touch : 创建一个原本不存在的新文件或者更新该文件的时间标记
mkdir : 创建一个新目录
rm : 删除一个文件
rmdir : 删除一个空目录
rm -rf : 删除一个目录及其内容（无确认过程，请谨慎使用！）

You are never wrong,you are just not right yet.




