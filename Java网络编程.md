

## 网络编程

### 1.1 概述

#### 计算机网络：

计算机网络是指将**地理位置不同**的具有独立功能的多台计算机及其外部设备，通过通信线路连接起来，在网络操作系统，网络管理软件及**网络通信协议**的管理和协调下，**实现资源共享和信息传递**的计算机系统

##### 网络编程的目的：

传播交流信息，数据交换，通信

##### 要求：

1.如何准确的定位网络上的一台主机    IP地址+端口

2.找到主机，如何进行数据传输？



javaweb是指网页编程

网络编程主要是指TCP/IP等



### 1.2 网络通信的要素

如何实现网络通信？

**通信双方地址：**

ip、端口、



TCP/IP参考模型：

![image-20200503190321891](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200503190321891.png)



**小结**

> 1.网络编程中的两个主要问题
>
> ​	如何准确的定位到网络上的一台或多台主机
>
> ​	找到主机后如何进行通信
>
> 2.网络编程中的要素
>
> ​	IP、端口号
>
> ​	网络通信协议 UDP/TCP



### 1.3 IP

IP地址：Java对应的包（InetAddress）

几个注意的点：

- 唯一定位一台网络上计算机

- 127.0.0.1：本机localhost

- ip地址的分类

    - ipv4/ipv6

        - **IPV4**127.0.0.1     4个字节组成。0~255，约有42亿个IP
        - **IPV6** fe80::b5f0:9e00:b642:7d99%14   128位。8个无符号整数

    - 公网（互联网）--私网（局域网）

        - ABCDE类IP地址
            - IP地址根据网络号和主机号来分，分为A、B、C三类及特殊地址D、E。  全0和全1的都保留不用。
            - A类：(1.0.0.0-126.0.0.0)（默认子网掩码：255.0.0.0或 0xFF000000）第一个字节为网络号，后三个字节为主机号。该类IP地址的最前面为“0”，所以地址的网络号取值于1~126之间。一般用于大型网络。
            - B类：(128.0.0.0-191.255.0.0)（默认子网掩码：255.255.0.0或0xFFFF0000）前两个字节为网络号，后两个字节为主机号。该类IP地址的最前面为“10”，所以地址的网络号取值于128~191之间。一般用于中等规模网络。
            - C类：(192.0.0.0-223.255.255.0)（子网掩码：255.255.255.0或 0xFFFFFF00）前三个字节为网络号，最后一个字节为主机号。该类IP地址的最前面为“110”，所以地址的网络号取值于192~223之间。一般用于小型网络。
            - D类：是多播地址。该类IP地址的最前面为“1110”，所以地址的网络号取值于224~239之间。一般用于多路广播用户[1] 。
            - E类：是保留地址。该类IP地址的最前面为“1111”，所以地址的网络号取值于240~255之间。
            - ![image-20200504164641924](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200504164641924.png)

        - 192.168.xx.xx     专门给组织内部使用的
        - 域名：记忆IP问题

### 1.4 端口

端口表示计算机上一个程序的进程；

- 不同的进程有不同的端口号，用来区分软件
- 被规定 0~65535
- TCP，UDP：65535*2     单个协议下，端口号不能冲突
- 端口分类
    - 共有端口 0~1023
        - HTTP：80
        - HTTPS：443
        - FTP：21
        - Telent：23
        
    - 程序注册端口：1024~49151,分配用户或者程序
        - Tomcat：8080
        - MySql：3306
        - Oracle：1521
        
    - 动态、私有：49152~65535
    
        ```bash
        netstat -ano #查找所有的端口
        netstat -ano|findstr "端口号" #查看指定端口
        ```

### 1.5 通信协议

**网络通信协议**：速率、传输码率、代码结构、传输控制等等

问题：过于复杂

解决方案：分层

**TCP/IP协议簇**：实际是一组协议

- TCP：用户传输协议
- UDP：用户数据报协议

出名的协议：

- TCP
- IP：网络互连协议

**TCP和UDP对比**

- TCP：类比于打电话

    - 连接、稳定

    - 三次握手、四次挥手

        ```
        最少需要三次，建立稳定连接
        A:你瞅啥?
        B:瞅你咋地
        A:干一场
        
        最少需要四次断开连接：
        A:我要断开了
        B:你真的要断开了吗？
        B:你真的真的要断开了吗？
        A:我真的断开了
        ```

        ![image-20200504174736606](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200504174736606.png)

        ![image-20200504175018276](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200504175018276.png)

    - 客户端、服务端

    - 传输完成、释放连接、效率低

- UDP：类比于发短信

    - 不连接、不稳定
    - 客户端、服务端：没有明确的界限
    - 不管有没有准备好，都可以发给你

### 1.6 Java模拟TCP

需要客户端和服务端

**客户端**

1. 连接服务器Socket
2. 发送消息

**服务端**

1. 建立服务端口  ServerSocket
2. 等待用户的连接  accept
3. 接收消息

#### 模拟文件上传

**客户端**

```java
package internetwork;

import java.io.*;
import java.net.InetAddress;
import java.net.Socket;

/**
 * @author 10483
 * 客户端
 */
public class TcpClientDemo2 {
    public static void main(String[] args) throws IOException {
        //1.创建一个Socket连接
        Socket socket = new Socket(InetAddress.getByName("127.0.0.1"),9500);
        //2.创建一个输出流
        OutputStream os = socket.getOutputStream();
        //3.读取文件
        FileInputStream fis = new FileInputStream(new File("5.jpg"));
        //4.写出文件
        byte[] buffer = new byte[1024];
        int len;
        while ((len = fis.read(buffer)) != -1){
            os.write(buffer,0,len);
        }

        //通知服务器，已经传输信息完毕
        socket.shutdownOutput();

        //确定服务器接收完毕，断开连接
        InputStream is = socket.getInputStream();
        //用管道流来接收
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        byte[] buffer2 = new byte[1024];
        int len2;
        while((len2 = is.read(buffer2)) != -1){
            baos.write(buffer2,0,len2);
        }
        System.out.println(baos.toString());

        //5.关闭资源
        baos.close();
        is.close();
        fis.close();
        os.close();
        socket.close();
    }
}
```

**服务端**

```java
package internetwork;

import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

/**
 * @author 10483
 */
public class TcpServerDemo2 {
    public static void main(String[] args) throws IOException {
        //1.建立一个地址
        ServerSocket serverSocket = new ServerSocket(9500);
        //2.等待用户连接   阻塞式监听，会一直等待客户端连接
        Socket socket = serverSocket.accept();
        //3.接收消息
        InputStream is = socket.getInputStream();
        //4.文件输出
            //用管道输出流来进行输出
        FileOutputStream fos = new FileOutputStream(new File("receive.jpg"));

        byte[] buffer = new byte[1024];
        int len;
        while ((len = is.read(buffer)) != -1){
            fos.write(buffer,0,len);
        }

        //通知客户端消息接收完毕
        OutputStream os = socket.getOutputStream();
        os.write("消息接收完毕，可以关闭连接".getBytes());

        //5.关闭连接
        os.close();
        fos.close();
        is.close();
        socket.close();
        serverSocket.close();
    }
}
```



#### 初始Tomcat

B/S模式

服务端

- 自定义   S
- Tomcat服务器      S

客户端

- 自定义   C
- 浏览器   B

### 1.7 UDP传输

发送消息，无所谓服务器和客户端，双方均可发送与接收消息

#### **发送端**

```java
package internetwork;

import java.io.IOException;
import java.net.*;

/**
 * @author 10483
 * 模拟UDP通信，不需要建立连接（类比发短信）
 */
public class UdpClientDemo1 {
    public static void main(String[] args) throws IOException {
        //1.建立一个socket
        DatagramSocket socket = new DatagramSocket();
        //2.建立一个要发送的数据包
        String msg = "Hello UDP!!";
        InetAddress address = InetAddress.getByName("127.0.0.1");
        int port = 9300;
        //数据包，包含数据，发送出去的地址和端口等信息
        DatagramPacket packet = new DatagramPacket(msg.getBytes(),0,msg.getBytes().length,address,port);

        //3.发送消息
        socket.send(packet);

        //关闭流
        socket.close();
    }
}
```

#### **接收消息端**

```java
package internetwork;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;

/**
 * @author 10483
 * 接收消息
 */
public class UdpServerDemo1 {
    public static void main(String[] args) throws IOException {
        //1.需要开放端口，才可能接收到消息
        DatagramSocket socket = new DatagramSocket(9300);
        //2.接收数据包
        byte[] buffer = new byte[1024];
        DatagramPacket packet = new DatagramPacket(buffer, 0, buffer.length);
        socket.receive(packet);

        System.out.println(packet.getAddress().getHostAddress());
        System.out.println(new String(packet.getData(),0,packet.getLength()));
        //关闭流
        socket.close();
    }
}
```

#### 模拟聊天

##### 单方面发送消息

发送消息

```java
package internetwork;


import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

/**
 * @author 10483
 * 模拟聊天  发送消息方
 */
public class UdpSenderDemo {
    public static void main(String[] args) throws IOException {
        //1.建立一个端口
        DatagramSocket socket = new DatagramSocket(8888);

        //2.准备数据，从控制台输入信息System.in
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

        //加入while循环发送消息
        while (true){
            //读取数据
            String data = bufferedReader.readLine();
            //将数据转换为字节流
            byte[] buffer = data.getBytes();
            DatagramPacket packet = new DatagramPacket(buffer,0,buffer.length, InetAddress.getByName("localhost"),6666);

            //3.发送数据
            socket.send(packet);

            //发送消息结束
            if(data.trim().equals("bye")){
                break;
            }
        }
        //4.关闭流
        socket.close();
    }
}
```

接收消息

```java
package internetwork;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;

/**
 * @author 10483
 * 接收消息方
 */
public class UdpReceiverDemo {
    public static void main(String[] args) throws IOException {
        //1.建立端口
        DatagramSocket socket = new DatagramSocket(6666);

        //加while循环持续接收信息
        while (true){
            //2.准备接收数据
            byte[] container = new byte[1024];
            DatagramPacket packet = new DatagramPacket(container,0,container.length);

            //阻塞式接收消息
            socket.receive(packet);

            String receiveData = new String(packet.getData(), 0, packet.getLength());
            System.out.println(receiveData);

            //断开与另一方的连接
            if(receiveData.trim().equals("bye")){
                break;
            }
        }

        //关闭连接
        socket.close();
    }
}
```

##### 双方在线同时聊天(模拟老师学生聊天)

> 利用多线程

**发送消息类**

```java
package internetwork.Chat;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.*;

/**
 * @author 10483
 * 模拟双方在线聊天
 */
public class ChatSender implements Runnable{
    DatagramSocket socket = null;
    BufferedReader bufferedReader = null;
    private String toIP;
    private int fromPort;
    private int toPort;

    public ChatSender(String toIP, int fromPort, int toPort) {
        this.toIP = toIP;
        this.fromPort = fromPort;
        this.toPort = toPort;
        try {
            //1.建立一个端口
            socket = new DatagramSocket(fromPort);
            //2.准备数据，从控制台输入信息System.in
            bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        } catch (SocketException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void run() {
        //加入while循环发送消息
        while (true){
            //读取数据
            String data = null;
            try {
                data = bufferedReader.readLine();
            } catch (IOException e) {
                e.printStackTrace();
            }
            //将数据转换为字节流
            byte[] buffer = data.getBytes();
            DatagramPacket packet = new DatagramPacket(buffer,0,buffer.length,new InetSocketAddress(this.toIP,this.toPort));

            //3.发送数据
            try {
                socket.send(packet);
            } catch (IOException e) {
                e.printStackTrace();
            }

            //发送消息结束
            if(data.trim().equals("bye")){
                break;
            }
        }
        //4.关闭流
        socket.close();
    }
}
```

**接收消息类**

```java
package internetwork.Chat;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketException;

/**
 * @author 10483
 * 双方通信，接收消息
 */
public class ChatReceive implements Runnable{
    DatagramSocket socket = null;
    private int port;
    private String msgFrom;
    public ChatReceive(int port,String msgFrom) {
        this.port = port;
        this.msgFrom = msgFrom;
        try {
            //1.建立端口
            socket = new DatagramSocket(port);
        } catch (SocketException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void run() {
        //加while循环持续接收信息
        while (true){
            //2.准备接收数据
            byte[] container = new byte[1024];
            DatagramPacket packet = new DatagramPacket(container,0,container.length);

            //阻塞式接收消息
            try {
                socket.receive(packet);
            } catch (IOException e) {
                e.printStackTrace();
            }

            String receiveData = new String(packet.getData(), 0, packet.getLength());
            System.out.println(msgFrom+receiveData);

            //断开与另一方的连接
            if(receiveData.trim().equals("bye")){
                break;
            }
        }

        //关闭连接
        socket.close();
    }
}
```

**学生实例化**

```java
package internetwork.Chat;

public class ChatStudent {
    public static void main(String[] args) {
        new Thread(new ChatSender("localhost",5000,8000)).start();
        new Thread(new ChatReceive(6000,"老师：")).start();
    }
}
```



**老师实例化**

```java
package internetwork.Chat;

public class ChatTeacher {
    public static void main(String[] args) {
        new Thread(new ChatSender("localhost",7000,6000)).start();
        new Thread(new ChatReceive(8000,"学生：")).start();
    }
}
```

### 1.8 URL

https://www.baidu.com/

URL：统一资源定位器，定位互联网上的某一资源

DNS域名解析：将域名解析为IP地址。例如www.baidu.com   --->  145.xx.xx.xx

```
URL组成部分
[协议]：//[IP地址]:[端口]/[项目名]/[对应资源]
```

