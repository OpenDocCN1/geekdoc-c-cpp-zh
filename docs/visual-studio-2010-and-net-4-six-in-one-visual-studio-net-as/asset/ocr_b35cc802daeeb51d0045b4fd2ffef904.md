These synchronization primitives play an important role in TPL implementation. They are heavily used, and significantly contribute to the great performance of TPL.

# Lazy Initialization Classes

Postponing initialization of type members until they are needed is a frequently used programming pattern. It is especially useful when initialization is expensive by means of consumed CPU cycles, memory, or other resources. Lazy initialization classes listed in Table 10-7 help you in these scenarios.

**TABLE 10-7:** Lazy Initialization Types

| TYPE NAME | DESCRIPTION |
| --- | --- |
| System.Lazy<T> | This class provides support for lazy initialization of a T instance. When you create an instance of Lazy<T>, it does not instantiate T. You can access the instance behind Lazy<T> using its Value property. Lazy initialization occurs the first time the Lazy<T>.Value property is accessed, or the Lazy<T>.ToString method is called. |
| System.Threading.LazyInitializer | This static class provides lazy initialization routines. .NET Framework 4.0, you can use a few overloads of the EnsureInitialized method. In the future, the class may be extended with more helper methods. In scenarios where you might lazy-initialize a number of objects, you might decide that wrapping each object in a Lazy<T> requires too much memory, or too many computing resources. Or, you might have stringent requirements about how lazy initialization is exposed. In such cases, you can use the static EnsureInitialized methods to lazy-initialize each object without wrapping it in an instance of Lazy<T>. |
| System.Threading.ThreadLocal<T> | This class provides thread-local storage of data type T. Although this class lazy initialization in its implementation, "laziness" isn't its main functionality. By providing an instance of ThreadLocal<T>, you can be sure that the T instance accessed through the Value property is shared within the thread it created. Its role is similar to the role of the ThreadStatic attribute used to decorate static fields in order to have thread-local behavior. However, ThreadLocal<T> provides better performance. |