
对象（这意味着我们可能保存了使用 LinkedList 的某些内容，却取回使用 ArrayList 的某些内容）。由于这可能产生相当显著的性能影响，我建议为 JDO 字段显式使用具体集合类型。

- 我们可以通过在数据对象上标注 `@Persistent(serialized=true)` 来使用 Java 可序列化类型。请注意，它们的行为与通常对 Java 的预期略有不同。例如，假设某个持久对象的列表字段中有某个可序列化对象的两个副本。如果我们保存该对象再加载它，这两个副本不保证 `==`，而它们是否 equals() 取决于我们类的 equals() 方法如何实现。
- String 类型的字段不允许超过 500 字节。我们可以使用 datastore 包中的 Text 类为该字段存储更长的字符串，但将无法基于该字段的值执行查询。
- 如果我们不使用 Eclipse，就需要添加一个名为 _代码增强_ 的额外编译步骤。在增强期间，App Engine JDO 实现会根据持久化注解向类添加代码，使这些类能够被数据存储保存和查询。我们需要确保每次重新编译 Java 源码时都执行增强过程。（Eclipse 会自动将 JDO 增强纳入项目构建，因此无需担心——这也是使用 Eclipse 的又一个理由！）

## 10.2 在 GWT 中存储持久对象

在 Python 中，将内容存储到数据存储中非常简单。我们创建一个持久对象，然后调用它的 put 方法。转眼间！——它就存好了。在 Java 中，我们需要多做一点工作。同样，这有点像是静态样板代码。Java 为我们提供了很多优势，但确实需要多得多的样板代码。

为了能够存储和检索对象，我们需要一个称为 PersistenceManagerFactory 的东西。该工厂的创建成本很高，我们不想每次处理请求时都重新初始化它；相反，我们将其设置为当应用加载到 App Engine 云中的服务器时创建。并且我们希望在一个集中且合适的位置创建它，以确保任何需要 PersistenceManager 的人都知道在哪里找到该工厂的唯一实例。对此有一个自然的解决方案——单例设计模式。我们将创建一个单例类，它以静态方式创建 PersistenceManager 的单个实例，然后任何需要它的人都可以访问该实例。

下载 `workspace/PersistChat/src/com/pragprog/ebook/persistchat/server/Persister.java`

```java
package com.pragprog.aebook.persistchat.server;

import javax.jdo.JDOHelper;
import javax.jdo.PersistenceManager;
import javax.jdo.PersistenceManagerFactory;

public final class Persister {

    private static final PersistenceManagerFactory pmfInstance =
        JDOHelper.getPersistenceManagerFactory("transactions-optional");

    private Persister() {}

    public static PersistenceManagerFactory get() {
        return pmfInstance;
    }

    public static PersistenceManager getPersistenceManager() {
        return get().getPersistenceManager();
    }
}
```

现在，任何需要使用持久化管理器的客户端代码只需调用 Persister.getPersistenceManager()。有了持久化管理器，我们可以通过调用 PersistenceManager.makePersistent() 来存储对象，然后调用 PersistenceManager.close()。

这比 Python 的 o.put() 调用麻烦得多：我们需要设置持久化管理器工厂、分配一个 PersistenceFactory，并在完成后调用 close()。幸运的是，这样做有好处。通过 PersistenceFactory 的接口提供了对事务的支持。从我们分配持久化管理器开始，直到调用其 .close() 方法为止，我们所做的一切都是一个原子单元的一部分——也就是说，要么全部成功，要么全部失败。我们存储的每个对象、对持久对象所做的每次更改，要么全部存储，要么全都不存储。这就是事务的美妙之处：我们获得了关系数据库的安全性和保障。样板代码可能看起来烦人，但它有优点。

我们已准备好发布新消息。我们需要创建一个 RPC 服务，客户端通过它告诉服务器何时有要发布的新消息。（再次值得指出的是，在 GWT 中我们将 post 操作实现为异步 RPC——就我们程序的操作而言，它确实如此——而不是陷入 XMLHttpRequest 的混乱之中。）我们的 RPC 服务需要两个方法：一个用于发布新消息，一个用于获取消息。基本接口如下所示：

### 事务

当你与任何人谈论分布式应用时，你会不断听到 *事务性*。原因如下。

事务性可以防止数据损坏。没有事务性，如果你在存储某些内容时被中断——因为网络故障或所涉某台计算机崩溃——你的数据存储可能最终处于不一致状态。

例如，假设你正在编写一个在线商店。你创建一条订单记录，指示发货部门向客户发货；然后创建一条计费记录，告诉银行如何收取该订单的付款。如果你的系统在存储发货记录和存储计费记录之间崩溃，你可能发出产品却从未收到付款！

你希望这两个步骤是 *原子性* 的，这意味着要么两者都成功存储，要么两者都不存储。所有内容都成功存储或什么都不存储的原子单元称为 *事务*。

Java 数据存储提供了一种将多个存储操作收集到单个事务中的方法。

下载 workspace/persistchat/src/com/pragprog/aebook/persistchat/client/ChatSubmissionService.java

```java
package com.pragprog.aebook.persistchat.client;
import java.util.Date;
import java.util.List;
import com.google.gwt.user.client.rpc.RemoteService;
import com.google.gwt.user.client.rpc.RemoteServiceRelativePath;
import com.pragprog.aebook.persistchat.ChatMessage;

@RemoteServiceRelativePath("chat")
public interface ChatSubmissionService extends RemoteService {
    List<ChatMessage> postMessage(ChatMessage message);
    List<ChatMessage> getMessages(String room);
    List<ChatMessage> getMessagesSince(String chat, Date timestamp);
}
```

我们像往常一样将其转换为异步接口：

```java
package com.pragprog.aebook.persistchat.client;

import java.util.Date;
import java.util.List;

import com.pragprog.aebook.persistchat.ChatMessage;
import com.google.gwt.user.client.rpc.AsyncCallback;

public interface ChatSubmissionServiceAsync {
    void postMessage(ChatMessage message,
        AsyncCallback<List<ChatMessage>> callback);

    void getMessages(String chatroom,
        AsyncCallback<List<ChatMessage>> callback);

    void getMessagesSince(String chat, Date timestamp,
        AsyncCallback<List<ChatMessage>> callback);
}
```

我们通过 server 包中的一个类来实现它。实现非常直接。我们使用刚刚实现的 Persister 来获取用于该操作的 PersistenceManager，使消息对象持久化，以便它作为事务的一部分被保存，然后关闭持久化管理器，这将执行事务。最后，我们使用另一个服务方法（直接从服务器调用）来向用户提供聊天中消息的更新列表。

```java
public List<ChatMessage> postMessage(ChatMessage message) {
    PersistenceManager persister = Persister.getPersistenceManager();
    persister.makePersistent(message);
    persister.close();
    return getMessages(message.getChat());
}
```

如果我们想将任何其他对象作为与聊天消息同一事务的一部分保存，只需在调用 close 之前添加更多 makePersistent 调用来存储它们。
