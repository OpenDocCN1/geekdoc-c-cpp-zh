
**注意：** 可以支持更复杂的两阶段协议，即如果登录配置中的所有模块都成功，则提交登录。有关更多信息，请参阅位于 http://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASLMDevGuide.html 的登录模块开发者指南。

### 清单 9.10 `jaas/SimplePrincipal.java`

```java
package jaas;

import java.security.*;
import java.util.*;

/**
 * A principal with a named value (such as "role=HR" or "username=harry").
 */
public class SimplePrincipal implements Principal
{
    private String descr;
    private String value;

    /**
     * Constructs a SimplePrincipal to hold a description and a value.
     * @param descr the description
     * @param value the associated value
     */
    public SimplePrincipal(String descr, String value)
    {
        this.descr = descr;
        this.value = value;
    }

    /**
     * Returns the role name of this principal.
     * @return the role name
     */
    public String getName()
    {
        return descr + "=" + value;
    }

    public boolean equals(Object otherObject)
    {
        if (this == otherObject) return true;
        if (otherObject == null) return false;
        if (getClass() != otherObject.getClass()) return false;
        SimplePrincipal other = (SimplePrincipal) otherObject;
        return Objects.equals(getName(), other.getName());
    }

    public int hashCode()
    {
        return Objects.hashCode(getName());
    }
}
```

### 清单 9.11 `jaas/SimpleLoginModule.java`

```java
package jaas;

import java.io.*;
import java.nio.file.*;
import java.security.*;
import java.util.*;
import javax.security.auth.*;
import javax.security.auth.callback.*;
import javax.security.auth.login.*;
import javax.security.auth.spi.*;

/**
 * This login module authenticates users by reading usernames, passwords, and roles from a text
 * file.
 */
public class SimpleLoginModule implements LoginModule
{
    private Subject subject;
    private CallbackHandler callbackHandler;
    private Map<String, ?> options;

    public void initialize(Subject subject, CallbackHandler callbackHandler,
            Map<String, ?> sharedState, Map<String, ?> options)
    {
        this.subject = subject;
        this.callbackHandler = callbackHandler;
        this.options = options;
    }

    public boolean login() throws LoginException
    {
        if (callbackHandler == null) throw new LoginException("no handler");

        NameCallback nameCall = new NameCallback("username: ");
        PasswordCallback passCall = new PasswordCallback("password: ", false);
        try
        {
            callbackHandler.handle(new Callback[] { nameCall, passCall });
        }
        catch (UnsupportedCallbackException e)
        {
            LoginException e2 = new LoginException("Unsupported callback");
            e2.initCause(e);
            throw e2;
        }
        catch (IOException e)
        {
            LoginException e2 = new LoginException("I/O exception in callback");
            e2.initCause(e);
            throw e2;
        }

        try
        {
            return checkLogin(nameCall.getName(), passCall.getPassword());
        }
        catch (IOException ex)
        {
            LoginException ex2 = new LoginException();
            ex2.initCause(ex);
            throw ex2;
        }
    }

    /**
     * Checks whether the authentication information is valid. If it is, the subject acquires
     * principals for the user name and role.
     * @param username the user name
     * @param password a character array containing the password
     * @return true if the authentication information is valid
     */
    private boolean checkLogin(String username, char[] password) throws LoginException, IOException
    {
        try (Scanner in = new Scanner(Paths.get("" + options.get("pwfile")), "UTF-8"))
        {
            while (in.hasNextLine())
            {
                String[] inputs = in.nextLine().split("\\|");
                if (inputs[0].equals(username) && Arrays.equals(inputs[1].toCharArray(), password))
                {
                    String role = inputs[2];
                    Set<Principal> principals = subject.getPrincipals();
                    principals.add(new SimplePrincipal("username", username));
                    principals.add(new SimplePrincipal("role", role));
                    return true;
                }
            }
            return false;
        }
    }

    public boolean logout()
    {
        return true;
    }

    public boolean abort()
    {
        return true;
    }

    public boolean commit()
    {
        return true;
    }
}
```

### 清单 9.12 `jaas/SimpleCallbackHandler.java`

```java
package jaas;

import javax.security.auth.callback.*;


/**
 * This simple callback handler presents the given user name and password.
 */
public class SimpleCallbackHandler implements CallbackHandler
{
    private String username;
    private char[] password;

    /**
     * Constructs the callback handler.
     * @param username the user name
     * @param password a character array containing the password
     */
    public SimpleCallbackHandler(String username, char[] password)
    {
        this.username = username;
        this.password = password;
    }
```

### 清单 9.14 `jaas/JAASTest.policy`

```java
grant codebase "file:login.jar"
{
    permission java.awt.AWTPermission "showWindowWithoutWarningBanner";
    permission java.awt.AWTPermission "accessEventQueue";
    permission javax.security.auth.AuthPermission "createLoginContext.Login1";
    permission javax.security.auth.AuthPermission "doAsPrivileged";
    permission javax.security.auth.AuthPermission "modifyPrincipals";
    permission java.io.FilePermission "jaas/password.txt", "read";
};

grant principal jaas.SimplePrincipal "role=admin"
{
    permission java.util.PropertyPermission "*", "read";
};
```

### 清单 9.15 `jaas/jaas.config`

```java
Login1
{
    jaas.SimpleLoginModule required pwfile="jaas/password.txt" debug=true;
};
```

- **javax.security.auth.callback.CallbackHandler** 1.4
  - `void handle(Callback[] callbacks)` 处理给定的回调，按需与用户交互，并将安全信息存储在回调对象中。
- **javax.security.auth.callback.NameCallback** 1.4
  - `NameCallback(String prompt)`
  - `NameCallback(String prompt, String defaultName)` 使用给定的提示和默认名称构造一个 NameCallback。
  - `String getName()`
  - `void setName(String name)` 获取或设置此回调收集的名称。
  - `String getPrompt()` 获取查询此名称时要使用的提示。
  - `String getDefaultName()` 获取查询此名称时要使用的默认名称。

“令人紧张的文字”），在 JDK 1.0 安全模型中，小程序无法做很多有用的事情。例如，由于 JDK 1.0 下的小程序受到如此严密的监管，它们在企业内联网上无法发挥多大作用，尽管从公司安全内联网执行小程序所附带的风险相对较小。Sun 很快意识到，要让小程序真正有用，用户需要能够根据小程序来源分配*不同*级别的安全权限。如果小程序来自受信任的供应商且未被篡改，该小程序的用户就可以决定是否授予该小程序更多权限。

要给予某个小程序更多信任，我们需要知道两件事：

- 小程序来自哪里？
- 代码在传输过程中是否被损坏？

过去 50 年里，数学家和计算机科学家开发了复杂的算法，用于确保数据完整性和电子签名。`java.security` 包包含许多此类算法的实现。幸运的是，你不需要理解底层数学，就能使用 `java.security` 包中的算法。在接下来的几节中，我们将展示消息摘要如何检测数据文件中的变化，以及数字签名如何证明签名者的身份。

### 9.4.1 消息摘要

消息摘要是数据块的数字指纹。例如，所谓的 SHA-1（安全散列算法 #1）可将任意数据块（无论多长）压缩为 160 位（20 字节）的序列。与真实指纹一样，人们希望没有两条消息具有相同的 SHA-1 指纹。当然，这不可能成立——SHA-1 指纹只有 2^160 个，因此必然有些消息具有相同指纹。但 2^160 如此之大，发生重复的概率可以忽略不计。有多可以忽略不计？根据 James Walsh 在 *《真实概率：风险如何影响你的日常生活》*（梅里特出版社，1996）一书中的说法，你被闪电击中致死的概率约为三万分之一。现在，再想想另外九个人——例如，你最不喜欢的九位经理或教授。你和*他们所有人*都被闪电击中致死的概率，比伪造消息具有与原消息相同 SHA-1 指纹的概率还要高。（当然，会有超过十个人死于闪电击中，而且其中很可能没有一个是你认识的人。不过，我们讨论的是*你所特别选择的那群人*全部被消灭这一渺茫得多的概率。）

消息摘要有两个基本特性：

- 如果数据中的一位或多位发生变化，消息摘要也会变化。
