
234
235     // return minimum size of Square
236     public Dimension getMinimumSize()
237     {
238         return getPreferredSize(); // return preferred size
239     } // end method getMinimumSize
240
241     // set mark for Square
242     public void setMark( String newMark )
243     {
244         mark = newMark; // set mark of square
245         repaint(); // repaint square
246     } // end method setMark
247
248     // return Square location
249     public int getSquareLocation()
250     {
251         return location; // return location of square
252     } // end method getSquareLocation
253
254     // draw Square
255     public void paintComponent( Graphics g )
256     {
257         super.paintComponent( g );
258
259         g.drawRect( 0, 0, 29, 29 ); // draw square
260         g.drawString( mark, 11, 20 ); // draw mark
261     } // end method paintComponent
262     } // end inner-class Square
263 } // end class TicTacToeClient

图27.15 | 客户端/服务器Tic-Tac-Toe程序的客户端部分（第6部分，共6部分）

1   // Fig. 27.16: TicTacToeClientTest.java
2   // Test class for Tic-Tac-Toe client.
3   import javax.swing.JFrame;
4
5   public class TicTacToeClientTest
6   {
7       public static void main( String[] args )
8       {
9           TicTacToeClient application; // declare client application
10
11          // if no command line args
12          if ( args.length == 0 )
13              application = new TicTacToeClient( "127.0.0.1" ); // localhost
14          else
15              application = new TicTacToeClient( args[ 0 ] ); // use args
16
17          application.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
18      } // end main
19   } // end class TicTacToeClientTest

图27.16 | Tic-Tac-Toe客户端的测试类

如果收到的消息是 "Valid move."，第134–135行会显示消息 "Valid move, please wait."，并调用 setMark 方法（第173–184行）来在当前方格（用户单击的那个方格）中设置客户端的标记，同时使用 SwingUtilities 的 invokeLater 方法以确保 GUI 更新在事件分发线程中进行。如果收到的消息是 "Invalid move, try again."，第139行会显示该消息，以便用户单击另一个方格。如果收到的消息是 "Opponent moved."，第144行从服务器读取一个整数，指示对手移动的位置，第149–150行在棋盘的该方格中放置一个标记（同样使用 SwingUtilities 的 invokeLater 方法以确保 GUI 更新在事件分发线程中进行）。如果收到任何其他消息，第155行仅显示该消息。

a) 玩家X已连接到服务器。

![](img/009e962758dcc71dbc43a493362e6dc0_1201_0.png)

b) 玩家O已连接到服务器。

![](img/009e962758dcc71dbc43a493362e6dc0_1201_1.png)

c) 玩家X走了一步。

![](img/009e962758dcc71dbc43a493362e6dc0_1201_2.png)

d) 玩家O看到了玩家X的走法。

![](img/009e962758dcc71dbc43a493362e6dc0_1201_3.png)

e) 玩家O走了一步。

![](img/009e962758dcc71dbc43a493362e6dc0_1201_4.png)

f) 玩家X看到了玩家O的走法。

![](img/009e962758dcc71dbc43a493362e6dc0_1201_5.png)

g) 玩家X走了一步。

h) 玩家O看到了玩家X的最后一步。

![](img/009e962758dcc71dbc43a493362e6dc0_1202_0.png)

![](img/009e962758dcc71dbc43a493362e6dc0_1202_1.png)

图27.17 | 客户端/服务器Tic-Tac-Toe程序的示例输出（第2部分，共2部分）

## 27.9 [网络附加]案例研究：DeitelMessenger

本案例研究可在 www.deitel.com/books/jhtp9/ 获取。聊天室提供了一个中心位置，用户可以通过短文本消息相互聊天。每个参与者都能看到其他用户发布的所有消息，并且每个用户都可以发布消息。本案例研究整合了你迄今学到的许多 Java 网络、多线程和 Swing GUI 特性，以构建一个在线聊天系统。我们还介绍了多播（multicasting），它使应用程序能够向客户端组发送 DatagramPacket。

DeitelMessenger 案例研究是一个重要的应用程序，它使用了许多中级 Java 特性，例如使用 Socket、DatagramPacket 和 MulticastSocket 进行网络通信、多线程以及 Swing GUI。该案例研究还通过将接口与实现分离，并使开发人员能够支持不同的网络协议和提供不同的用户界面，展示了良好的软件工程实践。读完本案例研究后，你将能够构建更重要的网络应用程序。

## 27.10 总结

在本章中，你学习了 Java 网络编程的基础知识。我们从简单的 applet 和应用程序开始，其中 Java 为你执行网络通信。然后你学习了通过网络发送数据的两种不同方法——使用 TCP/IP 的基于流的网络通信和使用 UDP 的基于数据报的网络通信。我们展示了如何使用基于流和基于数据报的网络通信构建简单的客户端/服务器聊天程序。接着你看到了一个客户端/服务器Tic-Tac-Toe游戏，它使两个客户端能够通过与维护游戏状态和逻辑的多线程服务器交互来进行游戏。在下一章中，你将学习基本的数据库概念、如何使用 SQL 与数据库中的数据交互，以及如何使用 JDBC 让 Java 应用程序操作数据库数据。

## 小结

### 27.1 引言

- Java 提供了流套接字和数据报套接字（p. 1119）。使用流套接字（p. 1119）时，一个进程与另一个进程建立连接（p. 1119）。在连接存在期间，数据以流的形式在进程之间流动。流套接字被认为提供面向连接的服务（p. 1119）。用于传输的协议是流行的 TCP（传输控制协议；p. 1119）。

- 使用数据报套接字（datagram socket）时，信息以独立的数据包进行传输。UDP（用户数据报协议；p. 1119）是一种无连接服务，它不保证数据包不会丢失、重复或乱序到达。

### 27.2 操作 URL

- HTTP 协议（p. 1120）使用 URI（p. 1120）在 Internet 上定位数据。常见的 URI 表示文件或目录，也可以表示复杂任务，例如数据库查找和 Internet 搜索。表示网站或网页的 URI 称为 URL（p. 1120）。

- Applet 的 getAppletContext 方法（p. 1124）返回一个 AppletContext（p. 1120），它表示正在执行该 applet 的浏览器。AppletContext 的 showDocument 方法（p. 1120）接收一个 URL，并将其传递给 AppletContext，后者显示相应的 Web 资源。showDocument 的另一个版本允许 applet 指定目标框架（p. 1124），在其中显示 Web 资源。

### 27.3 在 Web 服务器上读取文件

- JEditorPane（p. 1125）的 setPage 方法（p. 1127）下载其参数指定的文档并显示它。

- 通常，HTML 文档包含指向 Web 上其他文档的超链接。如果 HTML 文档显示在不可编辑的 JEditorPane 中，并且用户单击超链接（p. 1127），则会发生 HyperlinkEvent（p. 1125），并通知 HyperlinkListeners。

- HyperlinkEvent 的 getEventType 方法（p. 1127）确定事件类型。HyperlinkEvent 包含嵌套类 EventType（p. 1127），它声明了事件类型 ACTIVATED、ENTERED 和 EXITED。HyperlinkEvent 的 getURL 方法（p. 1127）获取超链接所表示的 URL。

### 27.4 使用流套接字建立简单服务器

- 基于流的连接（p. 1119）使用 Socket 对象（p. 1128）进行管理。ServerSocket 对象（p. 1128）建立端口（p. 1128），服务器（p. 1119）在该端口等待来自客户端（p. 1119）的连接。ServerSocket 的 accept 方法（p. 1128）无限期地等待客户端连接，并在建立连接时返回一个 Socket 对象。

- Socket 的 getOutputStream 和 getInputStream 方法（p. 1129）分别获取 Socket 的 OutputStream 和 InputStream 的引用。close 方法（p. 1129）终止连接。

### 27.5 使用流套接字建立简单客户端

- 创建 Socket 对象时指定服务器名称和端口号（p. 1128），以便将客户端连接到服务器。连接尝试失败会抛出 IOException。

- InetAddress 的 getByName 方法（p. 1142）返回一个 InetAddress 对象（p. 1136），其中包含指定计算机的 IP 地址。InetAddress 的 getLocalHost 方法（p. 1142）返回一个 InetAddress 对象，其中包含执行程序的本地计算机的 IP 地址。

### 27.7 数据报：无连接客户端/服务器交互

- 面向连接的传输就像电话系统——你拨号，并与想要通话之人的电话建立连接。连接在你通话期间保持，即使你没有说话也是如此。

- 使用数据报的无连接传输（p. 1142）类似于通过邮政服务寄送的邮件。一个无法装入单个信封的大消息可以被拆分为独立的消息片段，这些片段被放入独立的、按顺序编号的信封中。然后所有信件同时寄出。它们可能按顺序到达、乱序到达，或者根本不到达。
