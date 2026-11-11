on the problem that we want to solve with the proxy mechanism. Proxies
can be used for many purposes, such as

+   - Routing method calls to remote servers
+   - Associating user interface events with actions in a running program
+   - Tracing method calls for debugging purposes

In our example program, we use proxies and invocation handlers to trace
method calls. We define a TraceHandler wrapper class that stores a wrapped
object. Its invoke method simply prints the name and parameters of the method
to be called and then calls the method with the wrapped object as the implicit
parameter.

```
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
```

Here is how you construct a proxy object that causes the tracing behavior
whenever one of its methods is called:

```
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
```

Now, whenever a method from one of the interfaces is called on proxy, the
method name and parameters are printed out and the method is then invoked
on value.