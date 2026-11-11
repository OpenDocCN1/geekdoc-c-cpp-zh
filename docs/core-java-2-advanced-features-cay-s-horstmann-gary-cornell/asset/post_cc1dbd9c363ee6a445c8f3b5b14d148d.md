
You can invoke multiple scripts on the same engine. If one script defines variables, functions, or classes, most scripting engines retain the definitions for later use. For example,

```java
engine.eval("n = 1728");
Object result = engine.eval("n + 1");
```

will return 1729.

**NOTE:** To find out whether it is safe to concurrently execute scripts in multiple threads, call

```java
Object param = factory.getParameter("THREADING");
```

The returned value is one of the following:

- null: Concurrent execution is not safe.
- "MULTITHREADED": Concurrent execution is safe. Effects from one thread might be visible from another thread.
- "THREAD-ISOLATED": In addition to "MULTITHREADED", different variable bindings are maintained for each thread.
- "STATELESS": In addition to "THREAD-ISOLATED", scripts do not alter variable bindings.

You will often want to add variable bindings to the engine. A binding consists of a name and an associated Java object. For example, consider these statements:

```java
engine.put("k", 1728);
Object result = engine.eval("k + 1");
```

The script code reads the definition of k from the bindings in the “engine scope.” This is particularly important because most scripting languages can access Java objects, often with a syntax that is simpler than the Java syntax. For example,

```java
engine.put("b", new JButton());
engine.eval("b.text = \"OK\"");
```

Conversely, you can retrieve variables that were bound by scripting statements:

```java
engine.eval("n = 1728");
Object result = engine.get("n");
```

In addition to the engine scope, there is also a global scope. Any bindings that you add to the ScriptEngineManager are visible to all engines.

Instead of adding bindings to the engine or global scope, you can collect them in an object of type `Bindings` and pass it to the `eval` method:

```java
Bindings scope = engine.createBindings();
scope.put("b", new JButton());
engine.eval(script, scope);
```

This is useful if a set of bindings should not persist for future calls to the eval method.

> **NOTE:** You might want to have scopes other than the engine and global scopes. For example, a web container might need request and session scopes. However, then you are on your own. You will need to write a class that implements the `ScriptContext` interface, managing a collection of scopes. Each scope is identified by an integer number, and scopes with lower numbers should be searched first. (The standard library provides a `SimpleScriptContext` class, but it only holds global and engine scopes.)

| `javax.script.ScriptEngine` | 6 |
|---|---|
| • `Object eval(String script)` | |
| • `Object eval(Reader reader)` | |
| • `Object eval(String script, Bindings bindings)` | |
| • `Object eval(Reader reader, Bindings bindings)` | |
| evaluates the script given by the string or reader, subject to the given bindings. | |
| • `Object get(String key)` | |
| • `void put(String key, Object value)` | |
| gets or puts a binding in the engine scope. | |
| • `Bindings createBindings()` | |
| creates an empty Bindings object suitable for this engine. | |

| `javax.script.ScriptEngineManager` | 6 |
|---|---|
| • `Object get(String key)` | |
| • `void put(String key, Object value)` | |
| gets or puts a binding in the global scope. | |

### 8.1.5 Compiling a Script

Some scripting engines can compile scripting code into an intermediate form for efficient execution. Those engines implement the `Compilable` interface. The following example shows how to compile and evaluate code contained in a script file:

```java
Reader reader = new FileReader("myscript.js");
CompiledScript script = null;
if (engine instanceof Compilable)
    script = ((Compilable) engine).compile(reader);
```

Once the script is compiled, you can execute it. The following code executes the compiled script if compilation was successful, or the original script if the engine didn't support compilation:

```java
if (script != null)
    script.eval();
else
    engine.eval(reader);
```

Of course, it only makes sense to compile a script if you need to execute it repeatedly.

| `javax.script.Compilable` 6 |
|---|
| • `CompiledScript compile(String script)`<br>• `CompiledScript compile(Reader reader)`<br><br>compiles the script given by a string or reader. |

| `javax.script.CompiledScript` 6 |
|---|
| • `Object eval()`<br>• `Object eval(Bindings bindings)`<br><br>evaluates this script |

### 8.1.6 An Example: Scripting GUI Events

To illustrate the scripting API, we will write a sample program that allows users to specify event handlers in a scripting language of their choice.

Have a look at the program in Listing 8.1 that adds scripting to an arbitrary frame class. By default it reads the `ButtonFrame` class in Listing 8.2, which is similar to the event handling demo in Volume I, with two differences:

- Each component has its name property set.
- There are no event handlers.

The event handlers are defined in a property file. Each property definition has the form

*componentName.eventName* = *scriptCode*

For example, if you choose to use JavaScript, supply the event handlers in a file js.properties, like this:

```properties
yellowButton.action=panel.background = java.awt.Color.YELLOW
blueButton.action=panel.background = java.awt.Color.BLUE
redButton.action=panel.background = java.awt.Color.RED
```

The companion code also has files for Groovy, R, and SISC Scheme.

The program starts by loading an engine for the language specified on the command line. If no language is specified, we use JavaScript.

We then process a script init.language if it is present. This is useful for the R and Scheme languages, which need some initializations that we did not want to include in every event handler script.

Next, we recursively traverse all child components and add the bindings (*name*, *object*) into a map of components. Then we add the bindings to the engine.

Next, we read the file *language.properties*. For each property, we synthesize an event handler proxy that causes the script code to be executed. The details are a bit technical. You might want to read the section on proxies in Volume I, Chapter 6, if you want to follow the implementation in detail. The essential part, however, is that each event handler calls

```java
engine.eval(scriptCode);
```

Let us look at the yellowButton in more detail. When the line

```properties
yellowButton.action=panel.background = java.awt.Color.YELLOW
```

is processed, we find the JButton component with the name "yellowButton". We then attach an ActionListener with an actionPerformed method that executes the script

```java
panel.background = java.awt.Color.YELLOW
```

if the scripting is done with Nashorn.

The engine contains a binding that binds the name "panel" to the JPanel object. When the event occurs, the setBackground method of the panel is executed, and the color changes.

You can run this program with the JavaScript event handlers simply by executing

```java
69   }
70
71   /**
72    * Gathers all named components in a container.
73    * @param c the component
74    * @param namedComponents a map into which to enter the component names and components
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
88    * Adds a listener to an object whose listener method executes a script.
89    * @param beanName the name of the bean to which the listener should be added
90    * @param eventName the name of the listener type, such as "action" or "change"
91    * @param scriptCode the script code to be executed
92    * @param engine the engine that executes the code
93    * @param bindings the bindings for the execution
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

*(Continues)*
