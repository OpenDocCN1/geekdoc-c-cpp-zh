
## 9.3 GWT 中的 RPC

现在我们进入复杂的部分。

正如我之前提到的，AJAX 代码并不是显式写在 GWT 中的。相反，我们编写一种称为*远程过程调用*（RPC）的东西。RPC 看起来几乎像一个普通的方法调用，但在底层，它会被系统转换为从客户端发送到服务器的请求。RPC 的返回值是服务器发回客户端的响应。

与其他任何 RPC 系统一样，GWT 中也有客户端和服务器端。我们可以分别查看它们的代码；把它们串联起来则取决于 GWT RPC 系统。

如果你做过分布式编程，Google 风格的 RPC 可能并不是你习惯的方式。传统上，RPC 会尽可能表现得像传统函数调用。换句话说，如果我们想为一个阶乘函数提供 RPC，函数实现看起来会像传统函数声明，而调用它看起来也会像传统调用。例如，Java 有一个原生 RPC 层，我们通过接口定义远程对象，然后就可以在接口类型的对象上调用方法。

我们可以把一个阶乘服务定义为 Java 接口：

```java
public interface Fact extends Remote {
    int fact(int n);
}
```

然后在使用它的代码中，我们会获取远程接口的句柄，并像下面这样直接调用它：

```java
int j = f.fact(n);
```

围绕这一点，服务器中会有一些底层连接机制来让该对象可用，以便客户端能获取它的句柄；客户端同样会有代码来取得远程对象的句柄。但调用本身看起来就像普通的本地调用。

这种方法有一个问题：通信很慢。一次远程过程调用很容易比本地调用多花两个数量级的时间。在传统调用中，代码会一直卡住等待，直到收到服务器返回的响应。这会造成巨大的时间浪费，并可能在我们的用户界面中造成不可接受的延迟。

因此，Google 对远程调用使用了一种称为*异步*或*延续传递*风格的方式。调用本身不返回任何内容。相反，它接受一个额外参数，该参数是一个函数，用于在收到 RPC 结果时对结果进行调用。

例如，假设我们有一个阶乘服务。在传统风格中，我们想要做的是：

```java
System.out.println("Foo = " + Math.log(3 * f.fact(n)));
```

在延续传递风格中，那会像这样：

```java
f.fact(n, new AsyncCallback<Integer>() {
    public void onSuccess(Integer result) {
        System.out.println("Foo = " + Math.log(3 * result));
    }
});
```

我所做的只是把原本要使用 RPC 返回值的代码包装进一个可以传给远程调用的对象中。这样做只是启动这个过程。当 RPC 把调用转换为消息、发送消息、等待服务器发送响应，再把响应消息转换回结果值时，我的代码可以转去做其他事情。每当结果返回时，回调就会被调用，调用的结果也会得到处理。

如果你习惯了命令式编程，这可能感觉有点不自然。（函数式程序员一直这么做，即使他们并没有在做分布式编程。）这需要一些时间适应，即使适应了，有时也显得有点别扭。但总的来说，不必等待 RPC 的优势超过了这些问题。它让应用对用户更响应，而这是最重要的。

### GWT 中的客户端 RPC

无论一个工具包有多好，通信都从来不是简单的事。我们需要能够把参数转换为可以作为消息传递的格式，也需要能够处理网络造成的延迟甚至失败。为了应对这一点，GWT 使用了一种非常 Google 式的惯用法。在 Google，我们有一些非常独特且程式化的方式来处理某些基本问题。特别是，我们有一种使用异步响应处理器来执行远程过程调用的方式。对于没有做过大量 Google 风格分布式编程的人来说，这相当陌生。总的来说，GWT 在让底层管道不可见方面确实非常出色。然而，在这个例子中，他们决定不这么做。

- 3. 这是同步方法声明。服务方法的任何参数都必须扩展 `java.io.Serializable` 或 GWT 特有的变体 `com.google.gwt.user.client.rpc.IsSerializable`。这里非常重要的一点是，GWT 使用 Java 序列化接口来标记将在 RPC 中传递的类，并*不*意味着它使用 Java 序列化。使用 IsSerializable 或 Serializable 只是一个标记，用来告诉 GWT 它需要生成序列化和反序列化该类型的代码。GWT 使用的实际格式甚至与 Java 的标准序列化不兼容。

  方法声明本身完全是标准的：它只是一个普通的接口方法声明。

除了同步接口之外，我们还需要编写一个异步接口。坦白说，这里正是我不明白 GWT 团队为什么没有提供某种自动支持的地方之一。为了生成异步接口，我们只需编写另一个接口，它是对同步接口的纯样板式转换。它必须包含与同步接口中的方法名称完全相同的方法；每个方法必须返回 void；并且每个方法都在末尾添加一个参数，该参数是一个 AsyncCallback，其类型参数是同步方法的返回类型。例如：

下载 workspace/HelloChat/src/com/pragprog/ebook/hellochat/client/GreetingServiceAsync.java

```java
package com.pragprog.ebook.hellochat.client;

import com.google.gwt.user.client.rpc.AsyncCallback;

/**
 * The async counterpart of <code>GreetingService</code>.
 */
public interface GreetingServiceAsync {
    void greetServer(String input, AsyncCallback<String> callback);
}
```

异步接口与同步接口没有任何显式连接，也不必使用任何特殊注解或继承任何特殊类。它实际上只由客户端使用——用于在异步接口和同步接口之间进行映射的实际底层管道由 GWT 生成。异步接口的唯一目的是提供客户端将使用的调用接口。

### GWT 中的服务器端 RPC

GWT RPC 的服务器端简单得令人惊讶。我们只需用一个扩展 RemoteServiceServlet 的类来实现同步客户端接口。对于我们的问候服务，该实现如下：

下载 workspace/HelloChat/src/com/pragprog/ebook/hellochat/server/GreetingServiceImpl.java

```java
package com.pragprog.ebook.hellochat.server;
import com.pragprog.ebook.hellochat.client.GreetingService;
import com.google.gwt.user.server.rpc.RemoteServiceServlet;

/**
 * The server-side implementation of the RPC service.
 */
@SuppressWarnings("serial")
public class GreetingServiceImpl extends RemoteServiceServlet implements
        GreetingService {

    public String greetServer(String input) {
        String serverInfo = getServletContext().getServerInfo();
        String userAgent = getThreadLocalRequest().getHeader("User-Agent");
        return "Hello, " + input + "!<br><br>I'm running " +
                serverInfo + "<br><br>It looks like you are using:<br>" +
                userAgent;
    }
}
```

@SuppressWarnings 注解有点不寻常。它存在的原因是，后续几代 Java 虚拟机中的序列化会为每个类文件使用版本标识符。如果我们有一个实现了 `java.io.Serializable` 的类，却没有为它提供版本标识符字段，Java 就会生成警告。服务实现总是实现 Serializable，因为 RemoteServiceServlet 继承自标准的 servlet 类，而该类实现了 Serializable。由于 GWT 不使用版本标识符，把它包含在代码中只会成为无意义的杂乱内容；该注解可防止编译器生成令人困惑的警告信息。

这就是我们在服务器端需要做的全部工作。当然，当我们想使用数据存储进行持久化时，情况会变得更复杂。但我们会把那个留到下一章。

所以现在，我们的 hello 应用已经具备了完整的 RPC。它比我们之前在 Python 中做 AJAX 的方式干净得多：我们有一个定义良好的接口，只需进行一次方法调用就能调用它。我们不必担心创建 XmlHTTPRequests、解析参数、检查状态码，或我们在 Python 中需要做的任何杂乱且容易出错的事情。
