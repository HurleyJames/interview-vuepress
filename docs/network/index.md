1. **HTTP 和 HTTPS 的区别**

    * **开销**：HTTPS 协议需要到 CA 申请证书或者自制证书
    * **安全性**：HTTP 的信息是明文传输，是简单无状态的；HTTPS 则是具有安全性的 SSL 加密传输，HTTPS 协议是由 SSL+HTTP 协议构建的，可进行加密传输、身份认证的网络协议，比 HTTP 协议安全
    * **资源消耗**：HTTP 是直接与 TCP 进行数据传输；HTTPS 运行在 SSL/TSL 之上，SSL/TSL 运行在 TCP 之上，需要消耗更多的 CPU 和内存资源；
    * **端口不同**：HTTP 用到的端口是 80（需要国内备案），HTTPS 用到的端口是 443

2. **HTTP2 与 HTTP1.x 相比的新特性**

    * HTTP2 使用新的二进制格式传输，HTTP1.x 使用文本（字符串）传输。二进制协议解析起来更高效

    * HTTP2 支持多路复用，即连接共享，即每一个`request`都是用作连接共享机制的。

        > 在 HTTP1.x 协议中，「浏览器客户端在同一时间，针对同一域名下的请求有一定的数量限制。超过限制数目的请求会被阻塞」。HTTP2 的多路复用（Multiplexing）允许同时超过单一的 HTTP2 连接发起多重的请求-响应消息。

        ![HTTP1.x与HTTP2的对比](https://i.loli.net/2021/01/07/W5OIPnRbZigDFGM.png)

    * HTTP2 头部压缩，通过`gzip`和`compress`压缩头部然后再发送，既避免了重复`header`的传输，又减小了需要传输的大小

    * HTTP2 支持服务器推送

3. **HTTP2 和 HTTPS 的关系**

    HTTP2 与 HTTPS **同属为一种网络传输协议**。HTTP2（原名 HTTP/2.0）即超文本传输协议 2.0，是下一代 HTTP 协议。HTTPS是以安全为目标的 HTTP 通道，在 HTTP 的基础上通过传输加密和身份认证保证了传输过程的安全性，HTTPS 在 HTTP 的基础下加入 SSL 层，HTTPS 的安全基础是 SSL，因此加密的详细内容就需要 SSL。

    HTTP2 虽然是下一代 HTTP 协议，做了一些改动（如二进制分帧、多路复用、头部压缩、服务器推送等），但是依然采取的是**不加密的传输方式**，容易导致数据在传输过程中被截取或篡改，无法保证数据的完整性。

    而 HTTPS 采用的则是**加密传输**，就是在HTTP协议下增加了一层 SSL 协议，通过对整个通信线路进行加密来防止通信内容被窃听、篡改或伪装。

    所以：

    * https: **加密**的 http 协议，默认 443 端口，**基于TCP协议**。
    * http2: **第二代**http 协议，相较于 HTTP1.x，大幅度的提升了 web 性能。在与 HTTP/1.1 完全语义兼容的基础上，进一步**减少了网络延迟和传输的安全性**，**基于 TCP 协议**。

4. **什么是数字签名和数字证书**

    * **数字签名**：为了避免数据在传输过程中被替换（例如被黑客修改了报文内容），所以需要发送端发送一个数字签名，即把数据的摘要消息进行加密，比如使用MD5进行加密，得到一个数字签名，然后把这个数字签名和数据一起发送。然后接收端把收到的数据摘要部分进行 MD5（相同加密算法）进行加密，如果加密后的结果和数字签名是一样的，就说明数据是正确的真实的。
    * **数字证书**：因为在对称加密中，发送端和接收端双方都是使用公钥进行解密的。**数字签名可以保证数据不被替换**，但是不能保证公钥不被替换。因为数据是通过公钥加密的，如果公钥被替换了，那么数据也可以被伪造。所以我们要确保公钥也是真的。那么，CA 证书机构会负责颁发一个证书，里面的公钥保证是真的，用户在请求服务器时，服务器将证书发给用户，而这个证书是由系统内置证书备案的，就能保证证书里的公钥是真的。

5. **对称加密与非对称加密**

    **对称密钥加密**指的是使用同一个密钥进行加密和解密，这种方法存在的问题就是密钥如何安全地发送给对方。

    **非对称加密**是指使用一对非对称密钥，即公钥和私钥。公钥是可以任意发布的，但是私钥只有自己知道。发送方使用接收方的公钥进行加密处理，接收方收到加密信息后，使用自己的私钥进行解密。

    因为非对称加密的方式只会发送公钥而不会发送用来解密的私钥，所以可以保证安全性。但是相比对称加密，它的速度非常慢。所以，我们仍然使用对称加密来传送消息，但对称加密所使用的密钥可以通过非对称加密的方式发送出去。

6. **TCP 与 UDP 的区别**

    * TCP 是面向连接的，UDP 是无连接的；
    * TCP 传输性可靠，UDP 传输性不可靠；
    * TCP 以**字节流**的形式传输，UDP 以**数据报文段**的形式传输；
    * TCP 传输效率慢，UDP 传输效率快；
    * TCP 所需资源多，UDP 所需资源少；
    * TCP 首部字节是 20-60，UDP 首部字节是 8；
    * TCP 应用于要求通信数据可靠的场景，例如文件传输，邮件传输等；UDP 则要求通信速度较快的场景，如域名转换，直播等；
    * TCP 的可靠性是通过顺序编号和确认（ACK）来实现的。

7. **TCP 的字节流是什么机制** <Badge text="Uncompleted"/>

8. **字节流和字符流说一下** <Badge text="Uncompleted"/>

9.  **TCP 协议的可靠性是如何保证的**

    * **数据包校验**：目的是检测数据在传输过程中的任何变化，若校验出包有错，则丢弃报文段并且不做任何响应，这样 TCP 发送数据端就会超时而重发数据；
    * **对失序的数据报重排序**：既然 TCP 报文段作为 IP 数据报来传输，因为 IP 数据报到达时可能会失效，所以 TCP 报文段的到达也可能会失序。所以 TCP 会对失序数据进行重新排序，然后再上交给应用层；
    * **丢弃重复数据**
    * **应答机制**：当 TCP 收到发自 TCP 连接另外一端的数据，它将发送一个确认（不是立即发送）；
    * **超时重发**：当 TCP 发出一个段后，会启动一个定时器，等待目的端确认收到这个报文段。如果不能及时收到这个确认，就需要重新发送这个报文段；
    * **流量控制**：TCP 连接的每一方都有固定大小的缓冲空间。TCP 接收端只需要另一端（发送端）发送接收端的缓冲区能够容纳得下的数据，这样做可以防止较快主机致使较慢主机的缓冲区溢出，这就是所谓的流量控制（TCP 使用的流量控制协议是可变大小的滑动窗口协议）。

10. **TCP 和 UDP 对应的常见应用层协议**

    * TCP 对应的应用层协议有：
        * FTP：定义了文件传输协议
        * SMTP：定义了简单邮件传输协议
        * POP3：POP3 是用于接收邮件的，和 SMTP 对应
        * HTTP：从 Web 服务器传输超文本到本地浏览器的传送协议
    * UDP 对应的应用层协议有：
        * DNS：用于域名解析服务，将域名地址转换为 IP 地址
        * SNMP：简单网络管理协议
        * TFTP：简单文件传输协议

11. **为什么TCP连接需要三次握手？为什么要四次挥手？画出全过程，并标注ack确认号和seq序列号的值**

    **三次握手**：

    1. 第一次握手：客户端发送 SYN=1 的包到服务器，进入 SYN_SEND 状态，等待服务器确认；
    2. 第二次握手：服务器收到 SYN 的包后，必须使用确认包 ACK 确认客户的 SYN，同时自己也发送 SYN 包给客户端，即发送 ACK=1，SYN=1 的包，此时服务器进入 SYN_RECY 状态；
    3. 第三次握手：客户端收到服务器的 SYN+ACK 的包，向服务器发送确认包 ACK=1，发送完毕后，就进行 ESTABLISHED 状态，完成三次握手。

    ![三次握手示意图](https://i.loli.net/2021/01/07/4drOhlxLBu21QMU.png)

    **四次挥手**：

    1. 客户端主动发送 FIN=1
    2. 服务端收到后发送 ACK=1
    3. 服务端再发送 FIN=1，ACK=1
    4. 客户端最后向服务端发送 ACK=1

    ![四次挥手示意图](https://i.loli.net/2021/01/07/N8RQHA2KwqhFT4p.png)


12. **HTTP 与 TCP 的区别**

    TCP 是传输层协议，主要解决数据如何在网络中进行传输。HTTP 协议是应用层协议，主要解决如何包装数据。

13. **保活计时器的作用**

    除了时间等待计时器之外，TCP 还有一个保活计时器。比如，一个客户与服务器建立了 TCP 连接，如果这时突然客户端主机发生故障，那么服务器也不应该再白白等待下去，所以需要使用到保活计时器。

    服务器每次收到一次客户的数据，就要重新设置保活计时器，时间通常设置是两个小时。如果在这个时间内都没有收到客户端的数据，服务端就会发送一个探测报文段（每隔 75 秒发送一次）。若连续发送 10 次后都没有收到客户端的响应，服务端就会认为客户端出现了故障，从而关闭连接。

14. **TCP 的拥塞处理**

    拥塞控制和流量控制的不同的，拥塞控制是一个全局性的过程，涉及到所有的主机，所有的路由器以及与降低网络传输性能相关的所有因素；流量控制是指点对点通信量的控制，是一个端到端的问，它的作用是抑制发送端发送数据的速率，以便使接收端来得及接收。

    **拥塞**是指在某段时间，若对网络中某一资源的需求超过了该资源所能提供的可用部分，那么网络的性能就会变坏。为了进行拥塞控制，TCP 发送方要维持一个拥塞窗口（cwnd）的状态变量，拥塞控制窗口的大小取决于网络的拥塞程度，并且可以动态变化。发送方的发送窗口会从拥塞窗口和接收方的接收窗口这两者中取较小的那个。

    TCP 的拥塞控制采用了四种算法：**慢开始**、**拥塞避免**、**快重传和快恢复**。在网络层也可以使路由器采用适当的分组丢弃策略，以减少网络拥塞的发生；

    * **慢开始**：当主机开始发送数据时，如果立即把大量的数据字节同时注入到网络，很有可能会引起网络阻塞。所以，较好的方法是先探测一下，即由小到大逐渐增大发送窗口（逐渐增大拥塞窗口数值）。例如，cwnd 的初始值为 1，每经过一个传播轮次，cwnd 加倍。
    * **拥塞避免**：拥塞避免算法的思路是让拥塞窗口 cwnd 缓慢增大，即每经过一个往返时间RTT就把发送方的 cwnd 加。
    * **快重传和快恢复**：快重传和快恢复（fast retransmit and recovery，FRR）是一种拥塞控制算法，它能快速恢复丢失的数据包。如果没有 FRR，那么如果数据包丢失了，TCP 就会使用定时器要求传输暂停；而如果有了 FRR，当接收方收到了不按顺序的数据段，就会立即给发送发发送一个**重复确认**，当发送方收到了三个重复确认，就会假定这个数据报丢失了，并立即重传这些丢失的数据段。所以，有了 FRR，就不会因为暂停而耽误重传要求。当单个数据包丢失时，FRR 十分有效；当多个数据包在短时间内丢失，FRR 不能很有效地工作；

15. **HTTP 方法有哪些**

    * GET：获取资源，网络中绝大部分请求都会 GET 请求；
    * HEAD：获取报文首部，使用和 GET 相似，但是不会返回报文的实体主体部分；
    * POST：传输实体主体；
    * PUT：上传文件，不带有验证机制，所有任何人都能上传文件，存在安全性问题，一般不推荐使用该方法；
    * PATCH：对资源进行部分修改。PUT 也可以修改资源，但是是完全替代，而 PATCH 允许部分修改；
    * OPTIONS：查询指定的 URL 支持的方法；
    * CONNECT：要求与代理服务器通信时建立隧道；使用 SSL 和 TLS 协议把通信内容加密后经网络隧道传输；
    * TRACE：追踪路径，服务器会把通信路径返回给客户端

16. **HTTP 中，POST 与 GET 的区别**

    * 用途不同：GET 是从服务器上获取数据，POST 向服务器传送数据；
    * 数据传输方式不同：GET 请求通过 URL 传输数据，POST 通过**请求体**传输数据（先发送请求头再发请求体，实际上是两次请求）；
    * 传输数据量限制不同：GET 传送的数据量小，不能大于 2KB（因为浏览器对 URL 的长度有限制）；POST 传送的数据量大，一般默认为不受限制；
    * GET 的数据在 URL 中，通过历史记录或缓存可以很容易查到数据信息；POST 的数据在请求主体内，所以有一定的安全性保证
    * GET 是安全且幂等（同一个请求方法执行多次和仅执行一次的效果完全相同）；POST 是非安全非幂等（每次请求对资源的改变并不是相同的），所以 GET 不会改变服务器上的资源，而 POST 会对服务器资源进行改变；

17. **HTTP 的长连接和短连接分别是什么**

    HTTP 的长连接和短连接实际上是 TCP 的长连接和短连接。

    * **长连接**：HTTP1.1 规定了默认保持长连接，也称为**持久连接**。当数据传输完成后保持 TCP 连接不断开，等待在同域名下继续用这个通道传输数据。但是长连接不是永久的连接，它有一个保持时间。使用长连接的 HTTP 协议，会在响应头加入这行代码：`Connection:keep-alive`
    * **短连接**：在 HTTP/1.0 中，默认使用短连接。浏览器和服务器每进行一次 HTTP 操作，就要建立一个连接，但任务结束就会中断这个连接

    使用长连接的好处：

    * 同一个客户端可以使用这个长连接处理其他请求，避免 HTTP 重新连接和断开消耗时间；
    * 服务器可以利用这个连接**主动推送**消息到客户端

18. **DNS 是什么，DNS 协议的原理**

    DNS 的全程是 Domain Name System 或者 Domain Name Service，主要作用就是将网址（域名）解析成电脑可以理解的 IP 地址，这个过程就是 DNS 域名解析（一个域名往往对应多个 DNS 地址）。

19. **DNS 的解析过程**

    1. 输入`www.baidu.com`这个域名，操作系统会先检查自己本地的 hosts 文件中是否已经有这个网址映射关系，如果有，就先调用这个已存在的IP地址映射去完成域名解析；
    2. 如果本地 hosts 文件中没有这个域名的映射，则查找本地 DNS 解析器缓存中是否有这个网址的映射，如果有就返回这个完成域名解析；
    3. 如果 hosts 和本地 DNS 解析器缓存里都没有这个域名的映射，那么就会找本地 DNS 服务器，此服务器收到查询请求时，如果要查询的域名包含在本地配置区域资源中，就返回解析结果给客户机，完成域名解析（此解析具有权威性）；
    4. 如果要查询的域名不由本地 DNS 服务器区域解析，但该服务器已缓存了此网址的映射关系，就调用这个进行 IP 地址映射，完成域名解析（此解析不具有权威性）；
    5. 如果本地 DNS 服务器本地区域资源和缓存解析都失败了，就让根 DNS 服务解析，如果自己无法解析，就联系下一级顶级域 DNS 服务器查询，如果还无法解析就联系下一级次级域名解析，如果还无法解析就使用下一级——主机名（host），又称三级域名进行解析，直到找个这个域名的主机为止。

    **另外一种表述方法是**：

    1. 发起基于域名的请求后，首先检查**本地缓存**（浏览器缓存$\longrightarrow$操作系统的 hosts 文件）；
    2. 如果**本地缓存**有，直接返回目标 IP 地址，否则将域名解析请求发送给**本地 DNS 服务器**；
    3. 如果**本地 DNS 服务器**中有，直接返回目标 IP 地址；如果没有，**本地DNS服务器**将解析请求发送给**根 DNS 服务器**;
    4. **根 DNS 服务器**会返回给**本地 DNS 服务器**一个所查询的 **TLD 服务器（顶级域名服务器）**地址列表；
    5. **本地 DNS 服务器**再向上一步返回的** TLD 服务器**发送请求，**TLD 服务器**查询并返回域名对应的域名对应的**权威域名服务器**的地址；
    6. **本地 DNS 服务器**再向上一步返回的**权威域名服务器**发送请求，**权威域名服务器**会查询存储的域名和 IP 的映射关系表，将IP连同一个`TTL`（过期时间）值返回给**本地 DNS 服务器**；
    7. **本地 DNS 服务器**会将 IP 和主机名的映射保存起来，保存时间由`TTL`来控制；
    8. **本地 DNS 服务器**把解析的结果返回给用户，用户根据`TTL`值缓存在**本地系统缓存**中，域名解析过程结束。

    **递归查询与迭代查询**：

    1. 主机向本地域名服务器的查询一般都是采用递归查询（客户端只发出一次请求，要求对方给出最终结果）。递归查询时，返回的结果只有两种：查询成功或者查询失败；
    2. 本地域名服务器向根域名服务器的查询时迭代查询（客户端发出了一次请求，对方如果没有授权回答，它就会返回一个能解答这个查询的其它名称服务器列表，客户端会再向返回的列表中发出请求，直到找到最终负责所查域名的名称服务器，从它那得到最终结果，即根域名服务器$\rightarrow$顶级域服务器$\rightarrow$次级域服务器$\rightarrow$主机名host）。迭代查询（又称重指引）时，返回的是最佳的查询点或者主机地址。

20. **浏览器输入一个 URL 后发生了什么（从输入网址到获得页面的过程）**

    1. **DNS 解析**：浏览器会查询 DNS，获取该域名（URL）对应的 IP 地址；具体过程包括了浏览器搜索自身的 DNS 缓存、搜索操作系统的 DNS 缓存、读取本地的 Host 文件和向本地的 DNS 服务器进行查询等；
        1. 首先向本地 DNS 服务器查询缓存。本地 DNS 服务器会让根 DNS 服务器查询，如果不知道就再向顶级域 DNS 服务器查询，如果还不知道就再向权威 DNS 服务器查询；(一个域名为`www.baidu.com.`，根域名就是最后的`.`，只是因为每个域名都有根域名，所以通常省略了；根域名的下一级是顶级域名，比如`.com`，`.org`等；再下一级就是次级域名，比如`.baidu`；再下一级就是主机名（host）了，比如`www`，这个又称为三级域名)。所以，整个解析流程就是**分级查询**；
        2. 这里查询使用了**递归查询**和**迭代查询**
    2. **TCP 连接**：浏览器获得了域名对应的 IP 地址之后，浏览器就会向服务器请求建立连接，发起三次握手；
    3. **发送 HTTP 请求**：TCP 连接建立之后，浏览器会向服务器发送 HTTP 请求；
    4. **服务器处理请求并返回 HTTP 报文**：服务器接收到这个请求，并根据路径参数映射到特定的请求处理器进行处理，并将处理结果及相应的视图返回给浏览器；
    5. **浏览器解析渲染界面**：浏览器解析并渲染视图，如果有对 js、css 和图片等静态资源的引用，就重复上述步骤并向服务器请求这些资源；浏览器会根据其请求到的资源、数据渲染页面，最终向用户呈现一个完整的页面。
    6. **连接结束**

21. **HTTP 响应码（状态码）**

    - 1XX：Informational（信息性状态码），表示请求已经被收到了，需要进一步的处理才能完成；
    - 2XX：Success（成功状态码），成功处理请求；
    - 3XX：Redirection（重定向状态码），重定向使用 Location 指向的资源或者缓存中的资源；
    - 4XX：Client Error（客户端错误状态码），客户端出现错误，请求失败；
    - 5XX：Server Error（服务端错误状态码），服务端出现错误，请求失败

    **常见状态码**：

    * 100：Continue，表示到目前为止都很正常，客户端可以继续发送请求；
    * 200：OK，请求正确；
    * 301：Moved Permanently，永久性重定向；
    * 302：Found，临时性重定向；
    * 400：Bad Request，请求报文中存在语法错误；
    * 403：Forbidden，请求被拒绝；
    * 404：Not Found；
    * 500：Internal Server Error，服务器正在执行请求时发生错误；

22. **cookie/session 的区别**

    - cooike 数据保存在用户的浏览器上（临时文件夹中），session 数据保存在服务器上；
    - cookie 是以明文的方式存放在客户端的，不是很安全，别人可以通过分析存在在本地的 cookie 来进行 COOKIE 诈骗；
    - cookie 会传递消息给服务器；session 本身存放在服务器中，不会有传送流量；
    - 生命周期：
        - cookie 的生命周期是累加的，从创建时开始计时，20 分钟后生命周期结束
        - session 的生命周期是间隔的，创建后 20 分钟内没有访问 session 就会被销毁；但如果 20 分钟内访问了 session，就又要重新计算 session 的生命周期；
    - session 是一定时间内会存储在服务器中。当访问增多时会增加服务器的性能消耗，此时就可以考虑使用 cookie；
    - cookie 为多个用户浏览器共享，session 为一个用户浏览器独享；

23. **OSI 和 TCP/IP 的网络模型，路由器和交换机位于哪一层**

    **OSI 七层模型**由上到下分别是：**应用层**、**表示层**、**会话层**、**传输层**、**网络层**、**数据链路层**和**物理层**。

    * 物理层：网卡、网线、集线器（采用广播的形式来传输信息）、中继器、调制解调器等
    * 数据链路层：网桥、交换机（用来进行报文交换，能够进行地址学习，采用存储转发的形式来交换报文）等
    * 网络层：路由器（一个作用是连通不同的网络，另一个作用是选择信息传送的线路）
    * 传输层以以上：网关工作

    所以，路由器位于 OSI 七层模型的第三层，网络层；二层交换机位于 OSI 的第二层数据链路层，三层交换机位于 OSI 的第三层网络层，因为其具有路由功能；

    **TCP/IP 四层模型**由上到下分别是：应用层、传输层（TCP 和 UDP 协议）、网络层（整个 TCP/IP 协议栈的核心，定义了 IP 协议）和网络接口层。

24. **IP 地址的分类**

    IP 地址编址方案将IP地址空间划分为 A、B、C、D、E 五类，A、B、C 是基本类，D、E 类作为多播和保留使用，为特殊地址；

    每个 IP 地址包括两个标识码（ID）：网络 ID 和主机 ID。**同一个物理网络下的所有主机都使用同一个网络 ID，而网络上的一个主机（网络工作站、服务器和路由器等）则有一个主机 ID 与其对应**。

    A~E 类地址的特点如下：

    * A 类地址：以 0 开头，第一个字节范围是：0~127
    * B 类地址：以 10 开头，第一个字节范围是：128~191
    * C 类地址：以 110 开头，第一个字节范围是：192~223
    * D 类地址：以 1110 开头，第一个字节范围是：224~239
    * E 类地址：以 1111 开头，保留地址

25. **私有 IP 地址的范围**

    - A 类私有 IP 地址：**10.0.0.0~10.255.255.255**
    - B 类私有 IP 地址：**172.16.0.0~172.31.255.255**
    - C 类私有 IP 地址：**192.168.0.0~192.168.255.255**

26. **为什么有了 MAC 地址还有 IP 地址**

    * 每台主机在出厂时都一个唯一的 MAC 地址，但是 IP 地址的分配是根据网络的拓扑结构，得以保证路由选择方案建立在网络所处的拓扑位置基础而不是设备制造商的基础上
    * 使用 IP 地址更方便传输数据。数据包在这些节点之间的移动都是由 ARP 协议负责将 IP 地址映射到 MAC 地址上来完成的

27. **五层网络协议体系结构的理解和每一层对应的网络协议有哪些**

    * **应用层**的任务是通过应用进程之间的监护来完成特定的网络应用。应用层的协议有域名系统DNS，超文本传输协议 HTTP，文本传输协议 FTP，支持电子邮件的 SMTP 协议，安全外壳协议 SSH 等；
    * **传输层**的主要任务就是负责向两台主机进程之间的通信提供通用的数据传输服务。应用进程利用该服务传送应用层报文。传输层的协议有传输控制协议 TCP 和用户数据报协议 UDP；
    * **网络层**的任务就是选择合适的网间路由和交换结点，确保数据及时传送。在发送数据时，网络层把传输层产生的报文段或用户数据封装成分组和包进行传送。网络层使用IP协议，所以分组也叫 IP 数据报，简称数据报。网络层的协议有网际协议 IP 协议和地址转换协议 ARP 等；
    * **数据链路层**：在两个相邻节点之间传送数据时，数据链路层将网络层传下来的 IP 数据报组装成帧，在两个相邻节点之间的链路上传送帧。帧中包含了数据和必要的控制信息（同步信息，地址信息，差错控制等）。控制信息使接收端能知道一个帧从哪个比特开始和到哪个比特结束，还可以让接收端检测帧中是否有差错，如果有，就丢弃。数据链路层的协议主要有自动重传请求协议 ARQ 和点对点协议 PPP 等；
    * **物理层**：在物理层上所传送的数据单位是比特。它的作用是实现相邻计算机之间比特流的透明传送。

28. **停止等待协议的理解**
    停止等待协议是为了实现可靠传输的，它的基本原理就是每发送完一个分组就停止发送，等待对方确认，收到确认再发送下一个分组；在停止等待协议中，若接收方收到了重复的分组，就丢弃该分组，但同时还要发送确认。主要包括几种情况：无差错情况、超时重传、确认丢失和确认迟到。

29. **ARQ 协议**

    * **自动重传请求 ARQ 协议**：停止等待协议中有一个超时重传的情况，指只要超过一段时间仍然没有收到确认，就会重传前面发送过的分组（默认之前发送的那个分组已经丢失了）。所以，每个发送完一个分组都要设置一个超时计时器，其重传时间会设置得比分组传输的平均往返时间要更长（如果更短，就可能是传输还有到达，不可取）。这种自动重传的方式就叫做**自动重传请求 ARQ**。
    * **连续 ARQ 协议**：连续 ARQ 协议是用来提高信道利用率的。发送方维持一个发送窗口，位于发送窗口内的分组都可以连续发送出去，不需要等待对方确认。而接收方则采用累计确认，对按序到达的最后一个分组发送确认，就能表明这个分组之前的所有分组（包括这个分组）都已经正确收到了。

30. **电路交换和分组交换**

    * **分组交换**：每个分组由首部和尾部组成，包含源地址和目的地址等控制信息，在同一个传输线路上同时传输多个分组是互不影响的，因此**在同一条传输线路上允许同时传输多个分组**。
    * **电路交换**：两个用户之间建立通信前需要有一条专用的物理链路，而且在通信过程中**始终占有该链路**。**电路交换对线路的利用率非常低**。

31. **时延**

    * 排队时延：分组在路由器的输入和输出队列中排队所需要等待的时间，取决于当前网络的通信量；
    * 处理时延：主机或者路由器接收到分组后进行处理所需的时间，处理包括分析首部、从分组中提取数据、进行差错校验等；
    * 传输时延：主机或路由器传输数据帧所需的时间，$delay = \frac{length(bit)}{v(bit/s})$，`length`是数据帧的长度，`v`是传播速率
    * 传播时延：电磁波（光波）在信道中传输所需的时间，$delay = \frac{length(m)}{v(m/s)}$，`length`是信道的长度，`v`是电磁波在信道中的传播速度

32. **URL 和 URI 的区别**

    * **URI**: Uniform Resource Identifier，统一资源标识符
    * **URL**: Uniform Resource Location，统一资源定位符

    通俗地说，URL 是 URI 的子集，URL 只不过是用定位的方式来实现 URI。

    例如，统一资源标识符 URI 就是在某个规则下能够把一个资源独一无二地标识出来，而 URL 就是通过一种方式，例如通过名字的方式来标识出它，URL 是 URI 的一个实例。

33. P2P协议是什么？

    P2P 就是 peer-to-peer。这种方式的特点是，资源一开始并不集中存储在某些设备上，而是分散地存储在多台设备上，这些设备我们称为 peer。

    在下载一个文件时，只要得到那些已经存在了文件的 peer 地址，并和这些 peer 建立点对点的连接，就可以就近下载文件，而不需要到中心服务器上。一旦下载了文件，你的设备也就称为这个网络的一个 peer，你旁边的那些机器也可能会选择从你这里下载文件。

    通过这种方式解决上面 C/S 结构单一服务器带宽压力问题。如果使用过 P2P 软件，例如 BitTorrent，你就会看到自己网络不仅有下载流量，还有上传流量，也就是说你加入了这个 P2P 网络，自己可以从这个网络里下载，同时别人也可以从你这里下载。这样就实现了，下载人数越多，下载速度越快的愿望。

34. 种子文件（.torrent） 是什么？

    .torrent 文件就是我们常说的种子，由 Announce（Tracker URL）和文件信息两部分组成。文件信息里有以下内容：

    * Info 区：指定该种子包含的文件数量、文件大小及目录结构，包括目录名和文件名；
    * Name 字段：指定顶层目录名字；
    * 每个段的大小：BitTorrent（BT）协议把一个文件分成很多个小段，然后分段下载；
    * 段哈希值：将整个种子种，每个段的 SHA-1 哈希值拼在一起。

35. BitTorrent 是怎么样的协议？

    下载时，BT 客户端首先解析 .torrent 文件，得到 Tracker 地址，然后连接 Tracker 服务器。Tracker 服务器回应下载者的请求，将其他下载者（包括发布者）的 IP 提供给下载者。下载者再连接其他下载者，根据 .torrent 文件，两者分别对方自己已经有的块，然后交换对方没有的数据。

    可以看到，下载的过程不需要其他服务器参与，并分散了单个线路上的数据流量，减轻了服务器的压力。下载者每得到一个块，需要算出下载块的 Hash 验证码，并与 .torrent 文件中的进行对比。如果一样，说明块正确，不一样就需要重新下载这个块。这种规定是为了解决下载内容的准确性问题。

    从这个过程也可以看出，这种方式特别依赖 Tracker。Tracker 需要收集所有 peer 的信息，并将从信息提供给下载者，使下载者相互连接，传输数据。虽然下载的过程是非中心化的，但是加入这个 P2P 网络时，需要借助 Tracker 中心服务器，这个服务器用来登记有哪些用户在请求哪些资源。

36. 什么是 Socket 编程？

    Socket 是对 TCP/IP 协议族的一种封装，是应用层与 TCP/IP 协议族通信的中间软件抽象层。从设计模式的角度看来，Socket 其实就是一个门面模式，它把复杂的 TCP/IP 协议族隐藏在 Socket 接口后面，对用户来说，一组简单的接口就是全部，让 Socket 去组织数据，以符合指定的协议。

    所以，应用层与运输层之间通过**套接字**来传递数据，套接字是运输层与应用层的一个中间媒介，位于两层之间。运输层接收到数据后，将它交付给正确的套接字中，应用层从相应进程的套接字获取数据。

37. 应用层、运输层以及网络层的关系

    网络层是五层结构中的第三层，它的作用是在网络中提供**端到端**（即主机之间）的逻辑通信；而运输层是五层结构中的第四层，它的作用是提供**进程之间**的通信；应用层则是最顶层，作用是为用户提供与网络打交道的接口。

38. 什么是**多路复用**和**多路分解**？

    **多路复用**：在数据的发送端，传输层收集各个套接字中需要发送的数据，将它们封装到首部的信息后，交个网络层；

    **多路分解**：在数据的接收端，传输层接收到网络层的报文后，将它交付到正确的套接字上；| 在运输层报文段中的数据交付到正确的的套接字。