
```java
for (int j = 0; j < paramTypes.length; j++)
{
   if (j > 0) System.out.print(", ");
   System.out.print(paramTypes[j].getName());
}
System.out.println(");");
}
}

/**
 * Prints all fields of a class
 * @param cl a class
 */
public static void printFields(Class cl)
{
   Field[] fields = cl.getDeclaredFields();

   for (Field f : fields)
   {
      Class type = f.getType();
      String name = f.getName();
      System.out.print(" ");
      String modifiers = Modifier.toString(f.getModifiers());
      if (modifiers.length() > 0) System.out.print(modifiers + " ");
      System.out.println(type.getName() + " " + name + ";");
   }
}
}
```

| java.lang.Class 1.0 |
|---|
| • `Field[] getFields()` 1.1<br>• `Field[] getDeclaredFields()` 1.1<br><br>getFields 返回一个数组，包含此类或其超类的公共字段的 Field 对象；getDeclaredFields 返回此类所有字段的 Field 对象数组。如果没有这样的字段，或者 Class 对象表示基本类型或数组类型，这些方法返回长度为 0 的数组。<br><br>• `Method[] getMethods()` 1.1<br>• `Method[] getDeclaredMethods()` 1.1<br><br>返回一个包含 Method 对象的数组：getMethods 返回公共方法并包含继承的方法；getDeclaredMethods 返回此类或接口的所有方法，但不包含继承的方法。 |

### java.lang.Class 1.0（续）

- `Constructor[] getConstructors()` 1.1
- `Constructor[] getDeclaredConstructors()` 1.1

  返回一个数组，包含 Constructor 对象，这些对象给出此 `Class` 对象所表示类的所有公共构造器（对于 `getConstructors`）或所有构造器（对于 `getDeclaredConstructors`）。

- `String getPackageName()` 9

  获取包含此类型的包名；如果此类型是数组类型，则获取元素类型的包名；如果这是基本类型，则返回 `"java.lang"`。

### java.lang.reflect.Field 1.1
### java.lang.reflect.Method 1.1
### java.lang.reflect.Constructor 1.1

- `Class getDeclaringClass()`

  返回定义此构造器、方法或字段的类的 Class 对象。

- `Class[] getExceptionTypes()`（在 Constructor 和 Method 类中）

  返回一个 Class 对象数组，表示该方法抛出的异常类型。

- `int getModifiers()`

  返回一个整数，描述此构造器、方法或字段的修饰符。使用 `Modifier` 类中的方法分析返回值。

- `String getName()`

  返回一个字符串，即构造器、方法或字段的名称。

- `Class[] getParameterTypes()`（在 Constructor 和 Method 类中）

  返回一个 Class 对象数组，表示参数的类型。

- `Class getReturnType()`（在 Method 类中）

  返回一个表示返回类型的 Class 对象。

### java.lang.reflect.Modifier 1.1

- `static String toString(int modifiers)`

  返回一个字符串，包含与 `modifiers` 中设置的位对应的修饰符。

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

  测试 modifiers 值中与方法名中的修饰符对应的位。

## 5.7.5 使用反射在运行时分析对象

在上一节中，我们看到了如何找出任何对象的数据字段的*名称*和*类型*：

- 获取对应的 `Class` 对象。
- 在 `Class` 对象上调用 `getDeclaredFields`。

在本节中，我们将更进一步，实际查看字段的*内容*。当然，查看一个在编写程序时已知名称和类型的对象的特定字段的内容很容易。但反射让你可以查看编译时未知的对象的字段。

实现这一点的关键方法是 `Field` 类中的 `get` 方法。如果 `f` 是一个 `Field` 类型的对象（例如，从 `getDeclaredFields` 获得的对象），而 `obj` 是 `f` 作为其字段的类的对象，那么 `f.get(obj)` 返回一个对象，其值为 `obj` 的该字段的当前值。这有点抽象，所以我们来看一个例子。

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

实际上，这段代码有一个问题。由于 `name` 字段是私有字段，`get` 和 `set` 方法将抛出 `IllegalAccessException`。你只能对可访问的字段使用 `get` 和 `set`。Java 的安全机制让你可以找出对象有哪些字段，但除非你有权限，否则它不会让你读取和写入这些字段的值。

反射机制的默认行为是遵循 Java 访问控制。但是，你可以通过在 `Field`、`Method` 或 `Constructor` 对象上调用 `setAccessible` 方法来覆盖访问控制。例如：

```java
f.setAccessible(true); // now OK to call f.get(harry)
```

`setAccessible` 方法是 `AccessibleObject` 类的方法，而 `AccessibleObject` 类是 `Field`、`Method` 和 `Constructor` 类的公共超类。此功能是为调试器、持久化存储和类似机制提供的。我们在本节后面会将其用于一个通用的 `toString` 方法。

如果未授予访问权限，调用 `setAccessible` 会抛出异常。访问可能被模块系统（第 II 卷第 9 章）或安全管理器（第 II 卷第 10 章）拒绝。安全管理器的使用并不常见。然而，从 Java 9 开始，由于 Java API 已模块化，每个程序都包含模块。

由于许多库都使用反射，Java 9 和 10 在你使用反射访问模块内的非公共特性时只会给出警告。例如，本节末尾的示例程序会查看 `ArrayList` 和 `Integer` 对象的内部结构。运行该程序时，控制台中会出现以下不祥消息：

```
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by objectAnalyzer.ObjectAnalyzer (file:/home/cay
/books/c11/code/v1ch05/bin/) to field java.util.ArrayList.serialVersionUID
WARNING: Please consider reporting this to the maintainers of
objectAnalyzer.ObjectAnalyzer
WARNING: Use --illegal-access=warn to enable warnings of further illegal
reflective access operations
WARNING: All illegal access operations will be denied in a future release
```

目前，你可以停用该警告。你需要将 `java.base` 模块中的 `java.util` 和 `java.lang` 包“开放”给“未命名模块”。详细信息见第 II 卷第 9 章。语法如下：

```
java --add-opens java.base/java.util=ALL-UNNAMED \
    --add-opens java.base/java.lang=ALL-UNNAMED \
    objectAnalyzer.ObjectAnalyzerTest
```

或者，你可以通过运行以下命令来查看该程序在未来 Java 版本中的行为：

```
java --illegal-access=deny objectAnalyzer/ObjectAnalyzerTest
```

然后程序将直接失败并抛出 `IllegalAccessException`。

> **注意：** 未来的库可能会使用变量句柄而不是反射来读取和写入字段。`VarHandle` 类似于 `Field`。你可以使用它读取或写入特定类的任何实例的特定字段。但是，要获得 `VarHandle`，库代码需要一个 `Lookup` 对象：

```java
public Object getFieldValue(Object obj, String fieldName, Lookup lookup)
    throws NoSuchFieldException, IllegalAccessException
{
    Class<?> cl = obj.getClass();
    Field field = cl.getDeclaredField(fieldName);
    VarHandle handle = MethodHandles.privateLookupIn(cl, lookup)
        .unreflectVarHandle(field);
    return handle.get(obj);
}
```

> 只要 `Lookup` 对象是在拥有访问该字段权限的模块中生成的，这种方式就有效。该模块中的某个方法只需调用 `MethodHandles.lookup()`，就会生成一个封装调用者访问权限的对象。通过这种方式，一个模块可以授予另一个模块访问私有成员的权限。实际问题是，如何以最少的麻烦授予这些权限。

趁着我们还能这样做，让我们看一个适用于任何类的通用 `toString` 方法（见代码清单 5.15）。通用 `toString` 方法使用 `getDeclaredFields` 获取所有数据字段，并使用 `setAccessible` 便捷方法使所有字段可访问。对于每个字段，它获取名称和值。每个值通过递归调用 `toString` 转换为字符串。

通用 `toString` 方法需要处理几个复杂问题。引用循环可能导致无限递归。因此，`ObjectAnalyzer` 会跟踪已经访问过的对象。此外，要窥视数组内部，你需要一种不同的方法。你将在下一节了解详细信息。

你可以使用这个 `toString` 方法窥视任何对象的内部。例如，以下调用

```java
var squares = new ArrayList<Integer>();
for (int i = 1; i <= 5; i++) squares.add(i * i);
System.out.println(new ObjectAnalyzer().toString(squares));
```
