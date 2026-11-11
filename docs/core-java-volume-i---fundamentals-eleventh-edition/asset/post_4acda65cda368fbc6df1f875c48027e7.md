
**`java.lang.reflect.Constructor<T>`** 1.1

- `T newInstance(Object... parameters)` returns a new instance constructed with the given parameters.

### 8.9.2 Using `Class<T>` Parameters for Type Matching

It is sometimes useful to match the type variable of a `Class<T>` parameter in a generic method. Here is the canonical example:

```java
public static <T> Pair<T> makePair(Class<T> c) throws InstantiationException,
    IllegalAccessException
{
    return new Pair<>(c.newInstance(), c.newInstance());
}
```

If you call

```java
makePair(Employee.class)
```

then `Employee.class` is an object of type `Class<Employee>`. The type parameter `T` of the `makePair` method matches `Employee`, and the compiler can infer that the method returns a `Pair<Employee>`.

### 8.9.3 Generic Type Information in the Virtual Machine

One of the notable features of Java generics is the erasure of generic types in the virtual machine. Perhaps surprisingly, the erased classes still retain some faint memory of their generic origin. For example, the raw `Pair` class knows that it originated from the generic class `Pair<T>`, even though an object of type `Pair` can't tell whether it was constructed as a `Pair<String>` or `Pair<Employee>`.

Similarly, consider a method

```java
public static Comparable min(Comparable[] a)
```

that is the erasure of a generic method

```java
public static <T extends Comparable<? super T>> T min(T[] a)
```

You can use the reflection API to determine that

- The generic method has a type parameter called `T`;
- The type parameter has a subtype bound that is itself a generic type;
- The bounding type has a wildcard parameter;
- The wildcard parameter has a supertype bound; and
- The generic method has a generic array parameter.

In other words, you can reconstruct everything about generic classes and methods that their implementors declared. However, you won't know how the type parameters were resolved for specific objects or method calls.

In order to express generic type declarations, use the interface `Type` in the `java.lang.reflect` package. The interface has the following subtypes:

- The `Class` class, describing concrete types
- The `TypeVariable` interface, describing type variables (such as `T extends Comparable<? super T>`)
- The `WildcardType` interface, describing wildcards (such as `? super T`)
- The `ParameterizedType` interface, describing generic class or interface types (such as `Comparable<? super T>`)
- The `GenericArrayType` interface, describing generic arrays (such as `T[]`)

Figure 8.5 shows the inheritance hierarchy. Note that the last four subtypes are interfaces—the virtual machine instantiates suitable classes that implement these interfaces.

![](img/127bccebb2cfadea3f02579edaad63c3_496_0.png)

**Figure 8.5** The `Type` interface and its descendants

Listing 8.4 uses the generic reflection API to print out what it discovers about a given class. If you run it with the `Pair` class, you get this report:

```
class Pair<T> extends java.lang.Object
public T getFirst()
public T getSecond()
public void setFirst(T)
public void setSecond(T)
```

**Listing 8.4** *(Continued)*

```java
42    System.out.print(cl);
43    printTypes(cl.getTypeParameters(), "<", ", ", ">", true);
44    Type sc = cl.getGenericSuperclass();
45    if (sc != null)
46    {
47        System.out.print(" extends ");
48        printType(sc, false);
49    }
50    printTypes(cl.getGenericInterfaces(), " implements ", ", ", "", false);
51    System.out.println();
52 }

54 public static void printMethod(Method m)
55 {
56    String name = m.getName();
57    System.out.print(Modifier.toString(m.getModifiers()));
58    System.out.print(" ");
59    printTypes(m.getTypeParameters(), "<", ", ", "> ", true);

61    printType(m.getGenericReturnType(), false);
62    System.out.print(" ");
63    System.out.print(name);
64    System.out.print("(");
65    printTypes(m.getGenericParameterTypes(), "", ", ", "", false);
66    System.out.println(")");
67 }
68 public static void printTypes(Type[] types, String pre, String sep, String suf,
69    boolean isDefinition)
70 {
71    if (pre.equals(" extends ") && Arrays.equals(types, new Type[] { Object.class }))
72        return;
73    if (types.length > 0) System.out.print(pre);
74    for (int i = 0; i < types.length; i++)
75    {
76        if (i > 0) System.out.print(sep);
77        printType(types[i], isDefinition);
78    }
79    if (types.length > 0) System.out.print(suf);
80 }

82 public static void printType(Type type, boolean isDefinition)
83 {
84    if (type instanceof Class)
85    {
86        var t = (Class<?>) type;
        System.out.print(t.getName());
    }
    else if (type instanceof TypeVariable)
    {
        var t = (TypeVariable<?>) type;
        System.out.print(t.getName());
        if (isDefinition)
            printTypes(t.getBounds(), " extends ", " & ", "", false);
    }
    else if (type instanceof WildcardType)
    {
        var t = (WildcardType) type;
        System.out.print("?");
        printTypes(t.getUpperBounds(), " extends ", " & ", "", false);
        printTypes(t.getLowerBounds(), " super ", " & ", "", false);
    }
    else if (type instanceof ParameterizedType)
    {
        var t = (ParameterizedType) type;
        Type owner = t.getOwnerType();
        if (owner != null)
        {
            printType(owner, false);
            System.out.print(".");
        }
        printType(t.getRawType(), false);
        printTypes(t.getActualTypeArguments(), "<", ", ", ">", false);
    }
    else if (type instanceof GenericArrayType)
    {
        var t = (GenericArrayType) type;
        System.out.print("");
        printType(t.getGenericComponentType(), isDefinition);
        System.out.print("[]");
    }
}
}
```

### 8.9.4 Type Literals

Sometimes, you want to drive program behavior by the type of a value. For example, in a persistence mechanism you may want the user to specify a way of saving an object of a particular class. This is typically implemented by associating the class object with an action.

However, with generic classes, erasure poses a problem. How can you have different actions for, say, `ArrayList<Integer>` and `ArrayList<String>` when both erase to the same raw `ArrayList` type?

There is a trick that can offer relief in some situations. You can capture an instance of the `Type` interface that you encountered in the preceding section. Construct an anonymous subclass like this:

```java
var type = new TypeLiteral<ArrayList<Integer>>() {} // note the {}
```

The `TypeLiteral` constructor captures the generic supertype:

```java
class TypeLiteral
{
    public TypeLiteral()
    {
        Type parentType = getClass().getGenericSuperclass();
        if (parentType instanceof ParameterizedType)
        {
            type = ((ParameterizedType) parentType).getActualTypeArguments()[0];
        }
        else
            throw new UnsupportedOperationException(
                "Construct as new TypeLiteral<...>(){}");
    }
    ...
}
```

If we have a generic type available at runtime, we can match it against the `TypeLiteral`. We can’t get a generic type from an object—it is erased. But, as you have seen in the preceding section, generic types of fields and method parameters survive in the virtual machine.

Injection frameworks such as CDI and Guice use type literals to control injection of generic types. The example program in the book’s companion code shows a simpler example. Given an object, we enumerate its fields, whose generic types are available, and look up associated formatting actions.

We format an `ArrayList<Integer>` by separating the values with spaces, an `ArrayList<Character>` by joining the characters to a string. Any other arrays are formatted by `ArrayList.toString`.

**Listing 8.5** `genericReflection/TypeLiterals.java`

```java
package genericReflection;

/**
 * @version 1.01 2018-04-10
 * @author Cay Horstmann
 */

import java.lang.reflect.*;
import java.util.*;
```
