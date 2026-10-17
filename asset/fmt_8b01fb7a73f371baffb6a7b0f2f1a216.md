
## 多维数组示例

```java
public static void main(String[] args) {
  int[][][] a = new int[5][10][15];

  a[1][2][3] = 4;

  get_elem(a);
}
```

```
public static void main(java.lang.String[][]);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=2, args_size=1
0: iconst_5
1: bipush 10
2: bipush 15
3: multianewarray #2, 3 // class "[[[I"
9: astore_1
10: aload_1
11: iconst_1
12: aload_0
13: iconst_2
14: aload_0
15: iconst_3
16: iconst_4
17: iastore
18: aload_1
19: invokestatic #3 // Method get_elem:([[[I)I
22: pop
23: return
```

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。感谢！

现在需要两个 `aaload` 指令来找到正确的引用：

```java
public static int get_elem(int[][][] a) {
    return a[1][2][3];
}
```

```
public static int get_elem(int[][][]);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=2, locals=1, args_size=1
0: aload_0
1: iconst_1
2: aaload
3: iconst_2
4: aaload
5: iconst_3
6: iaload
7: ireturn
```

## 总结

Java 中可能发生缓冲区溢出吗？

不，因为数组长度始终存在于数组对象中，边界受控制的，并且在越界访问时会抛出异常。

Java 中没有 C/C++ 意义上的多维数组，因此 Java 并不适用于快速的科学计算。

## 4.1.14 字符串

### 第一个示例

字符串是对象，构造方式与其他对象（以及数组）相同。

```java
public static void main(String[] args) {
    System.out.println("What is your name?");
    String input = System.console().readLine();
    System.out.println("Hello, " + input);
}
```

```
public static void main(java.lang.String[])
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=2, args_size=1
0: getstatic // Field java/lang/System.out:java/io/PrintStream
1: ldc #3 String is your name?
3: invokevirtual #4 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
5: aload_0
6: invokestatic #5 // Method java/lang/System.console():Ljava/io/Console;
7: astore_1
8: aload_1
9: invokevirtual #6 // Method java/io/Console.readLine():Ljava/lang/String;
10: astore_2
11: getstatic // Field java/lang/System.out:java/io/PrintStream;
12: ldc #2 "Hello, "
13: aload_2
14: new // class java/lang/StringBuilder
15: dup
16: invokespecial #8 // Method java/lang/StringBuilder.<init>()V
17: aload_2
18: invokevirtual #9 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
20: invokevirtual #10 // Method java/lang/StringBuilder.toString():Ljava/lang/String;
21: invokevirtual #11 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
22: return
```

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。感谢！

### 第二个示例

另一个示例：

```java
public class strings {
    public static char test(String a) {
        return a.charAt(3);
    }

    public static String concat(String a, String b) {
        return a + b;
    }
}
```

```
public static char test(java.lang.String);
```

如果你发现了拼写错误或有任何建议，请随时给我写信：我的邮箱。感谢！

873

字符串拼接是通过以下方式实现的：

```
public static java.lang.String concat(String a, String b)
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=2, locals=2, args_size=2
0: new // class java/lang/StringBuilder
1: dup
2: invokespecial #3 // Method <init>()
3: aload_0
4: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
5: aload_1
6: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
7: invokevirtual #6 // Method java/lang/StringBuilder.toString():Ljava/lang/String;
8: areturn
```

（注：原文示例代码中行号和指令略有出入或省略，此处保持原文逻辑翻译）

另一个示例：

```java
public static void main(String[] args) {
  String s = "Hello";
  int n = 123;
  System.out.println("s=" + s + " n=" + n);
}
```

再次，字符串使用 `StringBuilder` 类及其 `append` 方法构造，构造的字符串被传递给：

```
public static void main(java.lang.String[])
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=3, args_size=1
0: ldc #2 String Hello!
2: astore_1
3: bipush 123
5: istore_2
6: getstatic // Field java/lang/System.out:java/io/PrintStream;
7: new // class java/lang/StringBuilder
8: dup
9: invokespecial #5 // Method <init>()V
10: ldc #6 String s=
11: invokevirtual #7 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
13: aload_1
14: invokevirtual #7 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
15: ldc #7 String n=
16: invokevirtual #7 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
18: aload_2
19: invokevirtual #7 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;（注：此处原文索引号为_2，此处按逻辑对应）
20: invokevirtual #9 // Method java/lang/StringBuilder.toString():Ljava/lang/String;
21: invokevirtual #10 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
22: return
```

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。感谢！

## 4.1.15 异常

让我们重新思考一下我们的月份示例（第 864 页的 4.1.13）：

| 列表 4.10: IncorrectMonthException.java |
| --- |
| public class IncorrectMonthException extends Exception { |
| private int index; |
| public IncorrectMonthException(int index) { |
| this.index = index; |
| } |
| int getIndex() { |
| return index; |
| } } |

| 列表 4.11: Month2.java |
| --- |
| class Month2 { |
| public static String[] months = { |
| "January", |
| "February", |
| "March", |
| "April", |
| "May", |
| "June", |
| "July", |
| } } |

# 875

```
"August",
"September",
"October",
"November",
"December"
```

```java
public static String get_month(int i) throws IncorrectMonthException {
    if (i < 0 || i > 11)
        throw new IncorrectMonthException(i);
    return months[i];
}
public static void main(String[] args) {
    try {
        System.out.println(get_month(100));
    } catch (IncorrectMonthException e) {
        System.out.println("incorrect month index: " + e);
        e.printStackTrace();
    }
}
```

本质上，`IncorrectMonthException.class` 只有一个对象构造函数和一个 getter 方法。

`IncorrectMonthException` 类继承自 `Exception`，因此 `IncorrectMonthException` 构造函数首先调用 `Exception` 类的构造函数，然后将传入的整数值存入 `IncorrectMonthException` 类唯一的字段中：

```
public IncorrectMonthException(int i);
    flags: ACC_PUBLIC
Code:
    stack=2, locals=2, args_size=2
    0: aload_0
    1: invokespecial #1 // Method java/lang/Exception."<init>"()V
    3: aload_0
    4: iload_1
    5: putfield #2 // Field index:I
    6: return
```

`getIndex()` 仅仅是一个 getter。`IncorrectMonthException` 的引用被传递到零字节 LVA 槽（`this`），`aload_0` 获取了它，`getfield` 从对象加载一个整数值，`ireturn` 返回它。

如果你发现了任何拼写错误、错误或任何建议，请随时给我写信：我的邮箱。谢谢！

```
public int getIndex();
flags: ACC_PUBLIC
Code:
    stack=1, locals=1, args_size=1
0: aload_0
1: getfield #2 // Field index:I
4: ireturn
```

现在我们来看下 `Month2.class` 中的 `get_month()`：

### 列表 4.12: Month2.class

```java
public static java.lang.String get_month(int i) throws IncorrectMonthException;
flags: ACC_PUBLIC, ACC_STATIC
Code:
    stack=3, locals=1, args_size=1
0: iload_0
1: iflt 10
4: iload_0
5: bipush 11
7: if_icmple 19
10: new #2 // Class IncorrectMonthException
13: dup
14: iload_0
15: invokespecial #3 // Method IncorrectMonthException."<init>"(I)V
18: athrow
19: getstatic #4 // Field months:[Ljava/lang/String;
22: iload_0
23: aaload
24: areturn
```

偏移量 1 处的 `iflt` 表示小于。

在索引无效的情况下，将使用偏移量 10 处的 `new` 指令创建一个新对象。

对象的类型作为指令的操作数传递（即为 `IncorrectMonthException`）。它的构造函数被调用，索引通过 TOS（偏移量 14）传递。

当控制流到达偏移量 18 时，对象已经构造完成，因此现在 `athrow` 指令获取新构造对象的*引用*，并通知 JVM 寻找适当的异常处理器。

`athrow` 指令在此处不会返回控制流，因此在偏移量 19 处有另一个基本块，它与异常业务无关，我们可以从偏移量 7 到这里。

处理程序是如何工作的？

`Month2.class` 中的 `main()`。

### 列表 4.13: Month2.class
