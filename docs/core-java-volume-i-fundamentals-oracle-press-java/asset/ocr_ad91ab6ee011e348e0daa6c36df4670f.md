+   - The `TypeVariable` interface, describing type variables (such as `T extends Comparable<? super T>`)
+   - The `WildcardType` interface, describing wildcards (such as `? super T`)
+   - The `ParameterizedType` interface, describing generic class or interface types (such as `Comparable<? super T>`)
+   - The `GenericArrayType` interface, describing generic arrays (such as `T[]`)

Figure 8.5 shows the inheritance hierarchy. Note that the last four subtypes are interfaces—the virtual machine instantiates suitable classes that implement these interfaces.

![](bbox=[0.13, 0.36, 0.86, 0.63])

**Figure 8.5** The Type interface and its descendants

Listing 8.4 uses the generic reflection API to print out what it discovers about a given class. If you run it with the `Pair` class, you get this report:

```
```java
class Pair<T> extends java.lang.Object
public T getFirst()
public T getSecond()
public void setFirst(T)
public void setSecond(T)
```
```