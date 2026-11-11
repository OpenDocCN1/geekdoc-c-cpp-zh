
## **清单 9.4** *（续）*

```java
53 else if (action.equals("avoid"))
54 {
55     if (b.action.equals("avoid")) return b.badWordSet().containsAll(badWordSet());
56     else if (b.action.equals("insert"))
57     {
58         for (String badWord : badWordSet())
59             if (b.getName().indexOf(badWord) >= 0) return false;
60         return true;
61     }
62     else return false;
63 }
64 else return false;
65 }
66
67 /**
68  * Gets the bad words that this permission rule describes.
69  * @return a set of the bad words
70  */
71 public Set<String> badWordSet()
72 {
73     Set<String> set = new HashSet<>();
74     set.addAll(Arrays.asList(getName().split(",")));
75     return set;
76 }
77 }
```

## **清单 9.5** permissions/PermissionTest.java

```java
1 package permissions;
2
3 import java.awt.*;
4
5 import javax.swing.*;
6
7 /**
8  * This class demonstrates the custom WordCheckPermission.
9  * @version 1.04 2016-05-10
10  * @author Cay Horstmann
11  */
12 public class PermissionTest
13 {
14     public static void main(String[] args)
15     {
16         System.setProperty("java.security.policy", "permissions/PermissionTest.policy");
17         System.setSecurityManager(new SecurityManager());
```

## **清单 9.5** *（续）*

```java
EventQueue.invokeLater(() ->
{
   JFrame frame = new PermissionTestFrame();
   frame.setTitle("PermissionTest");
   frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
   frame.setVisible(true);
});
}

/**
 * This frame contains a text field for inserting words into a text area that is protected from
 * "bad words".
 */
class PermissionTestFrame extends JFrame
{
   private JTextField textField;
   private WordCheckTextArea textArea;
   private static final int TEXT_ROWS = 20;
   private static final int TEXT_COLUMNS = 60;

   public PermissionTestFrame()
   {
      textField = new JTextField(20);
      JPanel panel = new JPanel();
      panel.add(textField);
      JButton openButton = new JButton("Insert");
      panel.add(openButton);
      openButton.addActionListener(event -> insertWords(textField.getText()));

      add(panel, BorderLayout.NORTH);

      textArea = new WordCheckTextArea();
      textArea.setRows(TEXT_ROWS);
      textArea.setColumns(TEXT_COLUMNS);
      add(new JScrollPane(textArea), BorderLayout.CENTER);
      pack();
   }

   /**
    * Tries to insert words into the text area. Displays a dialog if the attempt fails.
    * @param words the words to insert
    */
   public void insertWords(String words)
   {
      try
      {
         textArea.append(words + "\n");
      }
67  catch (SecurityException ex)
68  {
69      JOptionPane.showMessageDialog(this, "I am sorry, but I cannot do that.");
70      ex.printStackTrace();
71  }
72  }
73  }
74
75  /**
76   * A text area whose append method makes a security check to see that no bad words are added.
77   */
78  class WordCheckTextArea extends JTextArea
79  {
80      public void append(String text)
81      {
82          WordCheckPermission p = new WordCheckPermission(text, "insert");
83          SecurityManager manager = System.getSecurityManager();
84          if (manager != null) manager.checkPermission(p);
85          super.append(text);
86      }
87  }
```

## **java.security.Permission 1.2**

- **Permission(String name)**  
  使用给定的目标名称构造一个权限。
- **String getName()**  
  返回此权限的目标名称。
- **boolean implies(Permission other)**  
  检查此权限是否蕴含另一个权限。如果另一个权限描述的条件是此权限所描述条件的更具体结果，则属于这种情况。

## **9.3 用户认证**

Java API 提供了一个名为 Java 认证和授权服务（JAAS）的框架，它将平台提供的认证与权限管理集成在一起。我们将在后续章节讨论 JAAS 框架。

### 9.3.1 JAAS 框架

顾名思义，JAAS 框架有两个组成部分。“认证”部分关注于确定程序用户的身份。“授权”部分将用户映射到权限。

JAAS 是一个“可插拔”的 API，它将 Java 应用程序与用于实现认证的特定技术隔离开来。它支持 UNIX 登录、NT 登录、Kerberos 认证和基于证书的认证等。

一旦用户通过认证，就可以附加一组权限。例如，这里我们授予哈里一组其他用户没有的特定权限：

```java
grant principal com.sun.security.auth.UnixPrincipal "harry"
{
    permission java.util.PropertyPermission "user.*", "read";
    ...
};
```

`com.sun.security.auth.UnixPrincipal` 类检查正在运行此程序的 UNIX 用户的名称。它的 `getName` 方法返回 UNIX 登录名，我们检查该名称是否等于 "harry"。

使用 `LoginContext` 让安全管理器检查这样的 grant 语句。以下是登录代码的基本框架：

```java
try
{
    System.setSecurityManager(new SecurityManager());
    LoginContext context = new LoginContext("Login1");  // defined in JAAS configuration file
    context.login();
    // get the authenticated Subject
    Subject subject = context.getSubject();
    ...
    context.logout();
}
catch (LoginException exception)  // thrown if login was not successful
{
    exception.printStackTrace();
}
```

现在，主体表示已通过认证的个体。

`LoginContext` 构造函数中的字符串参数 "Login1" 指向 JAAS 配置文件中具有相同名称的条目。以下是一个示例配置文件：

```java
Login1
{
  com.sun.security.auth.module.UnixLoginModule required;
  com.whizzbang.auth.module.RetinaScanModule sufficient;
};

Login2
{
  . . .
};
```

当然，JDK 不包含任何生物特征登录模块。以下模块由 `com.sun.security.auth.module` 包提供：

- UnixLoginModule
- NTLoginModule
- Krb5LoginModule
- JndiLoginModule
- KeyStoreLoginModule

登录策略由一系列登录模块组成，每个模块被标记为 *required*、*sufficient*、*requisite* 或 *optional*。这些关键字的含义由以下算法给出。

一次登录认证一个 *主体*，该主体可以拥有多个 *主体身份*。一个 *主体身份* 描述主体的某种属性，例如用户名、组 ID 或角色。正如你在 grant 语句中所看到的，主体身份决定权限。`com.sun.security.auth.UnixPrincipal` 描述 UNIX 登录名，而 `UnixNumericGroupPrincipal` 可以测试是否属于某个 UNIX 组。

grant 子句可以用以下语法测试某个主体身份：

```
grant principalClass "principalName"
```

例如：

```
grant com.sun.security.auth.UnixPrincipal "harry"
```

当用户登录后，你随后会在单独的访问控制上下文中运行需要检查主体身份的代码。使用静态方法 `doAs` 或 `doAsPrivileged` 启动一个新的 `PrivilegedAction`，其 `run` 方法执行该代码。

这两种方法都通过调用实现 `PrivilegedAction` 接口的对象的 `run` 方法来执行操作，并使用该主体各主体身份的权限：

```java
PrivilegedAction<Boolean> action = () ->
{
  // run with permissions of subject principals
  . . .
};
T result = Subject.doAs(subject, action); // or Subject.doAsPrivileged(subject, action, null)
```

如果操作可能抛出受检异常，则需要改为实现 `PrivilegedExceptionAction` 接口。

doAs 和 doAsPrivileged 方法之间的差异很微妙。doAs 方法从当前访问控制上下文开始，而 doAsPrivileged 方法从新的上下文开始。后一种方法允许你将登录代码的权限与“业务逻辑”的权限分开。在我们的示例应用程序中，登录代码具有以下权限：

```
permission javax.security.auth.AuthPermission "createLoginContext.Login1";
permission javax.security.auth.AuthPermission "doAsPrivileged";
```

已认证的用户具有以下权限：

```
permission java.util.PropertyPermission "user.*", "read";
```

如果我们使用 doAs 而不是 doAsPrivileged，那么登录代码也将需要该权限。

清单 9.6 和 9.7 中的程序演示了如何将权限限制为特定用户。AuthTest 程序认证一个用户，并运行一个检索系统属性的简单操作。

要使此示例正常工作，请将登录代码和操作代码打包到两个单独的 JAR 文件中：

```
javac auth/*.java
jar cvf login.jar auth/AuthTest.class
jar cvf action.jar auth/SysPropAction.class
```

如果查看清单 9.8 中的策略文件，你会看到名为 harry 的 UNIX 用户拥有读取所有文件的权限。将 harry 改为你的登录名。然后运行以下命令：

```
java -classpath login.jar:action.jar
  -Djava.security.policy=auth/AuthTest.policy
  -Djava.security.auth.login.config=auth/jaas.config
  auth.AuthTest
```

清单 9.9 显示了登录配置。

在 Windows 上，将 AuthTest.policy 中的 UnixPrincipal 改为 NTUserPrincipal，并将 jaas.config 中的 UnixLoginModule 改为 NTLoginModule。运行程序时，使用分号分隔 JAR 文件：

```
java -classpath login.jar;action.jar . . .
```

