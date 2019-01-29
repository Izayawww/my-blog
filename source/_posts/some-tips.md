---
title: some-tips
date: 2018-09-03 18:09:05
tags: 知识
description: 一些知识
---
### TCP/IP（互联网相关的各类协议族的总称）
    协议族按层次分别分为以下 4  层：
     应用层、传输层、网络层和数据链路层。
     1. IP(网际协议，位于网络层) 负责传输
    将各种数据包传输给对方，为了确保数据确实的传送，需要满足各类条件，其中两个重要的条件就是IP地址和MAC( Media Access Control)地址
    IP地址指明了节点被分配的地址，MAC地址是指网卡所属于的固定地址。
    IP间的通信依赖MAC地址，在通信过程中会使用ARP协议( Address Resolution Protocol 一种用以解析地址的协议)
    根据通信方的IP地址反查出对应的MAC地址
    2.TCP(位于传输层) 确保可靠性
    TCP提供可靠的字节流服务，将大块数据分割成以报文段为单位的数据包。
     TCP  协议采用了三次握手（ three-way handshaking ）策略：
     （1）发送端首先发送一个带 SYN  标志的数据包给对方。
     （2）接收端收到后，回传一个带有 SYN/ACK  标志的数据包以示传达确认信息。
     （3）最后，发送端再回传一个带 ACK  标志的数据包，代表 “ 握手 ” 结束。
    3. DNS服务(位于应用层) 负责域名解析
    在平时访问过程中，一般都是通过使用主机名或域名进行访问，而不是通过IP地址直接访问，但要让计算机去理解名称，就变得困难了。
    为了解决上述的问题， DNS  服务应运而生。 DNS  协议提供通过域名查找 IP  地址，或逆向从 IP  地址反查域名
### URI和URL：
    URI 统一资源标识符,由某个协议方案表示的资源的定位标识符。协议方案是指访问资源所使用的协议类型名 称。
    URL  统一资源定位符,表示资源的地点（互联网上所处的位置） URL  是 URI  的子集
### HTTP：
    用于客户端和服务器，通过请求响应达成通信：
    请求报文是由请求方法、请求 URI 、协议版本、可选的请求首部字段和内容实体构成的。
    GET /index.htm HTTP/1.1 请求访问某台服务器上/index.html的页面资源

    HTTP/1.1 200 OK
    Date: Tue, 10 Jul 2012 06:50:15 GMT
    Content-Length: 362
    Content-Type: text/html
    <html>
    ……
    响应报文基本上由协议版本、状态码（表示请求成功或失败的数字代码）、用以解释状态码的原因短语、可
    选的响应首部字段以及实体主体构成。
### HTTP 协议自身不具备保存之前发送过的请求或响应的功能
    优点：由于不必保存状态，自然可减少服务器的 CPU  及内存资源的消耗。
    使用Cookie状态管理： Cookie  技术通过在请求和响应报文中写入 Cookie  信息来控制客户端的状态。
    Cookie  会根据从服务器端发送的响应报文内的一个叫做 Set-Cookie  的首部字段信息，通知客户端保存
    Cookie 。当下次客户端再往该服务器发送请求时，客户端会自动在请求报文中加入 Cookie  值后发送出去。
    服务器端发现客户端发送过来的 Cookie  后，会去检查究竟是从哪一个客户端发来的连接请求，然后对比服务
    器上的记录，最后得到之前的状态信息。
    HTTP协议使用 URI  定位互联网上的资源。
### 持久连接节省通信量：
    HTTP  协议的初始版本中，每进行一次 HTTP  通信就要断开一次 TCP  连接，为解决TCP  连接的问题， HTTP/1.1  和一部分的 HTTP/1.0  想出了
    持久连接（ HTTP PersistentConnections ，也称为 HTTP keep-alive  或 HTTP connection reuse ）的方法。持久连接的特点是，只要任意
    一端没有明确提出断开连接，则保持 TCP  连接状态。旨在建立 1  次 TCP  连接后进行多次请求和响应的交互
    HTTP的几种请求方法用途
    1、GET方法
    发送一个请求来取得服务器上的某一资源
    
    2、POST方法
    向URL指定的资源提交数据或附加新的数据
    
    3、PUT方法
    跟POST方法很像，也是想服务器提交数据。但是，它们之间有不同。PUT指定了资源在服务器上的位置，而POST没有
    
    4、HEAD方法
    只请求页面的首部
    
    5、DELETE方法
    删除服务器上的某资源
    
    6、OPTIONS方法
    它用于获取当前URL所支持的方法。如果请求成功，会有一个Allow的头包含类似“GET,POST”这样的信息
    
    7、TRACE方法
    TRACE方法被用于激发一个远程的，应用层的请求消息回路
    
    8、CONNECT方法
    把请求连接转换到透明的TCP/IP通道

### HTTP状态码及其含义
    1XX：信息状态码
    100 Continue 继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
    
    2XX：成功状态码
    200 OK 正常返回信息
    201 Created 请求成功并且服务器创建了新的资源
    202 Accepted 服务器已接受请求，但尚未处理
    
    3XX：重定向
    301 Moved Permanently 请求的网页已永久移动到新位置。
    302 Found 临时性重定向。
    303 See Other 临时性重定向，且总是使用 GET 请求新的 URI。
    304 Not Modified 自从上次请求后，请求的网页未修改过。
    
    4XX：客户端错误
    400 Bad Request 服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。
    401 Unauthorized 请求未授权。
    403 Forbidden 禁止访问。
    404 Not Found 找不到如何与 URI 相匹配的资源。
    
    5XX: 服务器错误
    500 Internal Server Error 最常见的服务器端错误。
    503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。

### typeof null
    js第一版中，数值以32字节存储，由标志位（1~3字节）和数值组成，不同的对象在底层都表示为二进制，
    null的二进制全是0，所以typeof null结果为object。
    
    1. 000：对象，数据是对象的应用。
    2. 1：整型，数据是31位带符号整数。
    3. 010：双精度类型，数据是双精度数字。
    4. 100：字符串，数据是字符串。
    5. 110：布尔类型，数据是布尔值。
    
    undefined 是一个没有设置值的变量。
    typeof 一个没有值的变量会返回 undefined。
    null 和 undefined 的值相等，但类型不等
    
### 闭包：
    闭包在 JavaScript 中常用来实现对象数据的私有
    什么是闭包？
    简言之，闭包是由函数引用其周边状态（词法环境）绑在一起形成的（封装）组合结构。在 JavaScript 中，闭包在每个函数被创建时形成。
    闭包让我们能够从一个函数内部访问其外部函数的作用域。
    要使用闭包，只需要简单地将一个函数定义在另一个函数内部，并将它暴露出来。要暴露一个函数，可以将它返回或者传给其他函数。
### HTTP工作原理
    一次HTTP操作称为一个事务，其工作整个过程如下：
    
    1. 地址解析
    如用客户端浏览器请求这个页面：#3
    从中分解出协议名、主机名、端口、对象路径等部分，对于我们的这个地址，解析得到的结果如下：
    协议名：https
    主机名：github.com
    端口：''
    对象路径：/web/blog/a
    在这一步，需要域名系统DNS解析域名github.com，得主机的IP地址。
    
    2. 封装HTTP请求数据包
    把以上部分结合本机自己的信息，封装成一个HTTP请求数据包
    
    3. 封装成TCP包，建立TCP连接（TCP的三次握手）
    在HTTP工作开始之前，客户机（Web浏览器）首先要通过网络与服务器建立连接，该连接是通过TCP来完成的，该协议与IP协议共同构建Internet，即著名的TCP/IP协议族，因此Internet又被称作是TCP/IP网络。HTTP是比TCP更高层次的应用层协议，根据规则，只有低层协议建立之后才能，才能进行更层协议的连接，因此，首先要建立TCP连接，一般TCP连接的端口号是80。
    TCP的三次握手
    (1) 主机向服务器发送一个建立连接的请求；
    
    (2) 服务器接到请求后发送同意连接的信号；(为了防止已失效的连接请求报文段传至服务器导致错误)
    
    (3) 主机接到同意连接的信号后，再次向服务器发送了确认信号 ;
    
    
    4. 客户机发送请求命令
    建立连接后，客户机发送一个请求给服务器，请求方式的格式为：统一资源标识符（URL）、协议版本号，后边是MIME信息包括请求修饰符、客户机信息和内容。
    
    5. 服务器响应
    服务器接到请求后，给予相应的响应信息，其格式为一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容。
    实体消息是服务器向浏览器发送头信息后，它会发送一个空白行来表示头信息的发送到此为结束，接着，它就以Content-Type应答头信息所描述的格式发送用户所请求的实际数据
    
    6. 服务器关闭TCP连接
    一般情况下，一旦Web服务器向浏览器发送了请求数据，它就要关闭TCP连接，然后如果浏览器或者服务器在其头信息加入了这个请求头Connection:keep-alive，TCP连接在发送后将仍然保持打开状态，于是，浏览器可以继续通过相同的连接发送请求。保持连接节省了为每个请求建立新连接所需的时间，还节约了网络带宽。
    断开连接(TCP的四次挥手)
    (1) 主机向服务器发送一个断开连接的请求；
    
    (2) 服务器接到请求后发送确认收到请求的信号；(此时服务器可能还有数据要发送至主机)
    
    (3) 服务器向主机发送断开通知；(此时服务器确认没有要向主机发送的数据)
    
    (4) 主机接到断开通知后断开连接并反馈一个确认信号，服务器收到确认信号后断开连接；
    
### 浏览器从输入url到加载完成 都发生了什么
    1、浏览器地址栏输入url
    2、浏览器会先查看浏览器缓存–系统缓存–路由缓存，如有存在缓存，就直接显示。如果没有，接着第三步
    3、域名解析（DNS）获取相应的ip
    4、浏览器向服务器发起tcp连接，与浏览器建立tcp三次握手
    5、握手成功，浏览器向服务器发送http请求，请求数据包
    6、服务器请求数据，将数据返回到浏览器
    7、浏览器接收响应，读取页面内容，解析html源码，生成DOM树
    8、解析css样式、浏览器渲染，js交互

### SSL工作原理
    SSL(Server socket layer) 是一种保证网络两个节点进行安全通信的协议。SSL和TLS建立在TCP/IP协议基础上。建立在SSL上的HTTP协议称为HTTPS，默认端口443。SSL使用加密技术实现会话双方信息的安全传递。
    
    SSL加密类型
    有两种基本的加解密算法类型：
    
    1. 对称加密
    密钥只有一个，加密解密为同一个密码，且加解密速度快，典型的对称加密算法有DES、AES，RC5，3DES等；对称加密主要问题是共享秘钥，除你的计算机（客户端）知道另外一台计算机（服务器）的私钥秘钥，否则无法对通信流进行加密解密。
    
    2. 非对称加密
    使用两个秘钥：公共秘钥和私有秘钥。私有秘钥由一方密码保存（一般是服务器保存），另一方任何人都可以获得公共秘钥。
    获取证书（经过CA认证过的公钥）有两种方式
    
    1. 从权威机制购买证书。
    安全证书由国际权威的证书机构(CA)，如VeriSign和Thawte颁发，它们保证了证书的可信性。一个安全证书只对一个IP有效，多个IP必需购买多个证书。
    
    2. 创建自我签名的证书。
    如果通信双方只关心数据在网络上的可以安全传输，并不需要对方进行身份验证，这种情况下，可以创建自多签名证书。这证书达不到身份认证的目的，但可以用于加密通信。
    SSL握手
    SSL 连接总是由客户端启动的。在SSL 会话开始时执行 SSL 握手。此握手产生会话的密码参数。关于如何处理 SSL 握手的简单概述，如下图所示。此示例假设已在 Web 浏览器 和 Web 服务器间建立了 SSL 连接。

### html5有哪些新特性、移除了那些元素
    新特性:
    （1）语意化更好的内容元素，比如 article、footer、header、nav、section，表单控件，calendar、date、time、email、url、search;
    （2）一些功能标签，如绘画 canvas，用于媒介播放的 video 和 audio 元素;
    （3）本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;sessionStorage 的数据在浏览器关闭后自动删除;
    （4）新的技术，如webworker, websocket, Geolocation;
    **移除的元素：**
    （1）纯表现的元素：basefont，big，center，font, s，strike，tt，u;
    （2）对可用性产生负面影响的元素：frame，frameset，noframes；
        cookies，session,sessionStroage和localStorage的区别：
    cookies，sessionStroage和localStorage是在客户端，session是在服务器端。服务器端的session机制， session 对象数据保存在服务器上。
    实现上，服务器和浏览器之间仅需传递session id即可，服务器根据session id找到对应用户的session对象。会话数据仅在一段时间内有效，这个时间就是server端设置的session有效期。服务器session存储数据安全一些，一般存放用户信息，浏览器只适合存储一般数据
    其次，是**cookies，sessionStroage和localStorage三者的区别**：
    （1）cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递。而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存（2）存储大小限制也不同，cookie数据不能超过4k，同时因为每次Http请求都会携带cookie（这里可能还会追问，cookie是在http报文什么地方，答:cookie是携带在http请求头上的），所以cookie只适合保存很小的数据，比如会话标识sessionStroage和localstroage虽然也有大小限制，但是比cookie大很多，可以达到5M；
    （3） 数据有效期也不同，cookie在设置的有效期（服务端设置）内有效，不管窗口或者浏览器是否关闭，sessionStroage仅在当前浏览器窗口关闭前有效（也就是说只要这个浏览器窗口没有关闭，即使刷新页面或进入同源另一页面，数据仍然存在。关闭窗口后，sessionStorage即被销毁）；localStroage始终有效，窗口或者浏览器关闭也一直保存；
    （4） Web storage 支持事件通知机制，可以将数据更新的通知发送给监听者。如下：
        `window.addEventListener("storage", function (e) {`
                `alert(e.newValue);`
            `});`
    Web Storage带来的好处： 减少网络流量：一旦数据保存在本地后，就可以避免再向服务器请求数据，因此减少不必要的数据请求，减少数据在浏览器和服务器间不必要地来回传递。 快速显示数据：性能好，从本地读数据比通过网络从服务器获得数据快得多，本地数据可以即时获得。再加上网页本身也可以有缓存，因此整个页面和数据都在本地的话，可以立即显示。 临时存储：很多时候数据只需要在用户浏览一组页面期间使用，关闭窗口后数据就可以丢弃了，这种情况使用sessionStorage非常方便。
    
### 前端页面优化
    1.http请求优化
        (1)减少HTTP请求
            * 压缩合并js、css文件，可配置webpack使其合并成一个唯一出口文件
             * 延迟加载
            * 雪碧图CSS Sprite 一种CSS图像合并技术，该方法是将小图标和背景图像合并到一张图片上，然后利用css的背景定位
                          来显示需要显示的图片部分。
        (2)预加载 预先判断需要加载的数据，达到指定条件以后直接从浏览器缓存中获取
    2.页面/性能优化
        (1)引用优化
             *css放在head标签内，js文件放在body标签的最下面
             *css文件是异步加载的，浏览器在构建dom树的同时如果有对应的样式就直接显示出来，这样会让样式更早的出现
             *js文件在下载时会阻塞dom树构建，只有js下载完成后才回继续构建下面的dom树，将js文件的引用放在最下面可在视觉上
                        减少白屏的出现
        (2)将js动画替换成css动画

### js继承
    1.原型链继承:直接让子类的prototype属性指向父类的实例,这样在子类的原型上拥有了父类的私有和公有属性.
    2.借用构造函数(经典继承):在子类的构造函数中使用父类.call(this)方法,在构造新的子类实例的时候其实也执行了父类的
    初始化代码,并且改变了this指向,这样子类就可以使用父类的私有属性了
    3.原型式继承Object.create():create函数内部创建了一个临时的中间类,让这个类的原型等于传进来的原型对象,最后返回
    了这个中间类的实例,让子类的prototype属性等于返回的实例,这样就拿到了父类的公有方法.

### 水平垂直居中
    1、定位 盒子宽高已知， position: absolute; left: 50%; top: 50%; margin-left:-自身一半宽度; margin-top: -自身一半高度;
    
    2、table-cell布局 父级 display: table-cell; vertical-align: middle;  子级 margin: 0 auto;
    
    3、定位 + transform ; 适用于 子盒子 宽高不定时；
    
        position: relative / absolute;
        /*top和left偏移各为50%*/
           top: 50%;
           left: 50%;
        /*translate(-50%,-50%) 偏移自身的宽和高的-50%*/
        transform: translate(-50%, -50%); 
    
    4、flex 布局
        父级： 
            /*flex 布局*/
            display: flex;
            /*实现垂直居中*/
            align-items: center;
            /*实现水平居中*/
            justify-content: center;
            
### 跨域解决方案
    1.jsonp 动态创建script标签，请求一个带参网址并指定回调函数
    缺点：只能实现get一种请求。
        原生实现：
            <script>
                var script = doucment.createElement('script');
                script.src="http://www.asdf.com/?callback=abackfunction";
                function abackfunction(data){
                    数据处理；
                }
                                document.getElementsByTagName('head')[0].appendChild(script); 
            </script>
    发起端定义jsonp的回调处理。
    发起端做jsonp跨域请求
    响应端使用发起端的同名函数处理跨域请求

    2.CORS
    浏览器对跨域请求区分为“简单请求”与“非简单请求”
    “简单请求”满足以下特征：
    （1) 请求方法是以下三种方法之一：
             HEAD
             GET
             POST
    （2）HTTP的头信息不超出以下几种字段：
             Accept
             Accept-Language
             Content-Language
             Last-Event-ID
             Content-Type： application/x-www-form-urlencoded、 multipart/form-data、text/plain
    
    简单请求 只需要CORS服务端在接受到携带Origin字段的跨域请求后，在response header中添加Access-Control-Allow-Origin等字段给浏览器做同源判断。
    非简单请求 需要CORS服务端对OPTIONS类型的请求做处理，其他与简单请求一致
    
    3.nginx代理跨域