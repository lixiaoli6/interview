1.HTTP状态码
200	|	操作成功	|
301     永久重定向
302     临时重定向
304     缓存
400	|	参数校验失败	|
401 |	未登录或token已过期	|
402	|	用户已禁用	|
403	|	禁止用户访问	|
404	|	用户名或密码错误	|
500	|	服务器端发生错误	|
503     服务器不能处理客户端请求，一段时间后可能恢复正常
2.什么是AJAX，如何实现
    ajax是一种能够实现局部网页刷新的技术，可以使网页异步刷新。
        ajax的实现主要包括四个步骤：
            （1）创建核心对象XMLhttpRequest；
            （2）利用open方法打开与服务器的连接；
            （3）利用send方法发送请求；（"POST"请求时，还需额外设置请求头）
            （4）监听服务器响应，接收返回值。
3.什么是跨域？怎么解决跨域问题？
    跨域问题实际上是由于同源策略衍生出的一个问题，当传输协议，域名端口任一部分不一致时，便会产生跨域问题，从而拒绝请求，但<img src=XXX> <link href=XXX><script src=XXX>天然允许跨域加载资源
    解决方案
    （1）JSONP
            原理：利用<script>;标签没有跨域限制的漏洞，使得网页     可以得到从其他来源动态产生的JSON数据（前提是服务器支持）。
            优点：实现简单，兼容性好。
            缺点：仅支持get方法，容易受到XSS攻击。
        （2）CORS
        原理：服务器端设置Access-Control-Allow-Origin以开启CORS。该属性表示哪些域名可以访问资源，如设置通配符则表示所有网站均可访问。
        实现实例（express)：
（3）Node中间件代理
            原理：同源策略仅是浏览器需要遵循的策略，故搭建中间件服务器转发请求与响应，达到跨域目的。
（4）nginx反向代理
            原理：类似Node中间件服务器，通过nginx代理服务器实现。
            实现方法：下载安装nginx，修改配置。
    5.postMessage(H5中新增)
4.Cookie、sessionStorage、localStorage区别
共同点：都是保存在浏览器端，且同源的。 
区别：
（1）cookie数据始终在同源的http请求中携带，即cookie在浏览器和服务器间来回传递。
sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。
（2）cookie数据不能超过4k(适合保存小数据)。 
sessionStorage和localStorage容量较大，
（3）数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭前有效。
localStorage：始终有效，窗口或浏览器关闭也一直保存，需手动清除；
cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。
（4）作用域不同。 sessionStorage不在不同的浏览器窗口中共享；
localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。
应用场景：
localStorage：常用于长期登录（+判断用户是否已登录），适合长期保存在本地的数据。
sessionStorage ：敏感账号一次性登录；
 cookies与服务器交互。
5.get和post区别
简单来说：GET产生一个TCP数据包，POST产生两个TCP数据包
　　严格的说：对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；
　　而对于POST请求。浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）
GET请求的参数是放在请求的URL中，而POST方法是放在请求体中
GET请求在URL中传递参数时会有长度限制，而POST无限制（不是绝对的，只是相对来说）
GET请求会被浏览器主动缓存，而POST不会
GET请求的参数会保存在浏览器中，而POST的参数不会保存在浏览器中
6.http和https的区别
HTTPS = HTTP + SSL

　　1、https有ca证书，http一般没有

　　2、http是超文本传输协议，信息是明文传输。https则是具有安全性的ssl加密传输协议

　　3、http默认80端口，https默认443端口。
7.说说网络分层里七层模型是哪七层
应用层：允许访问OSI环境的手段

　　表示层：对数据进行翻译、加密和压缩

　　会话层：建立、管理和终止会话

　　传输层：提供端到端的可靠报文传递和错误恢复

　　网络层：负责数据包从源到宿的传递和网际互连

　　物理层：通过媒介传输比特,确定机械及电气规范
8.TCP和UDP的区别
TCP（Transmission Control Protocol，传输控制协议）是基于连接的协议，也就是说，在正式收发数据前，必须和对方建立可靠的连接。一个TCP连接必须要经过三次“对话”才能建立起来



UDP（User Data Protocol，用户数据报协议）是与TCP相对应的协议。它是面向非连接的协议，它不与对方建立连接，而是直接就把数据包发送过去！UDP适用于一次只传送少量数据、对可靠性要求不高的应用环境

9.SSL有几次握手，具体过程
10.ajax请求时，如何解释json数据
    如果是字符串形式的json：eval("("+ajax.response+")")
    如果是本地的json文件：JSON.parse(data)