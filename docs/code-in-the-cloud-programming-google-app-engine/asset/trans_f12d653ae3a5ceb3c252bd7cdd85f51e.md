
## 第16章：云中的服务器计算

到目前为止，我们所有的 App Engine 程序都完全是被动且请求驱动的。它们驻留在 App Engine 服务器上，在用户发起某种请求之前什么都不做；一旦收到请求就立即响应，然后再次回到什么都不做的状态。对于许多应用来说，这正是我们想要的。聊天室实际上不需要做别的事，只需在人们请求时把消息发送给他们。文件系统不会自行读写文件；它只在有人明确请求时才执行操作。

但有时被动方式行不通。例如，如果你在构建电子商务网站，可能希望每天生成销售汇总。或者，如果你在构建协作日历应用，可能希望能够通知人们即将发生的事件。这些事情不是被动的。它们要求服务器在不由请求触发的情况下运行某些代码，触发依据是时间安排或某个基于数据的事件发生。

App Engine 提供两种用于非被动服务器端计算的机制：一种按照固定时间表执行操作，另一种按照基于事件的 JavaScript 机制执行操作。本章我们将研究这两种机制，并了解如何使用它们在服务器上运行任务。

这是 App Engine 真正出彩的领域之一。正如我们在本书中反复看到的，App Engine 围绕 HTTP 请求处理程序构建。服务器端计算同样如此：你仍然将所有代码编写为简单的 HTTP 请求处理程序。由于 App Engine 允许你使用这些请求处理程序的方式，你可以为需要在特定时间表所指定的时刻对数据计算的任务构建任意复杂的工作流，并利用分析结果做有用的事。

我们将以报告生成作为典型示例，并为聊天服务设置一个报告任务：生成每个聊天室每天发送了多少条消息的报告。

### Cron 调度器

我们的应用有一个用于时间表的文件。在 Java 中，该文件名为 WEB-INF/cron.xml；在 Python 中，它是 cron.yaml。由于我们使用的是聊天应用的 Java 版本，我们会把一条条目放入 WEB-INF/cron.xml 文件。该文件包含一个由 `<cronentries>` 标签包裹的条目列表。每个条目是一个 `<cron>` 元素。

cron 条目包含三个字段，表示为 XML 子元素：

- `<url>`：首先，它有一个 URL。正如我们在 App Engine 中反复看到的，它基本上把所有东西都包装在 HTTP 请求中——几乎一切都是用 HTTP 请求处理程序实现的。Cron 也不例外。App Engine 将按照时间表为该 URL 生成一个 **GET** 请求。
- `<description>`：其次，有一个描述。这只是文档；它没有执行时效果。它的作用是让阅读 cron 文件的人理解该任务的内容。
- `<schedule>`：关于任务应在何时被调用的文本描述。

时间表用一种看起来像英语描述的方式编写：

- *每隔若干单位*：按指定间隔运行。例如 every 2 hours，或 every 3 minutes。
- *在指定时间*：在指定时间运行。例如 every monday 12:00 将在每周一中午运行；或 every day 00:00 将在每天午夜运行。
- *每月第 n 次*：为了让报告运行得不那么频繁，可以相对于月份来指定：2nd tuesday（省略月份表示 *每个月*），或 3rd friday of march, june, september, december，使报告每年运行四次。

例如，要让聊天室每天生成报告，请将以下内容放入 cron 文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<cronentries>
    <cron>
        <url>/report?to=mark@gmail.com</url>
        <description>Generate a daily chat usage report.</description>
        <schedule>every day 00:00</schedule>
    </cron>
</cronentries>
```

报告将通过向 `/report` URL 发送 **GET** 请求来生成，并且每天午夜执行一次。

### 实现 Cron 请求处理程序

请求处理程序的基本代码很直接。我们一直在编写针对聊天消息的数据存储查询——对于这个处理程序，我们只需要执行一个查询，返回过去二十四小时内添加的所有聊天消息。然后检查结果长度，这就是报告结果。

严格来说，这有些过度。我们不需要检索所有消息。但在大多数分析/报告类定时任务中，我们会希望浏览最新时间段的全部数据，所以这就是你在这类任务中会使用的基本结构：先检索全部数据，然后浏览这些数据并生成结果。

```java
@SuppressWarnings("serial")
public class Reporter extends HttpServlet {

    Logger logger = Logger.getLogger(Reporter.class.getName());

    @Override
    @SuppressWarnings("unchecked")
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        String toAddress = req.getParameter("to");
        PersistenceManager pm = Persister.getPersistenceManager();
        Query query = pm.newQuery(PChatMessage.class);
        query.setFilter("date >= yesterday");
        query.declareParameters("long yesterday");
        query.setOrdering("date");
        long yesterday = System.currentTimeMillis() - (24 * 60 * 60 * 1000);
        List<PChatMessage> messages =
                (List<PChatMessage>)query.execute(yesterday);
        resp.setContentType("text/html");

        PrintWriter out = new PrintWriter(new CharArrayWriter());
        out.println("<html>");
        out.println("  <head>");
        out.println("    <title>Chat Usage Report</title>");
        out.println("  </head>");
        out.println("  <body>");
        out.println("    <h1>Chat Usage Report</h1>");
        out.println("    <p> Messages in the last 24 hours: " +
                messages.size());
        out.println("</body></html>");
        out.close();
        String report = out.toString();

        Session mailSession =
                Session.getDefaultInstance(new Properties(), null);
        try {
            Message msg = new MimeMessage(mailSession);
            msg.setFrom(new InternetAddress(toAddress));
            msg.addRecipient(Message.RecipientType.TO,
                    new InternetAddress(req.getParameter("to")));
            msg.setSubject("Chat Status Report");
            msg.setText(report);
            Transport.send(msg);
        } catch (AddressException e) {
            // Email address is constant and valid, so this
            // can't happen.
        } catch (MessagingException e) {
            logger.log(Level.INFO, "Error sending report: " + e);
        }
    }
}
```

这段代码是一个简单的 servlet——到现在，你应该无需帮助就能读懂它。它只是我们之前见过的东西的组合：

- 1. 首先，我们执行通常的持久化操作，组装一个查询并从数据存储中检索聊天消息，就像第 141 页第 10.1 节 *Java 中的数据持久化* 中的代码那样。
- 2. 然后我们使用这些信息生成一个包含报告的字符串。
- 3. 最后，使用我们在第 243 页第 15.4 节 *发送邮件* 中看到的 App Engine 邮件服务，发送该消息。

还有一件事需要做。我们告诉调度器为我们的应用在 `/report` URL 上生成请求。我们需要告诉 App Engine 将这个 servlet 连接到该 URL。我们像往常一样做——向 `war/WEB-INF/web.xml` 的 `<servlet>` 元素添加一个条目来注册 servlet，然后添加一个 `<servlet-mapping>` 条目将 servlet 绑定到该 URL。

```xml
<servlet>
    <servlet-name>ChatServletReporter</servlet-name>
    <servlet-class>com.pragprog.aebook.chat.server.Reporter</servlet-class>
    <auth-constraint>
        <role-name>admin</role-name>
    </auth-constraint>
</servlet>
...
<servlet-mapping>
    <servlet-name>ChatServletReporter</servlet-name>
    <url-pattern>/report</url-pattern>
</servlet-mapping>
```

### 16.2 使用任务队列动态运行作业

在服务器上执行计算的第二种方法比 Cron 调度器更灵活、更有趣。不过，基本元素以类似方式处理：你想在用户请求之外完成的每一项工作，都设置为某个特定虚拟 URL 上的 HTTP 请求处理程序。

使用 Cron 调度器时，我们指定某个特定请求应按照特定时间表被调用。但有很多任务我们不一定想按时间表执行。例如，在我的博客上，我会定期检查关于它收到多少次点击以及点击来自何处的统计信息；如果数据中有任何有趣的内容，我会把报告副本发送到我的电子邮件地址。这没有特定时间表——每当我注意到想留存参考的内容时，就会请求一份报告。

App Engine 提供了一项名为 *任务队列* 的服务来处理这类事情。任务队列是一种非常通用的机制，用于执行最终由用户请求发起的任何工作——它不必是需要立即完成的工作。例如，如果我想构建一个在线日历，我可以让日历应用向任务队列添加一些内容来发送电子邮件提醒；该任务会被放入队列，并指定它应该运行的时间。该任务会在用户创建日历时被加入队列
