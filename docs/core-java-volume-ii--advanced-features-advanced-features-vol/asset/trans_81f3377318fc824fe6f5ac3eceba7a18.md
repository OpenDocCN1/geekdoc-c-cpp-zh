
### 代码清单 10.4（续）

```java
public class WordCheckPermission extends Permission
{
   private String action;

   /**
    * Constructs a word check permission.
    * @param target a comma separated word list
    * @param action "insert" or "avoid"
    */
   public WordCheckPermission(String target, String action)
   {
      super(target);
      this.action = action;
   }

   public String getActions()
   {
      return action;
   }

   public boolean equals(Object other)
   {
      if (other == null) return false;
      if (!getClass().equals(other.getClass())) return false;
      var b = (WordCheckPermission) other;
      if (!Objects.equals(action, b.action)) return false;
      if ("insert".equals(action)) return Objects.equals(getName(), b.getName());
      else if ("avoid".equals(action)) return badWordSet().equals(b.badWordSet());
      else return false;
   }

   public int hashCode()
   {
      return Objects.hash(getName(), action);
   }

   public boolean implies(Permission other)
   {
      if (!(other instanceof WordCheckPermission)) return false;
      var b = (WordCheckPermission) other;
      if (action.equals("insert"))
      {
         return b.action.equals("insert") && getName().indexOf(b.getName()) >= 0;
      }
      else if (action.equals("avoid"))
      {
         if (b.action.equals("avoid")) return badWordSet().containsAll(b.badWordSet());
         else if (b.action.equals("insert"))
         {
            for (String badWord : badWordSet())
               if (b.getName().indexOf(badWord) >= 0) return false;
            return true;
         }
         else return false;
      }
      else return false;
   }

   /**
    * Gets the bad words that this permission rule describes.
    * @return a set of the bad words
    */
   public Set<String> badWordSet()
   {
      var set = new HashSet<String>();
      set.addAll(List.of(getName().split(",")));
      return set;
   }
}
```

### 代码清单 10.5 permissions/PermissionTest.java

```java
package permissions;

import java.awt.*;

import javax.swing.*;

/**
 * This class demonstrates the custom WordCheckPermission.
 * @version 1.05 2018-05-01
 * @author Cay Horstmann
 */
public class PermissionTest
{
   public static void main(String[] args)
   {
      System.setProperty("java.security.policy", "permissions/PermissionTest.policy");
      System.setSecurityManager(new SecurityManager());
      EventQueue.invokeLater(() ->
      {
         var frame = new PermissionTestFrame();
         frame.setTitle("PermissionTest");
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         frame.setVisible(true);
      });
   }
}

/**
 * This frame contains a text field for inserting words into a text area that is protected
 * from "bad words".
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
      var panel = new JPanel();
      panel.add(textField);
      var openButton = new JButton("Insert");
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
      catch (SecurityException ex)
      {
         JOptionPane.showMessageDialog(this, "I am sorry, but I cannot do that.");
         ex.printStackTrace();
      }
   }
}
```

### 代码清单 10.5（续）

```java
/**
 * A text area whose append method makes a security check to see that no bad words are added.
 */
class WordCheckTextArea extends JTextArea
{
   public void append(String text)
   {
      var p = new WordCheckPermission(text, "insert");
      SecurityManager manager = System.getSecurityManager();
      if (manager != null) manager.checkPermission(p);
      super.append(text);
   }
}
```

## java.security.Permission 1.2

- `Permission(String name)` 使用给定的目标名称构造一个权限。
- `String getName()` 返回此权限的目标名称。
- `boolean implies(Permission other)` 检查此权限是否蕴含另一个权限。如果另一个权限描述的是由本权限所描述条件推导出的更具体条件，则属于这种情况。

## 10.3 用户认证

Java API 提供了一个名为 Java 认证与授权服务（JAAS）的框架，它将平台提供的认证与权限管理集成在一起。我们将在以下各节讨论 JAAS 框架。

### 10.3.1 JAAS 框架

顾名思义，JAAS 框架有两个组成部分。“认证”部分关注确定程序用户身份。“授权”部分将用户映射到权限。

JAAS 是一个“可插拔”API，它将 Java 应用程序与用于实现认证的特定技术隔离开来。它支持 UNIX 登录、Windows 登录、Kerberos 认证和基于证书的认证等。

一旦用户通过认证，就可以附加一组权限。例如，这里我们授予 Harry 一组其他用户没有的特定权限：

```
grant principal com.sun.security.auth.UnixPrincipal "harry"
{
    permission java.util.PropertyPermission "user.*", "read";
    . . .
};
```

`com.sun.security.auth.UnixPrincipal` 类检查正在运行此程序的 UNIX 用户名。其 `getName` 方法返回 UNIX 登录名，我们检查该名称是否等于 `"harry"`。

使用 `LoginContext` 允许安全管理器检查此类 grant 语句。以下是登录代码的基本轮廓：

```java
try
{
    System.setSecurityManager(new SecurityManager());
    var context = new LoginContext("Login1"); // defined in JAAS configuration file
    context.login();
    // get the authenticated Subject
    Subject subject = context.getSubject();
    . . .
    context.logout();
}
catch (LoginException exception) // thrown if login was not successful
{
    exception.printStackTrace();
}
```

现在，subject 表示已通过认证的个体。

`LoginContext` 构造函数中的字符串参数 `"Login1"` 引用 JAAS 配置文件中具有相同名称的条目。以下是一个示例配置文件：

```
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

当然，JDK 不包含生物识别登录模块。`com.sun.security.auth.module` 包中提供了以下模块：

- `UnixLoginModule`
- `NTLoginModule`
- `Krb5LoginModule`
- `JndiLoginModule`
- `KeyStoreLoginModule`

登录策略由一系列登录模块组成，每个模块都标记为 required、sufficient、requisite 或 optional。这些关键字的含义由以下算法给出。

登录会对 subject 进行认证，而 subject 可以有多个 principal。principal 描述 subject 的某些属性，例如用户名、组 ID 或角色。正如你在 grant 语句中所见，principal 支配权限。`com.sun.security.auth.UnixPrincipal` 描述 UNIX 登录名，而 `UnixNumericGroupPrincipal` 可以测试是否为 UNIX 组成员。

grant 子句可以使用以下语法测试 principal：

```
grant principalClass "principalName"
```

例如：

```
grant com.sun.security.auth.UnixPrincipal "harry"
```

当用户登录后，你随后在一个单独的访问控制上下文中运行需要检查 principal 的代码。使用静态 `doAs` 或 `doAsPrivileged` 方法启动一个新的 `PrivilegedAction`，其 `run` 方法执行该代码。

这两个方法都通过调用实现 `PrivilegedAction` 接口的对象的 `run` 方法来执行一个操作，并使用 subject 的 principal 的权限：

```java
PrivilegedAction<T> action = () -> {
    // run with permissions of subject principals
    ...
};
T result
    = Subject.doAs(subject, action); // or Subject.doAsPrivileged(subject, action, null)
```

如果这些操作可以抛出受检异常，则需要改为实现 `PrivilegedExceptionAction` 接口。

`doAs` 和 `doAsPrivileged` 方法之间的区别很微妙。`doAs` 方法从当前访问控制上下文开始，而 `doAsPrivileged` 方法从新的上下文开始。后一种方法允许
