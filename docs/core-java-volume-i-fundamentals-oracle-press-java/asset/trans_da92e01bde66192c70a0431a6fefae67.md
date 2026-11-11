

```java
/**
 * Prints all directly implemented interfaces of a class
 * @param cl a class
 */
public static void printInterfaces(Class cl)
{
    Class<?>[] interfaces = cl.getInterfaces();
    for (int i = 0; i < interfaces.length; i++)
    {
        if (i == 0)
            System.out.print(cl.isInterface() ? " extends " : " implements ");
        else
            System.out.print(", ");
        System.out.print(interfaces[i].getName());
    }
}
```

### java.lang.Class 1.0

- `Field[] getFields()` 1.1
- `Field[] getDeclaredFields()` 1.1

  `getFields` 返回一个数组，其中包含此类或其超类的公共字段的 `Field` 对象；`getDeclaredFields` 返回一个数组，其中包含此类的所有字段的 `Field` 对象。如果没有此类字段，或者类对象表示基本类型或数组类型，则这些方法返回长度为 0 的数组。

- `Method[] getMethods()` 1.1
- `Method[] getDeclaredMethods()` 1.1

  返回一个包含 `Method` 对象的数组：`getMethods` 返回公共方法并包括继承的方法；`getDeclaredMethods` 返回此类或接口的所有方法，但不包括继承的方法。

- `Constructor[] getConstructors()` 1.1
- `Constructor[] getDeclaredConstructors()` 1.1

  返回一个包含构造器对象的数组，这些对象给出此 `Class` 对象所表示类的所有公共构造器（对于 `getConstructors`）或所有构造器（对于 `getDeclaredConstructors`）。

- `isInterface()`

  如果此 `Class` 对象描述的是 `interface`，则返回 true。（关于接口，请参见[第6章](#)。）

- `isEnum()` 1.5

  如果此 `Class` 对象描述的是 `enum`，则返回 true。

- `isRecord()` 16

  如果此 `Class` 对象描述的是 `record`，则返回 true。

- `RecordComponent[] getRecordComponents()` 16

  返回一个由 `RecordComponent` 对象组成的数组，这些对象描述记录字段；如果此类不是记录，则返回 null。

- `String getPackageName()` 9

  获取包含此类型的包的名称；如果此类型是数组类型，则获取元素类型的包；如果此类型是基本类型，则获取 "java.lang"。

### `java.lang.reflect.Field` 1.1

### `java.lang.reflect.Method` 1.1

### `java.lang.reflect.Constructor` 1.1

- `Class getDeclaringClass()`

  返回定义此构造器、方法或字段的类的类对象。

- `Class[] getExceptionTypes()`（在 `Constructor` 和 `Method` 类中）

  返回一个类对象数组，这些类对象表示该方法抛出的异常类型。

- `int getModifiers()`

  返回一个整数，描述此构造器、方法或字段的修饰符。使用 `Modifier` 类中的方法分析返回值。

- `String getName()`

  返回一个字符串，即构造器、方法或字段的名称。

- `Class[] getParameterTypes()`（在 `Constructor` 和 `Method` 类中）

  返回一个类对象数组，这些类对象表示参数的类型。

- `Class getReturnType()`（在 `Method` 类中）

  返回一个表示返回类型的类对象。

### `java.lang.reflect.RecordComponent` 16

- `String getName()`
- `Class<?> getType()`

  获取此记录组件的名称和类型。

- `Method getAccessor()`

  返回用于访问此记录组件的 `Method` 对象。

### `java.lang.reflect.Modifier` 1.1

- `static String toString(int modifiers)`

  返回一个字符串，其中包含与 `modifiers` 中设置的位相对应的修饰符。

- `static boolean isAbstract(int modifiers)`
- `static boolean isFinal(int modifiers)`
- `static boolean isInterface(int modifiers)`
- `static boolean isNative(int modifiers)`
- `static boolean isPrivate(int modifiers)`
- `static boolean isProtected(int modifiers)`
- `static boolean isPublic(int modifiers)`
- `static boolean isStatic(int modifiers)`
- `static boolean isStrict(int modifiers)`
- `static boolean isSynchronized(int modifiers)`
- `static boolean isVolatile(int modifiers)`

  测试 `modifiers` 值中与方法名中的修饰符相对应的位。

## 5.9.5 使用反射在运行时分析对象

在上一节中，我们了解了如何找出任意对象实例字段的*名称*和*类型*：

- 获取对应的 `Class` 对象。
- 在类对象上调用 `getDeclaredFields`。

在本节中，我们将更进一步，实际查看字段的*内容*。当然，查看一个在编写程序时名称和类型已知的对象的特定字段的内容很容易。但反射允许你查看在编译时未知的对象的字段。

实现这一点的关键方法是 `Field` 类中的 `get` 方法。如果 `f` 是 `Field` 类型的对象（例如，从 `getDeclaredFields` 获得的对象），而 `obj` 是 `f` 所表示字段所属类的对象，那么 `f.get(obj)` 返回一个对象，其值是 `obj` 的该字段的当前值。这一切有点抽象，所以我们来看一个示例。

```java
var harry = new Employee("Harry Hacker", 50000, 10, 1, 1989);
Class cl = harry.getClass();
    // the class object representing Employee
Field f = cl.getDeclaredField("name");
    // the name field of the Employee class
Object v = f.get(harry);
    // the value of the name field of the harry object, i.e.,
    // the String object "Harry Hacker"
```

当然，你也可以设置能够获取的值。调用 `f.set(obj, value)` 会将对象 `obj` 中由 `f` 表示的字段设置为新值。

实际上，这段代码有一个问题。由于 `name` 字段是私有字段，`get` 和 `set` 方法将抛出 `IllegalAccessException`。你只能对可访问的字段使用 `get` 和 `set`。Java 的安全机制允许你找出对象有哪些字段，但除非你有权限，否则它不允许你读取和写入这些字段的值。

反射机制的默认行为是遵循 Java 访问控制。但是，你可以通过在 `Field`、`Method` 或 `Constructor` 对象上调用 `setAccessible` 方法来覆盖访问控制。例如：

```java
f.setAccessible(true); // now OK to call f.get(harry)
```

`setAccessible` 方法是 `AccessibleObject` 类的方法，而 `AccessibleObject` 是 `Field`、`Method` 和 `Constructor` 类的共同超类。此功能是为调试器、持久化存储和类似机制提供的。我们将在本节后面将它用于一个通用的 `toString` 方法。

如果未授予访问权限，调用 `setAccessible` 会抛出异常。访问权限可能被模块系统（第二卷[第9章](#)）或安全管理器（第二卷[第10章](#)）拒绝。安全管理器的使用并不常见，并且自 Java 17 起已被弃用。但是，从 Java 9 开始，由于 Java API 已模块化，每个程序都包含模块。

例如，本节末尾的示例程序会查看 `ArrayList` 和 `Integer` 对象的内部结构。当你在 Java 9 到 Java 16 中运行它时，会出现以下不祥消息：

```text
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by
objectAnalyzer.ObjectAnalyzer (file:/home/cay
    /books/cj11/code/v1ch05/bin/) to field
java.util.ArrayList.serialVersionUID
WARNING: Please consider reporting this to the maintainers of
    objectAnalyzer.ObjectAnalyzer
WARNING: Use --illegal-access=warn to enable warnings of
    further illegal reflective access operations
WARNING: All illegal access operations will be denied in a
    future release
```

当你使用 Java 17 运行该程序时，会发生 `InaccessibleObjectException` 异常。

为了让程序继续运行，请将 `java.base` 模块中的 `java.util` 和 `java.lang` 包“开放”给“未命名模块”。详细信息见第二卷[第9章](#)。语法如下：

```text
java --add-opens java.base/java.util=ALL-UNNAMED \
    --add-opens java.base/java.lang=ALL-UNNAMED \
    objectAnalyzer.ObjectAnalyzerTest
```

![](img/0e7b74ef51a065c077b42cd87b362288_433_0.png)

**注意：**

