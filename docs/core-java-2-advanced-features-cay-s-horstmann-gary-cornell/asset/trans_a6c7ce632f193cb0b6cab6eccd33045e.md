

您可以在同一个引擎上调用多个脚本。如果某个脚本定义了变量、函数或类，大多数脚本引擎会保留这些定义以供后续使用。例如，

```java
engine.eval("n = 1728");
Object result = engine.eval("n + 1");
```

将返回 1729。

**注意：** 要确定在多个线程中并发执行脚本是否安全，请调用

```java
Object param = factory.getParameter("THREADING");
```

返回值是以下之一：

- null：并发执行不安全。
- "MULTITHREADED"：并发执行是安全的。一个线程的效果可能对另一个线程可见。
- "THREAD-ISOLATED"：除了"MULTITHREADED"之外，每个线程维护不同的变量绑定。
- "STATELESS"：除了"THREAD-ISOLATED"之外，脚本不会改变变量绑定。

您通常希望向引擎添加变量绑定。绑定由名称和关联的 Java 对象组成。例如，考虑以下语句：

```java
engine.put("k", 1728);
Object result = engine.eval("k + 1");
```

脚本代码会从“引擎作用域”中的绑定读取 k 的定义。这一点特别重要，因为大多数脚本语言可以访问 Java 对象，而且语法通常比 Java 语法更简单。例如，

```java
engine.put("b", new JButton());
engine.eval("b.text = \"OK\"");
```

反过来，您也可以检索由脚本语句绑定的变量：

```java
engine.eval("n = 1728");
Object result = engine.get("n");
```

除了引擎作用域之外，还有一个全局作用域。您添加到 ScriptEngineManager 的任何绑定对所有引擎都是可见的。

除了向引擎或全局作用域添加绑定之外，您还可以将它们收集在 `Bindings` 类型的对象中，并将其传递给 `eval` 方法：

```java
Bindings scope = engine.createBindings();
scope.put("b", new JButton());
engine.eval(script, scope);
```

如果一组绑定不应在将来调用 eval 方法时持续存在，这很有用。

> **注意：** 您可能希望拥有除引擎和全局作用域之外的其他作用域。例如，Web 容器可能需要请求和会话作用域。但是，这样做需要您自己实现。您需要编写一个实现 `ScriptContext` 接口的类，管理一组作用域。每个作用域由一个整数标识，编号较小的作用域应首先被搜索。（标准库提供了 `SimpleScriptContext` 类，但它只包含全局和引擎作用域。）

| `javax.script.ScriptEngine` | 6 |
|---|---|
| • `Object eval(String script)` | |
| • `Object eval(Reader reader)` | |
| • `Object eval(String script, Bindings bindings)` | |
| • `Object eval(Reader reader, Bindings bindings)` | |
| 计算由字符串或读取器给出的脚本，受给定绑定的约束。 | |
| • `Object get(String key)` | |
| • `void put(String key, Object value)` | |
| 获取或放置引擎作用域中的绑定。 | |
| • `Bindings createBindings()` | |
| 创建一个适合此引擎的空 Bindings 对象。 | |

| `javax.script.ScriptEngineManager` | 6 |
|---|---|
| • `Object get(String key)` | |
| • `void put(String key, Object value)` | |
| 获取或放置全局作用域中的绑定。 | |

### 8.1.5 编译脚本

某些脚本引擎可以将脚本代码编译为中间形式以便高效执行。这些引擎实现了 `Compilable` 接口。以下示例展示了如何编译和评估脚本文件中的代码：

```java
Reader reader = new FileReader("myscript.js");
CompiledScript script = null;
if (engine instanceof Compilable)
    script = ((Compilable) engine).compile(reader);
```

脚本编译后，您可以执行它。以下代码在编译成功时执行已编译的脚本，如果引擎不支持编译则执行原始脚本：

```java
if (script != null)
    script.eval();
else
    engine.eval(reader);
```

当然，只有在需要重复执行脚本时，编译脚本才有意义。

| `javax.script.Compilable` 6 |
|---|
| • `CompiledScript compile(String script)`<br>• `CompiledScript compile(Reader reader)`<br><br>编译由字符串或读取器给出的脚本。 |

| `javax.script.CompiledScript` 6 |
|---|
| • `Object eval()`<br>• `Object eval(Bindings bindings)`<br><br>计算此脚本 |

### 8.1.6 示例：脚本化 GUI 事件

为了说明脚本 API，我们将编写一个示例程序，允许用户使用他们选择的脚本语言指定事件处理器。

看看清单 8.1 中的程序，它向任意框架类添加了脚本功能。默认情况下，它读取清单 8.2 中的 `ButtonFrame` 类，这与卷 I 中的事件处理演示类似，但有两个区别：

- 每个组件都设置了其 name 属性。
- 没有事件处理器。

事件处理器在属性文件中定义。每个属性定义的形式为

*componentName.eventName* = *scriptCode*

例如，如果您选择使用 JavaScript，请在 js.properties 文件中提供事件处理器，如下所示：

```properties
yellowButton.action=panel.background = java.awt.Color.YELLOW
blueButton.action=panel.background = java.awt.Color.BLUE
redButton.action=panel.background = java.awt.Color.RED
```

随附代码还包含 Groovy、R 和 SISC Scheme 的文件。

程序首先为命令行指定的语言加载引擎。如果未指定语言，我们使用 JavaScript。

然后，如果存在 init.language 脚本，我们处理它。这对于 R 和 Scheme 语言很有用，它们需要一些初始化，我们不想在每个事件处理器脚本中都包含这些初始化。

接下来，我们递归遍历所有子组件，并将绑定 (*name*, *object*) 添加到组件映射中。然后我们将绑定添加到引擎。

接下来，我们读取文件 *language.properties*。对于每个属性，我们合成一个事件处理器代理，该代理会导致脚本代码被执行。细节有点技术性。如果您想详细了解实现，可能需要阅读卷 I 第 6 章中关于代理的章节。但本质上，每个事件处理器都调用

```java
engine.eval(scriptCode);
```

让我们更详细地看看 yellowButton。当处理行

```properties
yellowButton.action=panel.background = java.awt.Color.YELLOW
```

时，我们找到 name 为 "yellowButton" 的 JButton 组件。然后我们附加一个 ActionListener，其 actionPerformed 方法执行脚本

```java
panel.background = java.awt.Color.YELLOW
```

如果脚本是使用 Nashorn 完成的。

引擎包含一个绑定，将名称 "panel" 绑定到 JPanel 对象。当事件发生时，panel 的 setBackground 方法被执行，颜色随之改变。

您可以通过执行以下命令，直接使用 JavaScript 事件处理器运行此程序

```java
69   }
70
71   /**
72    * 收集容器中所有已命名的组件。
73    * @param c 组件
74    * @param namedComponents 用于输入组件名称和组件的映射
75    */
76   private static void getComponentBindings(Component c, Map<String, Component> namedComponents)
77   {
78       String name = c.getName();
79       if (name != null) { namedComponents.put(name, c); }
80       if (c instanceof Container)
81       {
82           for (Component child : ((Container) c).getComponents())
83               getComponentBindings(child, namedComponents);
84       }
85   }
86
87   /**
88    * 向对象添加监听器，其监听器方法执行脚本。
89    * @param beanName 要向其添加监听器的 bean 的名称
90    * @param eventName 监听器类型的名称，如 "action" 或 "change"
91    * @param scriptCode 要执行的脚本代码
92    * @param engine 执行代码的引擎
93    * @param bindings 执行时的绑定
94    * @throws IntrospectionException
95    */
96   private static void addListener(String beanName, String eventName, final String scriptCode,
97       final ScriptEngine engine, Map<String, Component> components)
98       throws ReflectiveOperationException, IntrospectionException
99   {
100      Object bean = components.get(beanName);
101      EventSetDescriptor descriptor = getEventSetDescriptor(bean, eventName);
102      if (descriptor == null) return;
103      descriptor.getAddListenerMethod().invoke(bean,
104          Proxy.newProxyInstance(null, new Class[] { descriptor.getListenerType() },
105              (proxy, method, args) ->
106              {
107                  engine.eval(scriptCode);
108                  return null;
109              }
110          ));
111  }
112
113  private static EventSetDescriptor getEventSetDescriptor(Object bean, String eventName)
114      throws IntrospectionException
115  {
116      for (EventSetDescriptor descriptor : Introspector.getBeanInfo(bean.getClass())
117          .getEventSetDescriptors())
```

*（续）*

