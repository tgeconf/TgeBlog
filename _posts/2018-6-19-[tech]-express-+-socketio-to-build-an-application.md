<p>我们在使用express应用生成器结合Socketio搭建应用的过程中，有一个常见的问题就是如何将Socket.io的配置代码从express自动生成的项目中分离。</p>

<h3>express-generator生成express项目</h3>
<p>通过如下命令安装express</p>
<pre>
	$ npm install express-generator -g
</pre>
<p>之后生成一个名为msgTrans的应用，注意这里我用了-e选项表示将默认的静态模板格式jade更改为ejs，可以使用-h查看更多可用的命令选项.</p>
<pre>
	$ express msgTrans -e
</pre>
<p>安装依赖包</p>
<pre>
	$ cd msgTrans
	$ npm install
</pre>
<p>启动app</p>
<pre>
	> set DEBUG=msgTrans
	> npm start
</pre>
<p>之后在浏览器中访问http://localhost:3000/就可以看到这个应用了。</p>
<pre>
	|-bin
	|   --www
	|-public
	|   --images
	|   --javascripts
	|   --stylesheets
	|         --style.css
	|-route
	|   --index.js
	|   --users.js
	|-views
	|   --error.ejs
	|   --index.ejs
	|-app.js
	|-package.json
</pre>

<h3>加入Socket.io</h3>
<p>1. 在根目录下创建socketio.js，并将socketio相关的配置写入</p>
<pre>
	// socketio.js
	var socketio = {};
	var socket_io = require('socket.io');

	//get io
	socketio.getSocketio = function(server){
	  var io = socket_io.listen(server);
	};

	module.exports = socketio;
</pre>
<p>2. 修改bin/www，启动服务器</p>
<pre>
	// bin/www
	/**
	 * Module dependencies.
	 */

	var app = require('../app');
	var debug = require('debug')('msgtrans:server');
	var http = require('http');
	var io = require('../socketio');// import socketio
	// ...

	/**
	 * Create HTTP server.
	 */

	var server = http.createServer(app);

	io.getSocketio(server);//start Socket.io

	// ...
</pre>
<p>启动服务器之后，前端页面便可以从http://localhost:3000/socket.io/socket.io.js加载前端部分的socketio的代码</p>
<p>3. 分离功能业务和socket.io的配置</p>
<p>在根目录下新建model/funccore.js:</p>
<pre>
	// model/funccore.js
	var funccore = {};

	/**
	 * message send/get app
	 */
	funccore.init = function(io) {
		io.on('connection', function(socket) {
			console.log('a user connected');
			socket.on('test message', function(msg){
				console.log("message : " + msg);
				io.emit('test message', msg);
			});
			socket.on('disconnect', function(){
				console.log('user disconnected');
			});
		});
	};

	module.exports = funccore;
</pre>
<p>4. 修改socketio.js</p>
<pre>
	// socketio.js
	var socketio = {};
	var socket_io = require('socket.io');
	var funccore = require('./model/funccore');

	//get io
	socketio.getSocketio = function(server){
		var io = socket_io.listen(server);
		// Start app
		funccore.init(io);
	};

	module.exports = socketio;
</pre>
<p>5. 修改index.ejs</p>
<pre><xmp>
	<html>
		<head>
			<title><%= title %></title>
			<link rel='stylesheet' href='/stylesheets/style.css' />
		</head>
		<body>
			<script src="http://localhost:3000/socket.io/socket.io.js"></script>
			<script src="https://code.jquery.com/jquery-1.11.1.js"></script>
			<script>
				$(function () {
					var socket = io();
					$('form').submit(function(){
						socket.emit('test message', $('#m').val());
						$('#m').val('');
						return false;
					});
					
					socket.on("test message", function(obj) {
						var curContent = $('#messages').html();
						$('#messages').html(curContent+'<li>'+obj+'</li>');
					});
				});
			</script>
			<ul id="messages"></ul>
			<form action="">
				<input id="m" autocomplete="off" /><button>Send</button>
			</form>
		</body>
	</html>
</xmp></pre>
