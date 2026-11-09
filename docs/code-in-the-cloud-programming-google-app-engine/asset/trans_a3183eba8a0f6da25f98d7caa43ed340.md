
## 9.4 使用 GWT 进行测试与部署

现在我们已经有了一个基本的 GWT 应用，接下来运行它。和在 Python 中一样，在 App Engine 中运行 GWT 应用有两种方式：本地模式，应用在你的机器上运行；部署模式，应用在 App Engine 云端运行。

GWT 中的本地模式与 Python 中的本地模式非常不同。在 Python 中，本地模式适合在不部署的情况下进行测试，但它并没有真正提供同等水平的调试支持。但在 GWT 中，本地模式下客户端和服务器都用 Java 运行，我们可以使用 Eclipse 的全部能力来调试 GWT 应用。这带来了巨大差别：我们可以完全使用断点、跟踪、单步执行以及所有其他 Java 调试工具。

要在 Eclipse 中以本地模式运行，请转到 Run 菜单并选择 Run As.../Web Application。GWT 会打开一个本地模拟浏览器环境来显示客户端，并启动本地 Tomcat Web 服务器来执行服务器端。

要将其部署到 App Engine，请转到 Package Explorer 视图并右键单击项目。在弹出的项目菜单中有一个 Google 子菜单。只需选择 Deploy to App Engine，你的程序就会在 App Engine 云端上线。如果它需要关于该项目的任何信息，会在你第一次运行部署命令时提示你填写。

我们完成了第一个基础 GWT 应用。它目前还不如我们的 Python 聊天应用功能完整，但它有更好的 UI 和更清晰的通信层。在下一章中，我们将运用学到的 GWT 知识来构建聊天应用的 Java 版本。在此过程中，我们将了解数据存储的 Java 接口，以及 GWT 对服务器端 Java 代码施加的限制。

## 第 10 章：管理服务器端数据

在前几章中，我们考察了 App Engine 中一个基础 GWT 应用的各个部分。我们构建了 GUI，设置了一个简单的 RPC，并把所有基础连接串接起来，让应用运行起来。在本章中，我们将使用 GWT 实现聊天程序。我们不会花太多时间研究如何构建 GUI——已有整本的书讲解如何在 GWT 中构建 GUI，而且 GWT 自己关于其 UI 类的文档非常出色。我们将把大部分时间花在 *数据存储* 上，它是在 App Engine 中处理持久化数据的机制。就像在 Python 中一样，我们需要做一些额外工作，使类可持久化并且可查询。现在我们将看看如何使用 Java 做到这一点。

我们还会简要讨论 App Engine Java 端服务器端基础连接的一些其他问题。具体来说，App Engine 对代码能做什么以及如何在 App Engine 云端环境中运行施加了一些限制，我们将考察这些限制是什么，以及它们对我们编写 App Engine 应用服务器端的方式有什么影响。

### 10.1 Java 中的数据持久化

如果你回头看看第 4 章 *在云端管理数据*（第 53 页），就会记得我们需要在 Python 代码中做一些额外工作来存储数据，并让一切在云端正确运行。Java 中也是如此。不幸的是，这正是 Java 的静态类型使事情变得有些繁琐的地方之一。App Engine 使用的基本后端数据存储与 Python 中完全相同，但让它与 Java 配合工作需要多花一点心思。这并不困难，只是我们需要在代码中加入更多样板代码。像往常一样，Eclipse 可以为我们处理其中大量工作。不过，我们还是先在不借助 Eclipse 帮助的情况下开始吧。我们将手写所有内容，以便理解所有细节。

以典型的 Google 风格，App Engine 让数据存储与 Java 配合工作的方式是：采用一个标准 Java API——Java Data Objects（JDO）——并挑选出其功能中一个有用的子集。JDO 是一个极其复杂、臃肿的 API（标准通常如此）。但它其中有一个不错的精华内核。App Engine 使用的正是这个内核。

下面，我们将了解 JDO 持久化如何用于描述持久化对象，以及如何存储、查询和检索它们。

### 存储 Java 类

在 Python 的数据存储接口中，我们通过向类对象添加属性来创建持久化类。在 Java 中，我们会做类似的事情——但在 Java 中，属性是通过在类声明中使用注解来添加的。用示例来描述最容易，因此我们将拿聊天消息并将其转换为一个数据对象：

下载 `workspace/PortalChat/src/com/progprog/aebook/persistchat/ChatMessage.java`

```java
package com.progprog.aebook.persistchat;

import java.util.Date;

import javax.jdo.annotations.IdGeneratorStrategy;
import javax.jdo.annotations.IdentityType;
import javax.jdo.annotations.PersistenceCapable;
import javax.jdo.annotations.Persistent;
import javax.jdo.annotations.PrimaryKey;

import com.google.appengine.api.datastore.Key;

@PersistenceCapable(identityType = IdentityType.APPLICATION)
public class ChatMessage {

    public ChatMessage() {
    }

    public ChatMessage(String sender, String msg, String chatname) {
        this.senderName = sender;
        this.message = msg;
        this.chat = chatname;
    }

    @PrimaryKey
    @Persistent(valueStrategy = IdGeneratorStrategy.IDENTITY)
    private Key key;

    @Persistent
    protected String senderName;

    @Persistent
    protected String message;

    @Persistent
    protected String chat;

    @Persistent
    protected long date;

    public Key getKey() {
        return key;
    }

    public String getSenderName() {
        return senderName;
    }

    public void setSenderName(String senderName) {
        this.senderName = senderName;
    }

    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }

    public String getChat() {
        return chat;
    }

    public void setChat(String chat) {
        this.chat = chat;
    }

    public long getDate() {
        return date;
    }

    public void setDate(long date) {
        this.date = date;
    }
}
```

让我们更仔细地看看这个示例：

- 1. 要让 Java 对象存储在 App Engine 数据存储中，其类必须声明为持久化类。在 JDO 中，通过附加 `@PersistenceCapable` 注解来完成。在完整的 JDO 中，我们需要声明身份类型。App Engine 仅支持 `IdentityType.APPLICATION`，但由于 Java 的类型系统要求注解与其声明匹配，因此该字段必须始终声明。

  为了能够存储、检索或搜索特定对象，对象必须有一个用于标识它的唯一键。在 Python 中，当我们定义持久化对象时，框架会自动添加一个数据存储使用的不可见键字段。在 Java 中，一切都必须静态声明。因此，我们需要在源代码中手动插入键声明，并将其注解为键。我们使用 `@PrimaryKey` 注解将其标记为键，并通过 `@Persistent` 注解的 `valueStrategy = IdGeneratorStrategy.IDENTITY` 属性告诉它，比较主键的方式是对象标识。

- 2. 持久化对象中每个应存储的字段都需要用 `@Persistent` 注解。

Java 中的数据对象有一些限制。它们大多是为了让错综复杂的对象指针保持可管理状态的要求：

- 当一个持久化对象将另一个持久化对象作为字段包含时，它就拥有该对象，并且不允许任何其他持久化对象引用该被拥有的对象。这意味着我们有时需要保存对象。
- 当一个持久化对象包含其他持久化对象的集合时，它拥有该集合中的所有对象。
- 我们仅限于使用 Java 的基本集合类。我们不能使用数组，也不能使用任何扩展集合类型。我们可以使用 ArrayList、LinkedList、HashSet、TreeSet、Stack 和 Vector 等具体类。我们也可以使用更抽象的接口，比如 List，但当我们保存并重新加载一个对象时，无法保证恢复后的对象中列表类型仍然相同
