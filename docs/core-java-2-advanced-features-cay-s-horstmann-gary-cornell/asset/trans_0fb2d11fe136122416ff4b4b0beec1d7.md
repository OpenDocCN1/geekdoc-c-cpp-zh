
## 代码清单 4.5

```java
blockingButton.addActionListener(event ->
{
    interruptibleButton.setEnabled(false);
    blockingButton.setEnabled(false);
    cancelButton.setEnabled(true);
    connectThread = new Thread(() ->
    {
        try
        {
            connectBlocking();
        }
        catch (IOException e)
        {
            messages.append("\nInterruptibleSocketTest.connectBlocking: " + e);
        }
    });
    connectThread.start();
});

cancelButton = new JButton("Cancel");
cancelButton.setEnabled(false);
northPanel.add(cancelButton);
cancelButton.addActionListener(event ->
{
    connectThread.interrupt();
    cancelButton.setEnabled(false);
});
server = new TestServer();
new Thread(server).start();
pack();
}

/**
 * Connects to the test server, using interruptible I/O.
 */
public void connectInterruptibly() throws IOException
{
    messages.append("Interruptible:\n");
    try (SocketChannel channel = SocketChannel.open(new InetSocketAddress("localhost", 8189)))
    {
        in = new Scanner(channel, "UTF-8");
        while (!Thread.currentThread().isInterrupted())
        {
            messages.append("Reading ");
            if (in.hasNextLine())
            {
                String line = in.nextLine();
                messages.append(line);
                messages.append("\n");
124        }
125    }
126 }
127 finally
128 {
129     EventQueue.invokeLater(() ->
130     {
131         messages.append("Channel closed\n");
132         interruptibleButton.setEnabled(true);
133         blockingButton.setEnabled(true);
134     });
135 }
136 }
137
138 /**
139  * Connects to the test server, using blocking I/O.
140  */
141 public void connectBlocking() throws IOException
142 {
143     messages.append("Blocking:\n");
144     try (Socket sock = new Socket("localhost", 8189))
145     {
146         in = new Scanner(sock.getInputStream(), "UTF-8");
147         while (!Thread.currentThread().isInterrupted())
148         {
149             messages.append("Reading ");
150             if (in.hasNextLine())
151             {
152                 String line = in.nextLine();
153                 messages.append(line);
154                 messages.append("\n");
155             }
156         }
157     }
158     finally
159     {
160         EventQueue.invokeLater(() ->
161         {
162             messages.append("Socket closed\n");
163             interruptibleButton.setEnabled(true);
164             blockingButton.setEnabled(true);
165         });
166     }
167 }
168
169 /**
170  * A multithreaded server that listens to port 8189 and sends numbers to the client, simulating
171  * a hanging server after 10 numbers.
172  */
173 class TestServer implements Runnable
174 {
175     public void run()
176     {
177         try (ServerSocket s = new ServerSocket(8189))
178         {
179             while (true)
180             {
181                 Socket incoming = s.accept();
182                 Runnable r = new TestServerHandler(incoming);
183                 Thread t = new Thread(r);
184                 t.start();
185             }
186         }
187         catch (IOException e)
188         {
189             messages.append("\nTestServer.run: " + e);
190         }
191     }
192 }
193
194 /**
195  * This class handles the client input for one server socket connection.
196  */
197 class TestServerHandler implements Runnable
198 {
199     private Socket incoming;
200     private int counter;
201
202     /**
203      * Constructs a handler.
204      * @param i the incoming socket
205      */
206     public TestServerHandler(Socket i)
207     {
208         incoming = i;
209     }
210
211     public void run()
212     {
213         try
214         {
215             try
216             {
217                 OutputStream outStream = incoming.getOutputStream();
218                 PrintWriter out = new PrintWriter(
219                     new OutputStreamWriter(outStream, "UTF-8"),
220                     true /* autoFlush */);
while (counter < 100)
{
    counter++;
    if (counter <= 10) out.println(counter);
    Thread.sleep(100);
}
}
finally
{
    incoming.close();
    messages.append("Closing server\n");
}
}
catch (Exception e)
{
    messages.append("\nTestServerHandler.run: " + e);
}
}
}
}
```

| `java.net.InetSocketAddress` | 1.4 |
|---|---|
| • `InetSocketAddress(String hostname, int port)` | 用给定的主机名和端口构造一个地址对象，并在构造期间解析主机名。如果无法解析主机名，该地址对象的未解析属性会被设为 true。 |
| • `boolean isUnresolved()` | 如果此地址对象无法解析，则返回 true。 |

| `java.nio.channels.SocketChannel` | 1.4 |
|---|---|
| • `static SocketChannel open(SocketAddress address)` | 打开一个套接字通道，并将其连接到远程地址。 |

| `java.nio.channels.Channels` | 1.4 |
|---|---|
| • `static InputStream newInputStream(ReadableByteChannel channel)` | 构造一个从给定通道读取的输入流。 |
| • `static OutputStream newOutputStream(WritableByteChannel channel)` | 构造一个向给定通道写入的输出流。 |

## 4.4 获取 Web 数据

要在 Java 程序中访问 Web 服务器，你会希望工作在比套接字连接和 HTTP 请求更高的层次上。在接下来的几节中，我们将讨论 Java 库为此提供的类。

### 4.4.1 URL 和 URI

`URL` 和 `URLConnection` 类封装了从远程站点检索信息的大部分复杂性。你可以从字符串构造一个 `URL` 对象：

```
URL url = new URL(urlString);
```

如果你只是想获取资源的内容，请使用 `URL` 类的 `openStream` 方法。该方法会产出一个 `InputStream` 对象。按通常方式使用它——例如，构造一个 `Scanner`：

```
InputStream inStream = url.openStream();
Scanner in = new Scanner(inStream, "UTF-8");
```

`java.net` 包对 URL（统一资源定位符）和 URI（统一资源标识符）作出了有用的区分。

URI 是一种纯语法构造，包含指定 Web 资源的字符串的各个部分。URL 是一种特殊的 URI，即具有足够信息来定位资源的 URI。其他 URI，例如

```
mailto:cay@horstmann.com
```

不是定位符——从这个标识符中没有可定位的数据。这样的 URI 称为 URN（统一资源名称）。

在 Java 库中，`URI` 类没有用于访问标识符所指定资源的方法——它的唯一用途是解析。相比之下，`URL` 类可以打开指向该资源的流。因此，`URL` 类只适用于 Java 库知道如何处理方案，例如 `http:`、`https:`、`ftp:`、本地文件系统（`file:`）和 JAR 文件（`jar:`）。

要了解为什么解析并不简单，请考虑 URI 可以有多复杂。例如，

```
http://google.com?q=Beach+Chalet
ftp://username:password@ftp.yourserver.com/pub/file.txt
```

URI 规范给出了这些标识符构成的规则。URI 的语法为

```
[schema:]schemaSpecificPart[#fragment]
```

这里，[ . . . ] 表示可选部分，而 : 和 # 按字面包含在标识符中。

如果存在 `schema:` 部分，则该 URI 称为绝对的。否则，称为相对的。

如果 schemaSpecificPart 不以 / 开头，则绝对 URI 是不透明的，例如

```
mailto:cay@horstmann.com
```

所有绝对非不透明 URI 和所有相对 URI 都是分层的。例如

```
http://horstmann.com/index.html
../../java/net/Socket.html#Socket()
```

分层 URI 的 schemaSpecificPart 具有结构

```
[//authority][path][?query]
```

其中，同样，[ . . . ] 表示可选部分。

对于基于服务器的 URI，authority 部分的形式为

```
[user-info@]host[:port]
```

端口必须是整数。

标准化 URI 的 RFC 2396 还支持基于注册表的机制，其中 authority 具有不同的格式，但这并不常用。

URI 类的用途之一是解析标识符并将其分解为各个组成部分。你可以用以下方法检索它们：

- getScheme
- getSchemeSpecificPart
- getAuthority
- getUserInfo
- getHost
- getPort
- getPath
- getQuery
- getFragment

URI 类的另一个用途是处理绝对和相对标识符。如果你有一个绝对 URI，例如

```
http://docs.mycompany.com/api/java/net/ServerSocket.html
```

