| `java.util.Random` | `1.0` |
|---|---|
| • `Random()`<br>constructs a new random number generator. | |
| • `int nextInt(int n)` | `1.2`<br>returns a random number between 0 and n − 1. |

# 4.6.8 Object Destruction and the finalize Method

Some object-oriented programming languages, notably C++, have explicit destructor methods for any cleanup code that may be needed when an object is no longer used. The most common activity in a destructor is reclaiming the memory set aside for objects. Since Java does automatic garbage collection, manual memory reclamation is not needed, so Java does not support destructors.

Of course, some objects utilize a resource other than memory, such as a file or a handle to another object that uses system resources. In this case, it is important that the resource be reclaimed and recycled when it is no longer needed.

If a resource needs to be closed as soon as you have finished using it, supply a close method that does the necessary cleanup. You can call the close method when you are done with the object. In Chapter 7, you will see how you can ensure that this method is called automatically.

If you can wait until the virtual machine exits, add a “shutdown hook” with the method `Runtime.addShutdownHook`. As of Java 9, you can use the Cleaner class to register an action that is carried out when an object is no longer reachable (other than by the cleaner). These are uncommon situations in practice. See the API documentation for details on these two approaches.

> **CAUTION:** Do not use the finalize method for cleanup. That method was intended to be called before the garbage collector sweeps away an object. However, you simply cannot know when this method will be called, and it is now deprecated.

# 4.7 Packages

Java allows you to group classes in a collection called a package. Packages are convenient for organizing your work and for separating your work from code