<p><b>PWA</b>(Progressive Web App, 渐进式网页应用)</p>
<p><b>SPA</b>(Single-page Application, 单页web应用)</p>
<h3>什么是PWA</h3>
<p>PWA是指可以在任何浏览器上执行的支持互联网的应用程序，由服务器端脚本（PHP、ASP）和客户端脚本（JS、HTML）组成。</p>
<h3>PWA的优势</h3>
<ul>
	<li>有无服务人员，服务人员是PWA背后强大的技术支撑。例如实现离线模式工作等。</li>
	<li>网络的安全，尊重隐私+原生应用的访问能力。</li>
	<li>简单易安装。</li>
	<li>跨平台。</li>
</ul>
<h3>PWA的缺点</h3>
<ul>
	<li>不支持所有浏览器，包括Safari。</li>
	<li>有些功能如应用程序之间的通信，近场通信等不可用。</li>
</ul>
<h3>什么是SPA</h3>
<p>它将所有的活动局限于一个Web页面中，仅在该Web页面初始化时加载相应的HTML、JavaScript 和 CSS。一旦页面加载完成了，SPA不会因为用户的操作而进行页面的重新加载或跳转。而是利用 JavaScript 动态的变换HTML的内（采用的是div切换显示和隐藏），从而实现UI与用户的交互。由于避免了页面的重新加载，SPA 可以提供较为流畅的用户体验。</p>
<h3>PWA + SPA有何优势</h3>
<ul>
	<li>https 环境部署。</li>
	<li>响应式设计，一次部署，可以在移动设备和 PC 设备上运行。</li>
	<li>在不同浏览器下可正常访问。</li>
	<li>浏览器离线和弱网环境可极速访问。</li>
	<li>可以把 App Icon 入口添加到桌面。</li>
	<li>点击 Icon 入口有类似 Native App 的动画效果。</li>
	<li>灵活的热更新</li>
</ul>
<h3>前后端分离</h3>
<p>传统MVC形式：前端html，后端套界面，转成jsp像freemarker这种模板引擎。</p>
<p>前后端分离的开辟形式：前端html5,js,css3+前端MVC形式，后端数据接口。</p>
<p>SPA便是前后端分离的例子，一切用到的展示数据都是后端经由过程异步接口供给，前端只负责展示。</p>