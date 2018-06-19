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
	bin
		www
	public
		images
		javascripts
		stylesheets
			style.css
	route
		index.js
		users.js
	views
		error.ejs
		index.ejs
	app.js
	package.json
</pre>