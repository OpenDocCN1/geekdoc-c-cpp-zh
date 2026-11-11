
要创建代理对象，请使用 `Proxy` 类的 `newProxyInstance` 方法。该方法有三个参数：

- 一个*类加载器*。作为 Java 安全模型的一部分，平台类和应用类、从 Internet 下载的类等可以使用不同的类加载器。我们将在第二卷的[第 9 章](#)中讨论类加载器。在此示例中，我们指定加载平台类和应用类的“系统类加载器”。
- 一个 `Class` 对象数组，每个待实现的接口对应一个对象。
- 一个调用处理器。

还剩下两个问题。我们如何定义处理器？以及可以用生成的代理对象做什么？答案当然取决于我们想用代理机制解决的问题。代理可用于许多目的，例如

- 将方法调用路由到远程服务器
- 将用户界面事件与正在运行的程序中的操作关联起来
- 出于调试目的跟踪方法调用

在示例程序中，我们使用代理和调用处理器来跟踪方法调用。我们定义一个 `TraceHandler` 包装类，用于存储被包装的对象。它的 `invoke` 方法只是打印要调用的方法的名称和参数，然后以被包装对象作为隐式参数调用该方法。

```java
class TraceHandler implements InvocationHandler
{
   private Object target;
   public TraceHandler(Object t)
   {
      target = t;
   }
   public Object invoke(Object proxy, Method m, Object[] args)
         throws Throwable
   {
      // print method name and parameters
      . . .
      // invoke actual method
      return m.invoke(target, args);
   }
}
```

下面说明如何构造一个代理对象，使其任一方法被调用时都会产生跟踪行为：

```java
Object value = . . .;
// construct wrapper
var handler = new TraceHandler(value);
// construct proxy for one or more interfaces
var interfaces = new Class[] { Comparable.class};
Object proxy = Proxy.newProxyInstance(
    ClassLoader.getSystemClassLoader(),
    new Class[] { Comparable.class }, handler);
```

现在，每当在 proxy 上调用某个接口中的方法时，都会打印出方法名称和参数，然后在该 value 上调用该方法。

在清单 6.10 所示的程序中，我们使用代理对象来跟踪二分查找。我们用整数 1 . . . 1000 的代理填充一个数组。然后调用 `Arrays` 类的 `binarySearch` 方法在数组中搜索一个随机整数。最后，打印匹配的元素。

```java
var elements = new Object[1000];
// fill elements with proxies for the integers 1 . . . 1000
for (int i = 0; i < elements.length; i++)
{
    Integer value = i + 1;
    elements[i] = Proxy.newProxyInstance(. . .); // proxy for value;
}
// construct a random integer
Integer key = (int) (Math.random() * elements.length) + 1;
// search for the key
int result = Arrays.binarySearch(elements, key);
// print result if found
if (result >= 0) System.out.println(elements[result]);
```

Integer 类实现了 Comparable 接口。代理对象属于一个在运行时定义的类。（它的名称类似于 $Proxy0。）该类也实现了 Comparable 接口。但是，它的 compareTo 方法会调用代理对象处理器的 invoke 方法。

> **注意：**
>
> 正如本章前面所见，`Integer` 类实际上实现的是 `Comparable<Integer>`。但是，在运行时，所有泛型类型都会被擦除，代理是使用原始 `Comparable` 类的类对象构造的。

binarySearch 方法会进行如下调用：

```java
if (elements[i].compareTo(key) < 0) . . .
```

由于我们用代理对象填充了数组，因此 compareTo 方法会调用 TraceHandler 类的 invoke 方法。该方法打印方法名称和参数，然后在被包装的 Integer 对象上调用 compareTo。

最后，在示例程序的末尾，我们调用

```java
System.out.println(elements[result]);
```

println 方法会在代理对象上调用 toString，而该调用也会被重定向到调用处理器。

下面是程序运行的完整跟踪输出：

```
500.compareTo(288)
250.compareTo(288)
375.compareTo(288)
312.compareTo(288)
281.compareTo(288)
296.compareTo(288)
288.compareTo(288)
288.toString()
```

你可以看到二分查找算法如何通过每一步将搜索区间减半来逐步锁定键。注意，即使 `toString` 方法不属于 `Comparable` 接口，它也会被代理——正如你将在下一节看到的，某些 `Object` 方法总是会被代理。

### **清单 6.10** proxy/ProxyTest.java

```java
1  package proxy;
2
3  import java.lang.reflect.*;
4  import java.util.*;
5
6  /**
7   * This program demonstrates the use of proxies.
8   * @version 1.02 2021-06-16
9   * @author Cay Horstmann
10  */
11 public class ProxyTest
12 {
13    public static void main(String[] args)
14    {
15       var elements = new Object[1000];
16
17       // fill elements with proxies for the integers 1 . . . 1000
18       for (int i = 0; i < elements.length; i++)
19       {
20          Integer value = i + 1;
21          var handler = new TraceHandler(value);
Object proxy = Proxy.newProxyInstance(
    ClassLoader.getSystemClassLoader(),
    new Class[] { Comparable.class }, handler);
    elements[i] = proxy;
}

// construct a random integer
Integer key = (int) (Math.random() * elements.length) + 1;

// search for the key
int result = Arrays.binarySearch(elements, key);

// print match if found
if (result >= 0) System.out.println(elements[result]);
}
}

/**
 * An invocation handler that prints out the method name and parameters, then
 * invokes the original method
 */
class TraceHandler implements InvocationHandler
{
    private Object target;

    /**
     * Constructs a TraceHandler
     * @param t the implicit parameter of the method call
     */
    public TraceHandler(Object t)
    {
        target = t;
    }

    public Object invoke(Object proxy, Method m, Object[] args)
throws Throwable
    {
58      // print implicit argument
        System.out.print(target);
60      // print method name
        System.out.print("." + m.getName() + "(");
62      // print explicit arguments
        if (args != null)
        {
            for (int i = 0; i < args.length; i++)
            {
                System.out.print(args[i]);
                if (i < args.length - 1) System.out.print(", ");
            }
        }
        System.out.println(")");

73      // invoke actual method
        return m.invoke(target, args);
75  }
76  }
```

## 6.5.3 代理类的属性

现在你已经看到了代理类的实际运用，下面来回顾它们的一些属性。请记住，代理类是在运行中的程序里动态创建的。但是，一旦创建，它们就是常规类，就像虚拟机中的任何其他类一样。

所有代理类都扩展 Proxy 类。代理类只有一个实例字段——调用处理器，它定义在 Proxy 超类中。执行代理对象任务所需的任何额外数据都必须存储在调用处理器中。例如，当我们在清单 6.10 所示的程序中代理 Comparable 对象时，TraceHandler 包装了实际对象。

所有代理类都会重写 Object 类的 toString、equals 和 hashCode 方法。与所有代理方法一样，这些方法只是调用调用处理器上的 invoke。Object 类的其他方法（例如 clone 和 getClass）不会被重新定义。

代理类的名称并未定义。Oracle 虚拟机中的 `Proxy` 类生成的类名以字符串 `$Proxy` 开头。

对于特定的类加载器和有序接口集合，只有一个代理类。也就是说，如果你用相同的类加载器和接口数组调用 `newProxyInstance` 方法两次，你会得到同一个类的两个对象。你也可以使用 `getProxyClass` 方法获得该类：

```java
Class proxyClass = Proxy.getProxyClass(null, interfaces);
```

代理类始终是 `public` 和 `final`。如果代理类实现的所有接口都是 public，则该代理类不属于任何特定包。否则，所有非 public 接口必须属于同一个包，并且该代理类也将属于该包。

你可以通过调用 Proxy 类的 `isProxyClass` 方法来测试某个特定类对象是否表示代理类。

> **注意：**
>
> 调用代理的默认方法会触发调用处理器。要实际调用该方法，请使用 `InvocationHandler` 接口的静态 `invokeDefault` 方法。例如，下面是一个调用默认方法并将抽象方法传递给另一个目标的调用处理器。

```java
InvocationHandler handler = (proxy, method, args) =>
    {
        if (method.isDefault())
            return InvocationHandler.invokeDefault(proxy, method,
                    args);
        else
            return method.invoke(target, args);
    }
```
