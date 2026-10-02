
```java
public static void main(String[] args)
{
    int a[] = new int[10];
    for (int i=0; i<10; i++)
        a[i]=i;
    dump(a);
}
```

```java
public static void main(java.lang.String[])
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=3, args_size=1
0: bipush 10
2: newarray int
4: astore_1
5: iconst 0
6: istore_2
7: iload_2
8: bipush 10
10: if_icmpge 23
13: aload 1
14: istore_2
15: iload_2
16: iconst
17: linc 2, 1
20: goto 7
23: aload 1
24: invokestatic #4 // Method dump:([I)V
27: return
```

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮件。谢谢！

## 862

```
8: getstatic      #2 // Field java/lang/System.out:Ljava/io/
PrintStream:
11: aload_0
12: aload_1
13: iaload
14: invokevirtual #3 // Method java/io/PrintStream.println(I)
17: iinc           1, 11
20: goto           2
23: return
```

传入的引用位于 0 号槽位。

源代码中的长度表达式会被转换为 `array_length` 指令：它接收一个数组引用，并将数组的大小留在栈顶（TOS）上。

在偏移量 13 处的 `aload` 用于加载数组元素，此时栈中应存在一个数组引用（由偏移量 11 处的 `aload_0` 准备）以及一个索引（由偏移量 12 处的 `aload_1` 准备）。

不用多说，带有错误的指令可能会被误认为是数组指令。

这是不对的。这些指令是与对象引用工作的。

而且数组和字符串也是对象。

## 数组元素的求和

另一个示例：

```java
public class ArraySum {
    public static int f (int[] a) {
        int sum=0;
        for (int i=0; i<a.length; i++)
            sum=sum+a[i];
        return sum;
    }
}
```

```
public static int f(int[]) {
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, args_size=1
0: const_0
1: istore_1
2: const_0
3: istore_2
4: iload_0
5: aload_0
6: arraylength
7: if_icmpmp
22
```

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

## 863

```
10: iload_1
11: aload_0
12: iload_2
13: iaload
14: iadd
15: istore_1
16: iinc        2, 1
19: goto        4
22: iload_1
23: ireturn
```

LVA 槽位 0 包含输入数组的引用。

LVA 槽位 1 包含局部变量 sum。

## main() 函数的唯一参数也是一个数组

我们将使用 `main()` 函数的唯一参数，它是一个字符串数组：

```java
public class UseArgument
{
    public static void main(String[] args)
{
        System.out.print("Hi", );
        System.out.print(args[1]);
        System.out.println(" How are you?");
    }
}
```

0 号参数是程序的名称（类似于 C/C++ 等），用户提供的第 1 个参数是 1。

```
public static void main(java.lang.String[])
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=1, args_size=1
    0: static              // Field java/lang/System.out:Ljava/io/
PrintStream:
        3: idc                 #3 // String .
        5: invokevirtual #4 // Method java/io/PrintStream.print:(
    Ljava/lang/String;V
        6: static              // Field java/lang/System.out:Ljava/io/
PrintStream:
        11: aload_0
        12: istore_1
        13: aload
        14: invokevirtual #4 // Method java/io/PrintStream.print:(
    Ljava/lang/String;V
        17: static              // Field java/lang/System.out:Ljava/io/
PrintStream:
        20: idc                 #5 // String . How are you?
        22: invokevirtual #6 // Method java/io/PrintStream.println:(
    Ljava/lang/String;V)
```

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

## 25: return

11 处的 `aload 0` 加载了第 0 个 LVA 槽位的引用（第一个也是唯一的 `main()` 参数）。

`iconst 1` 以及 `aaload 12 和 13` 获取数组的第一个（从 0 开始计数）元素。

字符串对象的引用位于偏移量 14 处的 TOS，并由 `println` 方法从那里获取。

## 预初始化的字符串数组

```java
class Month {
    public static String[] months = {
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
    };
    public String get_month(int i) {
        return months[i];
    }
}
```

`get_month()` 函数非常简单：

```
public java.lang.String get_month(int i);
flags: ACC PUBLIC
Code:
stack=2,locals=2, args_size=2
0: getstatic #2 Field months:[java/lang/String;
3: iload 1
4: aaload
5: areturn
```

`aaload` 作用于引用数组，因此这些指令用于对它们进行操作。

Java 返回一个 String 对象的引用。

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

## months[] 是如何初始化的？

```
static {}
flags: ACC STATIC
Code:
stack=4, locals=0, args_size=0
```

```
0: bipush
2: anewarray # // class java/lang/String
5: dup
6: iconst_0
7: ldc #4 // January
9: aastore
10: dup
11: iconst_1
12: ldc #5 // February
14: aastore
15: dup
16: iconst_2
17: ldc #6 // March
19: aastore
20: dup
21: iconst_3
22: ldc #7 // April
24: aastore
25: dup
26: iconst_4
27: ldc #8 // May
29: aastore
30: dup
31: iconst_5
32: ldc #6 // June
34: aastore
35: dup
36: bipush
38: ldc #7 // July
40: aastore
41: dup
42: bipush
44: ldc #8 // August
46: aastore
47: dup
48: bipush
50: ldc #9 // September
52: aastore
53: dup
54: bipush
56: ldc #10 // October
58: aastore
59: dup
60: bipush
62: ldc #11 // November
64: aastore
65: dup
66: bipush
68: ldc #12 // December
70: aastore
71: putstatic #2 // months:[L/String];
74: return
```

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

## 866

```
4: arraylength
5: ificmpge 2
8: getstatic      #2 // Field java/lang/System.out:Ljava/io/
PrintStream:
11: load 0
12: iaload
14: invokevirtual #3 // Method java/io/PrintStream.println(I)
17: iinc           1, 11
20: goto           2
23: return
```

`f()` 接收一个整数数组，使用偏移量 3。

然后它获取数组的大小等。

```
public static void main(java.lang.String[] args)
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=4, locals=1, args_size=1
0: bipush 123
2: istore 1
3: idc 2 #2 // double 123.456d
6: dstore 2
7: getstatic #4 // Field java/lang/System.out/java/
PrintStream;
10: idc 2 #5 // String int: %d double: %f.%n
12: icost 1
13: anewarray #6 // class java/lang/Object
16: dup
17: icost 0
18: iload 1
19: invokestatic #7 // Method java/lang/Integer.valueOf(I)
Ljava/lang/Integer;
22: aastore
23: dup
24: icost 1
25: iload 2
26: invokestatic #8 // Method java/lang/Double.valueOf(D)
Ljava/lang/Double;
29: aastore
30: invokevirtual #9 // Method java/io/PrintStream.format(Ljava/lang/Object;L)
33: pop
34: return
```

数组在 `main()` 中通过 `newarray` 指令构造，然后被填充，最后调用 `f()`。

噢，数组对象在 `main()` 结束时并没有销毁。

Java 中完全没有析构函数，因为 JVM 有垃圾回收器会在需要时自动完成这一点。

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

## format() 方法如何？

它接收两个参数：一个字符串和一个对象数组：

```
public PrintStream format(String format, Object... args)
```

让我们来看看：

```java
public static void main(String[] args) {
    int i=123;
    double d=123.456;
    System.out.format("%d: %f.\n", i, d);
}
```

```
public static void main(java.lang.String[]) {
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=7, locals=4, args_size=1
0: bipush 123
2: istore 1
3: idc 2 #2 // double 123.456d
6: dstore 2
7: getstatic #4 // Field java/lang/System.out/java/
PrintStream;
10: idc 2 #5 // String int: %d double: %f.%n
12: icost 1
13: anewarray #6 // class java/lang/Object
16: dup
17: icost 0
18: iload 1
19: invokestatic #7 // Method java/lang/Integer.valueOf(I)
Ljava/lang/Integer;
22: aastore
23: dup
24: icost 1
25: iload 2
26: invokestatic #8 // Method java/lang/Double.valueOf(D)
Ljava/lang/Double;
29: aastore
30: invokevirtual #9 // Method java/io/PrintStream.format(Ljava/lang/Object;L)
33: pop
34: return
```

# 869

另一方面，数组总是同质的，即它不能包含不同类型的元素，这使得无法向其中推送 int 和 double 值。

在偏移 13 处创建了一个 Object 对象的数组，在偏移 22 处向数组中添加了一个 Integer 对象，在偏移 29 处向数组中添加了一个 Double 对象。

倒数第二个 pop 指令丢弃栈顶（TOS）的元素，因此当执行 return 时，栈变为空（或恢复平衡状态）。

## 二维数组

Java 中的二维数组只是指向其他一维数组的引用的一维数组。

让我们创建一个二维数组：

```java
public static void main(String[] args)
{
    int[][] a = new int[5][10];
    a[1][2]=3;
}
```

```
public static void main(java.lang.String[]);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=2, args_size=1
0: iconst_5
1: bipush 10
3: multianarray #2, 2      // class "[[I"
7: astore 1
8: aload 1
9: iconst_1
10: aal
11: iconst_2
12: iconst_3
13: astore
14: return
```

它是使用 `multianewarray` 指令创建的：对象的类型和维度作为操作数传递。

数组的大小（10*5）被留在栈中（使用指令 `iconst_5` 和 `bipush`）。

加载到第 #1 行的引用在偏移 10 处加载（使用 `iconst_1` 和 `aaload`）。

列在偏移 11 处使用 `iconst_2` 选择。

要写入的值在偏移 12 处设置。

`astore` 写入数组的元素。

元素是如何访问的？

```java
public static int get12(int[][][] in)
{
    return in[1][2];
}
```

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。感谢！

870

```
public static int get12(int[][][]);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=2, locals=1, args_size=1
0: aload_0
1: iconst_1
2: aload_0
3: iconst_2
4: aload_0
5: ireturn
```

指向数组行的引用在偏移 2 处加载，列在偏移 3 处设置，然后 `iaload` 加载数组的元素。

## 三维数组

三维数组只是指向指向一维数组的引用的一维数组的一维数组。
