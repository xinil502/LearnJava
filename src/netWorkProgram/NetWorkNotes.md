# 网络编程
## 一、网络编程基础知识
### 1.软件结构
* **C/S结构**：全称为Client/Server结构，是指客户端和服务器结构，如QQ,钉钉等。
通过客户端访问服务器。

* **B/S结构**: 全称为Browser/Server结构，是指浏览器和服务器结构，如火狐浏览器，谷歌浏览器。

无论哪种架构，都离不开网络的支持，网络编程，就是在一定的协议下，实现两台计算机通信的程序。
### 2.网络通信协议
* **网络通信协议** :通过计算机网络可以使多台计算机实现连接，位于同一网络中的计算机在连接和通信时需要遵守一定的规则，它对数据的传输格式，传输速率，传输步骤做了统一规定，双方必须同时遵守才能完成数据交换。
* **TCP/IP协议** :传输控制协议/因特网互联协议，是Internet最基本最广泛的协议，它定义了计算机如何连入因特网，以及数据如何在他们之间传输的标准，它的内部包含一系列用于处理数据通信的协议，并采用了四层的分层模型，每一层都呼叫下一层所提供的协议来完成自己的需求。

**数据链路层和物理层**：由底层网络定义的协议。(定义物理传输通道，光纤，网线提供的驱动)

**网络层**：ICMP,IGMP IP ARP,RARP（TCP/IP核心，主要用于将传输的数据进行分组，将分组数据发送给目标计算机）

**传输层**：TCP,UDP (使网络程序进行通信，通信时采用可以使用TCP和UDP协议)

**应用层**：HTTP,FTP,TFTP,SMTP,SNMP,DNS(负责应用程序的协议)
### 3.协议分类
* UDP: 用户数据报协议(User Datagram Protocol)。UDP是无连接通信协议,即在数据传输时,数据的发送端
和接收端不建立逻辑连接。简单来说，当-台计算机向另外一台计算机发送数据时,发送端不会确认接收端是
否存在,就会发出数据，同样接收端在收到数据时,也不会向发送端反馈是否收到数据。
由于使用UDP协议消耗资源小,通信效率高,所以通常都会用于音频、视频和普通数据的传输例如视频会议都
使用UDP协议。因为这种情况即使偶尔丢失-两个数据包 ,也不会对接收结果产生太大影响。
但是在使用UDP协议传送数据时,由于UDP的面向无连接性,不能保证数据的完整性,因此在传输重要数据时
不建议使用UDP协议。

特点:数据被限制在64kb以内,超出这个范围就不能发送了。
* **TCP**:传输控制协议(Transmission Control Protocol)。 TCP协议是**面向连接*的通信协议,即传输数据之
         前，在发送端和接收端建立逻辑连接,然后再传输数据,它提供了两台计算机之间可靠无差错的数据传输。
         在TCP连接中必须要明确客户端与服务器端,由客户端向服务端发出连接请求,每次连接的创建都需要经过“三
         次握手"。
         **三次握手**: TCP协议中,在发送数据的准备阶段,客户端与服务器之间的三次交互,以保证连接的可靠。
         ■第一次握手，客户端向服务器端发出连接请求,等待服务器确认。
         ■第二次握手，服务器端向客户端回送一 个响应,通知客户端收到了连接请求。
         ■第三次握手，客户端再次向服务器端发送确认信息，确认连接。
         完成三次握手,连接建立后,客户端和服务器就可以开始进行数据传输了。由于这种面向连接的特性. TCP协议
         可以保证传输数据的安全,所以应用十分广泛,例如下载文件、浏览网页等。I
### 4.网络编程三要素
#### 1）.协议
#### 2）.IP地址

指互联网协议地址( Internet Protocol Address) 一个计算机设备在网络中，对应的唯一编号。

**IP地址分类：**

* 1.**IPV4**:是-个32位的二进制数,通常被分为4个字节,表示成a.b.c.d的形式，例如"192,168,65,100”，其中a、b. C、d都是0~255之间的十进制整数,那么最多可以表示42亿个。
            
* 2.**IPV6**:采用128位地址长度 .每16个字节一组。分成8组十六进制数,表示成ABCD:EF01:2345:6789:ABCD:EF01:2345:6789，号称可以为全世界的每一粒沙子编上一个网址,这样就解决了网络地址资源数量不够的问题。
            
**常用命令：**

* `ipconfig` 查看本地ip地址。

* `ping ip地址` 检查网络是否连通，如果通了，说明我与该ip地址可以发送文件。

**特殊ip地址：**
* 本地ip地址：`127.0.0.1` 或 `localhost1`

#### 3）.端口号
IP连接了计算机，但是数据无法准确的发送到软件上，这个时候就需要端口号
瑞口号是一个逻辑端口，我们无法直接看到。可以使用一些软件查看端口号。
端口号是由两个字节组成取值范围在0-65535之间。

**端口号获取方法：**
* 1.网络软件在打开的时候和系统要指定的端口号，
* 2.当我们使用网络软件- 打开,那么操作系统就会为网络软件分配- 个随机的端口号

**注意:**
* 1024之前的端口号我们不能使用。已经被系统分配给已知的网络软件了

* 网络软件的端口号不能重复

根据IP地址和端口号就可以准确无误的发送到指定软件上。如：192.168.1.200.5000

**常用的端口号：**
* 1.80端口 网络端口 输入网址时，后面默认加80，手动改为其他会打不开。如：www.bilibili.com:80
* 2.数据库 mysql:3306 oracle:1521
* 3.Tomcat服务器 :8080

## 第二章 TCP通信程序
### 1.概述
TCP通信能实现两台计算机之间的数据交互,通信的两端,要严格区分为客户端( Client)与服务端( Server )。
面向连接的通信，客户端和服务端必须经过三次握手建立连接。

**两端通信时步骤：**
* 1.服务器端,需要事先启动,等待客户端的连接，服务端不可以主动连接客户端。

* 2.客户端主动连接服务器端,客户端与服务端之间会建立一个逻辑链接。

* 3.连接中包含着一个对象，这个对象就是IO对象，客户端和服务端可以使用IO对象进行通信，

* 4.通信不仅仅是字符，所以IO对象是字节流。

**两个用于实现TCP的类：**
* 1.客户端:IP:端口号 java.net.Socket 类表示。创建Socket对象,向服务端发出连接请求,服务端响应请求,两者建立连接开始通信。
* 2.服务端:IP:端口号 java.net.ServerSocket类表示。创建ServerSocket对象,相当于开启一个服务,并等待客户端的连接。

**服务器必须明确两件事：**
* 1.多个客户端同时和服务器进行交互,服务器必须明确和哪个客户端进行的交互，在服务器端有一个方法Accept,获取到请求的客户端对象`Socke a1 = Socke.accept()`.
* 2.多个客户端同时和服务器进行交互，需要使用多个IO流对象。服务器是没有IO流的，但是可以获取请求的客户端对象Socket，使用每个客户端Socket中提供的IO流和客户端交互。服务端使用客户端的字节输入流读取客户端发送的数据，服务端使用客户端的字节输出流给客户端回写数据。

### 2.Socke类
```java
/**
 * TCP通信的客户端实现
 *
 * 向服务器发送请求，给服务器发送数据，读取服务器回写的数据
 *
 * 表示客户端的类：java.net.Socket
 *          此类实现客户端套接字，套接字是包含IP地址和端口号的网络单位。
 *
 * 构造方法：Socket(String host, int port)创建一个流套接字，并将其连接到指定主机上的指定端口号。
 *          参数：
 *              String host: 服务器主机的名称/服务器的IP地址。
 *              int post: 服务器的端口号。
 * 成员方法：
 *          OutputStream getOutputStream()  返回此套接字的输出流。
 *          InputStream getInputStream()   返回此套接字的输入流。
 *          void close()  关闭此套接字。
 *
 * 实现步骤：
 *          1.创建一个客户端对象Socket, 构造方法绑定服务器的IP地址和端口号
 *          2.使用Socket对象中的getOutputStream()获取网络字节输出流对象OutputStream(不是自己创建的，是通过SOcket获取的)
 *          3.使用网络字节输出流对象OutputStream对象中的write方法，给服务器发送数据。
 *          4.使用Socket对象中的getInputStream()获取网络字节输入流对象InputStream(不是自己创建的，是通过SOcket获取的)
 *          5.使用网络字节输出流对象InputStream对象中的read方法，接受服务器回写的数据。
 *          6.释放资源(Socket)
 *
 * 注意事项：
 *          1.客户端和服务器端进行交互，必须使用Socket中提供的网络流，不能使用自己创建的流对象。
 *          2.当我们创建客户端对象Socket的时候，就会去请求服务器进行三次握手建立连接通路。
 *            这是如果服务器没有启动，就会抛出异常，
 *            如果服务器已经启动，那么就可以进行交互了。
 */

public class NetWork_Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("127.0.0.1", 8765);
        OutputStream os = socket.getOutputStream();
       //发送至服务器
        os.write("你好服务器".getBytes());

        InputStream is = socket.getInputStream();
        byte[] b = new byte[1024];
        int len;

        //读取服务器回写数据
        len = is.read(b);
        System.out.println(new String(b, 0, len));

        socket.close();
    }
}

```

```java

/**
 * TCP通信的服务器端
 *
 * 接收客户端的请求，读取客户端发送的数据，给客户端回写数据
 *
 * 表示服务器的类：
 *              java.net.ServerSocket: 此类实现服务器套接字
 *
 * 构造方法：
 *              ServerSocket(int port) 创建绑定到特定端口的服务器套接字。
 *
 * 服务器必须明确一件事情，是那个客户端请求的服务器，
 * 所以可以使用accept方法，获取到请求的客户端对象Socket
 * 成员方法：
 *              Socket accept() 侦听并接受到此套接字的连接。
 *
 * 服务器的实现步骤：
 *              1.创建服务器ServerSocket对象，和系统要指定的端口号。
 *              2.使用ServerSocket对象中的accept方法，获取到请求的客户端对象Socket
 *              3.使用Socket对象中的getInputStream()获取网络字节输入流对象InputStream
 *              4.使用网络字节输入流对象InputStream中的read方法，读取客户端发送的数据。
 *              5.使用Socket对象中的getOutputStream()获取网络字节输出流对象OutputStream。
 *              6.使用网络字节输出流对象OutputStream对象中的write方法，给客户端回写数据。
 *              7.释放资源(Socket, ServerSocket)
 */

public class NetWork_Server {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(8765); //问系统要固定的端口号
        Socket socket = ss.accept();  //获取请求的客户端Socket对象
        InputStream is = socket.getInputStream();

        //读取客户端数据
        byte[] b = new byte[1024];
        int len;

        len = is.read(b);
        System.out.println(new String(b, 0, len));

        //给客户端回写数据
        OutputStream os = socket.getOutputStream();
        os.write("已收到".getBytes());

        socket.close();
        ss.close();
    }
}

```