mongodb:
mongoose:
var mongoose = require('mongoose');

// 连接mongodb
mongoose.connect('mongodb://localhost:27017/test')

// 定义模型
var Shop = mongoose.model('Shop',{title:String})

// 增删改查
Shop.create({title:"商品"},function(err,data){})
Shop.remove({title:""},function(err,data){})
Shop.update({title:"mate 7"},{title:"mate 7s"},function(err,data){})
Shop.find({title:"mate 7"},function(err,data){})	// data=>[{},{},{}]
Shop.findOne({_id:""},function(err,data){})	// data=>{}
Shop.count(function(err,data){})

设置淘宝镜像：npm config set registry=https://registry.npm.taobao.org
设置官方镜像：npm config set registry=https://registry.npmjs.org

3.修改package.json文件，
	1.用下面的代码替换package.json中对应的内容
	"scripts": {
        "start": "supervisor ./bin/www"
    },
    "dependencies": {
        "body-parser": "~1.15.2",
        "cookie-parser": "~1.4.3",
        "debug": "~2.2.0",
        "express": "~4.14.0",
        "morgan": "~1.7.0",
        "serve-favicon": "~2.3.0",
        "mongoose": "*",
        "connect-flash": "^0.1.1",
        "connect-mongo": "^1.3.2",
        "express-session": "^1.14.2",
        "ejs": "^2.5.2",
        "multer": "^1.2.0"
    }

    2.执行 npm install(结果中不含有error等关键字，表示下载模块成功)

4.
	修改app.js中的代码（14,15行）
	4.1 app.set('views', path.join(__dirname, 'views'));
		// 将模版的后缀名改为html
		app.engine('.html', require('ejs').__express);
		app.set('view engine', 'html');

	4.2 修改views目录下的文件后缀名为html
	4.3 修改error.html内容
		<!DOCTYPE html>
		<html lang="en">

		<head>
		    <meta charset="UTF-8">
		    <title>错误页面</title>
		</head>

		<body>
		    <h3><%= message %></h3>
		    <h2><%= error.status %></h2>
		    <pre>
			<%= error.stack %>
			</pre>
		</body>

		</html>

1.Router

2.request请求对象
	=============================
	浏览器直接请求/ajax请求
	// post请求
	req.body：接收post请求传递的参数

	// get请求
	req.params:获取"localhost/zhangsan/20/男" 的参数
	req.query:获取"localhost?username=zhangsan&age=20"的参数
	====================================

	// cookie只要被存储，每次的访问该网站都会被通过互联网传递到服务器
	req.cookies:获取当前网站的cookie数据
	req.ip:获取用户的IP地址

3.response响应对象
	=====================
	res.render(模板页面,{username:"zhangsan"})：响应一个模板页面,并通过第二个参数给模板页面赋值

	res.end([data])：结束响应

	// 重定向
	res.redirect()
		res.redirect('back')
		res.redirect('/users')
		res.redirect('http://www.baidu.com')

	res.json()：给客户端响应一个json数据
