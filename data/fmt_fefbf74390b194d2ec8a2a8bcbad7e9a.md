
此合规解决方案定义了一个自定义的 `ExceptionReporterPermission`，目标为 `exc.reporter`，以防止非法的调用者设置默认异常处理器。这可以通过子类 `BasicPermission` 实现，该类允许二进制风格的权限（允许或不允许）。合规解决方案随后使用安全管理器检查调用者是否具有设置处理器的所需的权限。如果检查失败，代码将抛出 `SecurityException`。自定义权限类 `ExceptionReporterPermission` 也定义了两个所需的构造函数。

```java
class LoadLibrary {
    private void loadLibrary() {
        AccessController.doPrivileged(
            new PrivilegedAction() {
                public Object run() {
                    // 特权代码
                    System.loadLibrary("myLib.so");

                    // 执行某些敏感操作，例如
                    // 设置默认异常处理器
                    MyExceptionReporter.setExceptionReporter(reporter);
                    return null;
                }
            });
        );
    }
}

final class MyExceptionReporter extends ExceptionReporter {
    public void setExceptionReporter(ExceptionReporter reporter) {
        SecurityManager sm = System.getSecurityManager();
        if(sm != null) {
            sm.checkPermission(
                new ExceptionReporterPermission("exc.reporter")
            );
        }
    }

    // ... MyExceptionReporter 的其他方法
}

final class ExceptionReporterPermission extends BasicPermission {
    public ExceptionReporterPermission(String permName) {
        super(permName);
    }

    // 尽管 actions 参数被忽略了，
    // 但必须构造构造函数
    public ExceptionReporterPermission(String permName, String actions) {
        super(permName, actions);
    }
}
```

策略文件需要授予两个权限：`ExceptionReporterPermission exc.reporter` 和 `RuntimePermission loadlibrary.myLib`。以下策略文件假设上述源位于 Windows 系统的 `c:\package` 目录下。

```
grant codeBase"file:c:/package" {
    // 对于 *nix，使用 file:${user.home}/package/
    permission ExceptionReporterPermission "exc.reporter";
    permission java.lang.RuntimePermission "LoadLibrary.myLib";
};
```

默认情况下，无法通过 `BasicPermission` 定义支持操作的权限，但如果需要，可以在子类 `Exception-ReporterPermission` 中自由实现这些操作。尽管 `BasicPermission` 是抽象的，但它不包含任何抽象方法；它定义了从 `Permission` 类继承的所有方法。自定义的 `BasicPermission` 类子类必须定义两个构造函数，以调用最合适的（单参数或双参数）父类构造函数（因为父类缺少默认构造函数）。双参数的构造函数接受一个操作，尽管权限并不使用它。这种行为对于从策略文件构建权限对象是必需的。注意，自定义的 `BasicPermission` 类子类被声明为 `final`。

### 适用性

在默认权限无法胜任的情况下不定义自定义权限运行 Java 代码，可能会应用程序暴露权限提升漏洞。

### 参考文献

- [API 2013] Class FilePermission

- [Oaks 2001] Class SecurityManager 第 5 章“The Access Controller”中的“Permissions”小节

- [Oracle 2011d] Java" SE 6 Development Kit (JDK) 中的 Permissions

- [Oracle 2013c] Java Platform Standard Edition 7 Documentation

- [Policy 2010] “Permission Descriptions and Risks”

## 20. 使用安全管理器创建安全沙箱

根据 Java API 类 SecurityManager 文档 [API 2013]，

安全管理器是一个允许应用程序实现安全策略的类。它允许应用程序在执行可能不安全或敏感的操作之前，确定该操作是否在一个允许执行该操作的安全上下文中尝试执行。应用程序可以允许或禁止该操作。

安全管理器可以与任何 Java 代码关联。Applet 器拒绝所有最核心的权限。它的设计目的是防止无意的系统修改、信息泄露和用户冒充。Web 服务器（如 Tomcat 和 WebSphere）使用此机制来隔离 servlet 和恶意的 Java Server Pages (JSP)，同时也保护系统资源。从命令行运行的 Java 应用程序可以使用命令行创建默认或自定义的安全管理器。或者，也可以通过编程安装安全管理器。通过编程安装安全管理器有助于根据有效的安全策略创建一个允许或拒绝敏感操作的默认沙箱。

从 Java 2 SE 开始，SecurityManager 是一个非抽象类。因此，没有显式要求覆盖它的方法。要通过编程使用和创建安全管理器，代码必须具有运行时权限 `createSecurity`（实例化 SecurityManager）和 `setSecurity`（安装）。这些权限仅在已安装安全管理器时才会被检查。这对于已安装默认安全管理器的情况（例如在虚拟主机上）非常有用，所需的权限允许用自定义管理器替换默认管理器。

安全管理器与 `AccessController` 类紧密相关。前者作为访问控制的枢纽，而后者提供了访问控制算法的实际实现。前者支持

- 向后兼容：遗留代码通常包含安全管理器的实现，因为它最初是抽象的。

- 定义自定义策略：子类安全管理器允许定义自定义的安全策略（例如多级、粗粒度或细粒度）。

关于自定义管理器相对于默认管理器的实现和使用，Java 体系规范 [SecuritySpec2010] 指出：

我们鼓励在应用程序代码中使用 AccessController，而对安全管理器的自定义（通过子类）应该是最后的手段，并且必须极其小心。此外，自定义的安全管理器（例如，在调用标准安全检查之前总是检查时间）应该在适当的时候利用 AccessController 提供的算法。

许多 Java SE API 在执行敏感操作之前默认执行安全检查。例如，类 `java.io` 的构造函数

## 20. 使用安全管理器创建安全沙箱

如果调用者没有读取文件的权限，`.FileInputStream` 会抛出 `SecurityException`。由于 `SecurityException` 是 `RuntimeException` 的子类，某些 API 方法（例如 Java `io.FileReader` 类）的声明可能缺少列出 `SecurityException` 的语句。避免依赖 API 方法文档中未指定的安全管理器检查是否存在。

### 不合规代码示例（命令行安装）

此不合规代码示例未能从命令行安装安全管理器。因此，该程序在启用所有权限的情况下运行；也就是说，没有安全管理器来防止程序可能执行的任何恶意操作。

```
java LocalJava
```

## 合规解决方案（默认策略文件）

任何 Java 程序都可以通过程序化方式安装 `SecurityManager`，尽管当前激活的安全管理器可能会禁止此操作。设计为在本地运行的应用程序可以在调用时通过命令行上的标志来指定默认的安全管理器。

当禁止应用程序程序化安装自定义安全管理器，并且要求在任何情况下都遵守默认安全策略时，应首选命令行选项。此合规解决方案使用适当的命令行标志安装默认安全管理器。策略文件为应用程序的预定操作授予权限。

```
java -Djava.security.manager -Djava.security.policy=policyURL \
LocalJavaApp
```

命令行标志可以指定一个全局执行策略的自定义安全管理器。我们使用 `-java.security.manager` 标志，如下：

```
java -Djava.security.manager=my.security.CustomManager ...
```

如果当前的安全策略由安全管理器禁止替换（通过省略 `RuntimePermission("setSecurityManager")`），则任何调用 `setSecurityManager()` 的尝试将抛出 `SecurityException`。

默认策略文件 `java.policy`——在 UNIX 系统的 `/path/to/java.home/lib/security` 目录下以及在 Microsoft Windows 系统中的等效目录——授予了少量权限（读取系统属性、绑定非特权端口等）。用户特定的策略文件也可能位于用户的主目录。这些策略文件的并集指定了授予给程序的权限。`java.security` 文件可以指定使用哪些策略文件。如果删除了系统范围 `java.policy` 或 `java.security` 文件中的任何一个，则不会向执行的 `java.program` 授予权限。

## 合规解决方案（自定义策略文件）

在使用自定义策略文件覆盖 Java 安全策略文件时，请使用双等号 (==) 而不是单等号 (=)：

```
java -Djava.security.manager \
-Djava.security.policy=policyURL \
LocalJavaApp
```

## 合规解决方案（附加策略文件）

applet 会自动使用标准策略文件安装安全管理器。要指定额外的策略文件，请使用 `-j` 标志。

```
appletviewer -Djava.security.manager \
-Djava.security.policy=policyURL LocalJavaApp
```

注意，当安全策略文件（java.security）中的 `.allowSystemProperty` 属性设置为 `false` 时，参数中指定的策略将被忽略；《默认策略实现和策略文件语法 [Policy 2010]》深入讨论了编写策略文件的问题和语法。

### 不合规代码示例（程序化安装）

也可以使用静态 `System.setSecurityManager(Manager)` 方法激活 `SecurityManager`。一次只能有一个激活的 `SecurityManager`。该方法用参数提供的 `SecurityManager` 替换当前激活的 `SecurityManager`，如果参数为 `null`，则不提供 `SecurityManager`。

此不合规代码示例激活了任何当前的 `SecurityManager` 但没有在其位置安装另一个 `SecurityManager`。因此，后续代码将在启用所有权限的情况下运行；对程序可能执行的任何操作将没有任何限制。

```
try {
  System.setSecurityManager(null);
} catch (SecurityException e) {
  // 无法设置安全管理器，记录到文件
}
```

20. 使用安全管理器创建安全沙箱

一个执行明智安全策略的激活 `SecurityManager` 将防止系统去取消它，导致此代码抛出 `SecurityException`。

## 合规解决方案（默认安全管理器）

此合规解决方案实例化并设置了默认的安全管理器。

```
try {
  System.setSecurityManager(new SecurityManager());
} catch (SecurityException se) {
  // 无法设置安全管理器，适当记录日志
}
```

## 合规解决方案（自定义安全管理器）

此合规解决方案演示了如何通过密码密码构造函数实例化名为 `CustomSecurityManager` 的自定义 `SecurityManager` 类；然后将此自定义安全管理器安装为激活的安全管理器。

```
char password[] = /* initialize */
try {
  System.setSecurityManager(
    new CustomSecurityManager("password here")
  );
} catch (SecurityException se) {
  // 无法设置安全管理器，适当记录日志
}
```

此代码执行后，执行安全检查的 API 将使用自定义的安全管理器。如前所述，只有当默认安全管理器缺少所需功能时，才应安装自定义安全管理器。

### 适用性

Java 安全根本上取决于安全管理器的存在。在缺少它的情况下，敏感操作可以在不受限制的情况下执行。

在运行时程序化检测 `SecurityManager` 的存在或否是简单的。静态分析可以解决是否存在在代码执行时尝试安装 `SecurityManager` 的代码。在某些特殊情况下，检查 `SecurityManager` 是否安装得足够早、它是否指定了所需的属性、或者是否保证已安装可能是可能的，但通常情况下是不可判的。

在已知始终从命令行安装全局默认安全管理器的受控环境中，可以省略 `setSecurityManager()` 方法的调用。这很难强制，如果环境配置不当，可能会导致漏洞。

### 参考文献

- [API 2013] Class SecurityManager

- Class AccessOperationContext

- Class AccessController

- [Gong 2003] §6.1, "Security Manager"

- [Pistoia 2004] §7.4, "The Security Manager"

- [Policy 2010] Default Policy Implementation and Policy Syntax

- [SecuritySpec 2010] §6.2, "SecurityManager versus AccessController"

## 21. 不要让不可信的代码滥用回调方法的权限

回调提供了一种在发生感兴趣的事件时注册并调用（或回调）方法的方法。Java 将回调用于 applet 和 servlet 生命周期事件、AWT 和 Swing 事件通知（如按钮点击）、对存储器进行异步读写，甚至在 `Runnable.run()` 中，其中新线程会自动执行指定的 `run()` 方法。

在 Java 中，回调通常使用接口实现。回调的一般结构如下：

```
public interface Callback {
    void callMethod();
}

class CallbackImpl implements Callback {
    public void callMethod() {
        System.out.println("Callback invoked");
    }
}

class CallbackAction {
    private Callback callback;
```

## 21. 不要让不可信的代码滥用回调方法的权限

```
public CallbackAction(Callback callback) {
    this.callback = callback;
}

public void perform() {
    callback.callMethod();
}

class Client {
    public static void main(String[] args) {
    CallbackAction action =
    new CallbackAction(new CallbackImpl());
    // ..
    action.perform(); // 输出 "Callback invoked"
  }
}
```

回调方法通常在具有全权限的系统环境中调用。认为恶意代码需要位于栈上才能执行操作是合理的，但事实并非如此。恶意代码可能会设置对象，将回调桥接到安全检查的操作。例如，一个可以从用户操作操作文件系统的对话框可能会发布来自恶意代码的事件。或者，恶意代码可以将文件选择器伪装成无害的东西的同时重定向用户事件。

根据 Oracle 的安全编码指南 [SCG 2010]：

回调方法通常是在不改变权限的情况下调用的，这意味着它们可能在比声明处权限更高的特文中文中执行。如果这些回调方法接受来自不可信代码的数据，可能会发生权限提升。
