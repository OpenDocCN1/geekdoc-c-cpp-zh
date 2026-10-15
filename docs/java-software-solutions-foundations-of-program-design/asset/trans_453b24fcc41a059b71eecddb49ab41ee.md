

与其它位运算符一样，三个位移运算符操作整数值的各个位。它们都接受两个操作数。左操作数是其位被移位的数值；右操作数指定它们应移动的位置。在执行移位之前，byte 和 short 值会先被提升为 int，适用于所有移位运算符。此外，如果任一操作数是 long，则另一个操作数会被提升为 long。为了便于阅读，本节示例中仅使用 16 位，但概念在扩展到 32 位或 64 位串时是相同的。

移位时，一些位会从一端丢失，另一端需要填入新的位。左移运算符（<<）将位向左移，并用零填充右侧的位。例如，如果整数变量 number 当前的值为 13，则语句

```
number = number << 2;
```

会将值 52 存储到 number 中。最初，number 包含位串 000000000001101。左移后，值变为 000000000110100，即 52。请注意，每向左移一位，原值就乘以 2。

数值的符号位会随其它位一起移位。因此，如果移位足够多以改变符号位，值的符号可能会改变。例如，值 -8 以二进制补码形式存储为 1111111111111000。左移两位后，它变为 1111111111100000，即 -32。然而，如果移位的位置足够多，负数可能会变为正数，反之亦然。

右移运算符有两种形式：一种保留原始值的符号（>>），另一种用零填充最左边的位（>>>）。

让我们检查右移-带符号填充运算符的两个示例。如果 int 变量 number 当前的值为 39，则表达式 (number >> 2) 的结果为 9。number 中存储的原始位串为 0000000000100111，右移两位后的结果为 0000000000001001。最左边的符号位，在本例中为零，用于从左侧填充。

如果 number 的原始值为 -16，即 1111111111110000，则右移（带符号填充）表达式 (number >> 3) 的结果为二进制串 1111111111111110，即 -2。在本例中，最左边的符号位为 1，并用于填充新的左侧位，保持符号不变。

如果不希望保留符号，可以使用右移-零填充运算符（>>>）。它与 >> 运算符类似，但无论原始值的符号如何，都用零填充。

## Java Modifiers

本附录总结了赋予 Java 类、接口、方法及变量特定特征的修饰符。出于讨论目的，所有 Java 修饰符被分为两组：可见性修饰符和其它修饰符。

### Java Visibility Modifiers

图 E.1 中的表格描述了 Java 可见性修饰符对各种构造的影响。可视性修饰符对类和接口的作用相同，对方法和变量的作用相同。

默认可见性意味着没有显式使用可见性修饰符。默认可见性有时称为包可见性，但你不能使用保留字 package 作为修饰符。

请注意，只有内部类可以具有 private 或 protected 可见性。

| Modifier | Classes and interfaces | Methods and variables |
|---|---|---|
| default (no modifier) | Visible in its package. | Visible to any class in the same package as its class. |
| public | Visible anywhere. | Visible anywhere. |
| protected | Can only be applied to inner classes. Visible in its package and to classes that extend the class in which it is declared. | Visible to any class in the same package and to any derived classes. |
| private | Can only be applied to inner classes. Visible to the enclosing class only. | Not visible by any other class. |

FIGURE E.1 Java visibility modifiers

### Other Java Modifiers

图 E.3 总结了其余的 Java 修饰符，它们涉及各种问题。此外，修饰符对类、接口、方法及变量的效果不同。某些修饰符不能与特定构造一起使用，因此列为不适用（N/A）。

`transient` 修饰符用于指示在持久化（序列化）对象中无需存储的数据。也就是说，当对象写入序列化流时，对象表示将包含所有未指定为 transient 的数据。

| Modifier | Class | Interface | Method | Variable |
|---|---|---|---|---|
| `abstract` | The class may contain abstract methods. It cannot be instantiated. | All interfaces are inherently abstract. The modifier is optional. | No method body is defined. The method requires implementation when inherited. | N/A |
| `final` | The class cannot be used to drive new classes. | N/A | The method cannot be overridden. | The variable is a constant, whose value cannot be changed once initially set. |
| `native` | N/A | N/A | No method body is necessary since implementation is in another language. | N/A |
| `static` | N/A | N/A | Defines a class method. It does not require an instantiated object to be invoked. It cannot reference non-static methods or variables. It is implicitly final. | Defines a class variable. It does not require an instantiated object to be referenced. It is shared (common memory space) among all instances of the class. |
| `synchronized` | N/A | N/A | The execution of the method is mutually exclusive among all threads. | N/A |
| `transient` | N/A | N/A | N/A | The variable will not be serialized. |
| `volatile` | N/A | N/A | N/A | The variable is changed asynchronously. The compiler should not perform optimizations on it. |

**FIGURE E.3**  The rest of the Java modifiers

## Design Guidelines

- A. Design Preparation
- 1. The ultimate guideline is to develop a clean design. Think before you start coding. A working program is not necessarily a good program.
- 2. Express and document your design with consistent, clear notation.
- B. Structured Programming
- 1. Do not use the `continue` statement.
- 2. Use the `break` statement only to terminate cases of a `switch` statement.
- 3. Have only one `return` statement in a method as the last line, unless it unnecessarily complicates the method.
- C. Classes and Packages
- 1. Do not have additional methods in the class that contains the `main` method.
- 2. Define the class that contains the `main` method at the top of the file it is in, followed by other classes if appropriate.
- 3. If only one class is used from an imported package, import that class by name. If two or more are imported, use the * symbol.
- D. Modifiers
- 1. Do not declare variables with `public` visibility.
- 2. Do not use modifiers inside an interface.
- 3. Always use the most appropriate modifiers for each situation. For example, if a variable is used as a constant, explicitly declare it as a constant using the `final` modifier.
- E. Exceptions
- 1. Use exception handling only for truly exceptional conditions, such as terminating errors, or for significantly unusual or important situations.
- 2. Do not use exceptions to disguise or hide inappropriate processing.
- 3. Handle each exception at the appropriate level of design.
- F. Miscellaneous
- 1. Use constants instead of literals in almost all situations.
- 2. Design methods so that they perform one logical function. As such, the length of a method will tend to be no longer than 50 lines of code, and usually much shorter.
- 3. Keep the physical lines of a source code file to less than 80 characters in length.
- 4. Extend a logical line of code over two or more physical lines only when necessary. Divide the line at a logical place.

