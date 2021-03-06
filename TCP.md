# <center>三次握手</center>

>请求端（通常称之为客户）发送一个SYN段指明客户打算连接的服务器的端口，以及初始序号（ISN），这个SYN段为报文段1</br>
>
>服务端发回包含服务器的初始序号的SYN报文段（报文段2）作为应答，同时，将确认序号设置为客户的ISN加1以对客户的SYN，报文进行确认（ACK）。一个SYN将占用一个序号</br>

>客户必须将确认序号设置为服务器的ISN加1以对服务器的SYN报文段进行确认（ACK）

# <center>四次挥手</center>

>建立一个连接需要三次握手，而终止一个连接需要经过4次握手。这由TCP的半关闭（half-close）造成的。既然一个TCP连接是全双工，
因此每个方向必须单独地进行关闭。

>客户断开连接时候向服务端发送一个FIN，服务端收到后发回一个ACK，确认序号为收到序号+1；
>
>服务端断开连接时候向客户发送一个FIN，客户收到后发送一个ACK，确认序号为收到序号+1；


#<center>为什么TCP是可靠的</center>
>1.应用数据被分割成TCP认为最合适发送的数据块。这和UDP完全不同，应用程序产生的数据报长度将保持不变。由TCP传递给IP的信息单位称为报文段或者段。

>2.当TCP发出一个段后，它启动一个定时器，等待目的端确认收到这个报文段。如果不能及时收到一个确认，将重发这个报文段。

>3.当TCP收到发自TCP连接另一端的数据，它将发送一个确认。这个确认不是立即发送，通常推迟几分之一秒

>4.TCP将保持它首部和数据的检验和。这是一个端到端的检验和，目的是检验数据在传输过程中的任何变化。如果收到段的检验和有差错，TCP将丢弃这个报文段和不确认收到此报文段。

>5.既然TCP报文段作为IP数据报来传输，而IP数据报的到达可能失序，因此TCP报文段的到达也可能失序。如果必要，TCP将对收到的数据进行重新排序，将收到的数据以正确的顺序交给应用层

>6.既然IP数据报会发送重复，TCP的接收端必须丢弃重复的数据。

>7.TCP还能控制流量控制。TCP连接的每一方都有固定大小的缓冲空间。TCP的接收端只允许另一端发送接收端缓冲区所能接纳的数据。这将防止较快主机致使较慢主机的缓冲区溢出

#<center>TCP 和 UDP 的区别</center>
>TCP是面向连接，而UDP是无连接的，即UDP在发送之前不需要建立连接
>
>TCP提供可靠的服务。也就是说，通过TCP连接传送的数据保证了数据无差错，不丢失，不重复，且按序到达，而UDP只是尽最大的努力交付，不保证可靠交付
>
>TCP面向字节流，实际上TCP是把数据看成一连串无结构的字节流，UDP是面向报文的，UDP没有拥塞控制，因此网络出现拥塞不会使源主机降低发送速率（实际应用场景：IP电话，实时视频会议）

>每条TCP连接只能是点到点的；UDP支持一对一，一对多，多对一，多对多的交互通信

>TCP首部的开销20字节，UDP仅需要8个字节

>TCP的逻辑通信信道是全双工的可靠信道，UDP则是不可靠信道

>UDP的应用场景：面向数据报方式，网络数据大多为短消息，拥有大量client，对数据安全性无特殊要求，网络负担非常重，但对相应<h3>速度要求高</h3>