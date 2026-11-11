# **java.lang.reflect.InvocationHandler** 1.3

+   - `Object invoke(Object proxy, Method method, Object[] args)`
+   
+     define this method to contain the action that you want carried out whenever a method was invoked on the proxy object.
+   
+   - `static Object invokeDefault(Object proxy, Method method, Object... args)` 16
+   
+     Invokes a default method of the proxy instance with the given arguments, bypassing the invocation handler.

# **java.lang.reflect.Proxy** 1.3

+   - `static Class<?> getProxyClass(ClassLoader loader, Class<?>... interfaces)`
+   
+     returns the proxy class that implements the given interfaces.
+   
+   - `static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces, InvocationHandler handler)`
+   
+     constructs a new instance of the proxy class that implements the given interfaces. All methods call the invoke method of the given handler object.
+   
+   - `static boolean isProxyClass(Class<?> cl)`
+   
+     returns true if cl is a proxy class.

This ends the final chapter on the object-oriented features of the Java programming language. Interfaces, lambda expressions, and inner classes are concepts that you will encounter frequently, whereas cloning, service loaders, and proxies are advanced techniques that are of interest mainly to library designers and tool builders, not application programmers. You are now ready to learn how to deal with exceptional situations in your programs in [Chapter 7](#).