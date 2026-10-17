
```java
public static void main(lang.String args[]);
    flags: ACC_PUBLIC, ACC_STATIC
Code:
    stack=3, locals=2, args_size=1 out=Java/\
    0: getstatic #5 // Field java/lang/System.Ljava/io/PrintStream;
    3: bipush 100
    5: invokespecial #9 // Method get_month:(I)Ljava/lang/String;
    8: invokevirtual #7 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
    11: ldc 47
    14: goto 1
    15: getstatic #5 // Method java/lang/System.Ljava/io/PrintStream;
    18: new #8 // Class java/lang/StringBuilder
    22: invokevirtual # // Method java/lang/StringBuilder.append("")init:()V
    25: ldc #10 // String incorrect month index:
    27: append(Ljava/lang/String;)Ljava/lang/StringBuilder;
    30: load 1
    31: invokirtual #12 // Method IncorrectMonthException.getIndex():()V
    34: load 1 // Method java/lang/StringBuilder.append:(I)Ljava/lang/StringBuilder;
    37: invokirtual #14 // Method java/lang/StringBuilder.toString():()Ljava/lang/String;
    40: getstatic #7 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
    43: load 1
    44: invokirtual #15 // Method IncorrectMonthException.printStackTrace():()V
    47: return
Exception table:
    from to target
    0 11 14 IncorrectMonthException
```

新指令创建了一个对象，但没有调用构造函数（它在偏移量 4 处调用）。

`set_a()` 方法在偏移量 16 处调用。

使用偏移量 21 处的 `getstatic` 指令访问字段。

## 4.1.17 简单补丁

### 第一个示例

让我们开始一个简单的代码补丁任务。

```java
public class nag {
    public static void nag_screen() {
        System.out.println("This program is not registered");
    }
    public static void main(String[] args) {
        System.out.println("Greetings from the mega-software");
        nag_screen();
    }
}
```

我们如何移除“This program is not registered”字符串的打印？

将 .class 文件加载到 IDA：

```
: Segment type: Pure code
:method public static nag_screen()
.line 4
.limit stack 2
170 000 002
    getstatic java/lang/System.out Java/io/PrintStream; ; CODE XREF: main+b5P
018 003 003
    id: "This program is not registered"
182 000 004
    invokevirtual java/io/PrintStream.println(L/java/String;)U
177
    return
??? ???? ???? ?+++
    .end method
??? ???? ???? ????
    ???
```

```
: Segment type: Pure code
:method public static main(L/java/lang/String;)U
.line 5
.limit stack 2
170 000 002
    getstatic java/lang/System.out Java/io/PrintStream;
018 005 005
    "Greetings From the mega-software"
182 000 004
    invokevirtual java/io/PrintStream.println(L/java/String;)U
.line 9
184 000 006
    invokestatic nag.nag_screen()
.line 10
    return
177
```

图 4.1: IDA

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

将函数的第一个字节补丁为 177（这是 `return` 指令的操作码）：

```
; Segment type: Pure code
.method public static nag_screen()U
.limit stack 2
.line 4
| nag_screen:
return; CODE XREF: main*81P
177
000
000
018 083
102 000 004
idc "This program is not registered"
invokevirtUAL java/io/PrintStream.println(Ljava/lang/String;)U
.line 5
return
177
??? ??? ???*
??? ??? ???*
???
```

图 4.2: IDA

但这不起作用（JRE 1.7）：

```
Exception in thread "main" java.lang.VerifyError: Expecting a stack map ✓ frame

Exception Details:

Location:

nag.nag_screen()JV @1: nop

Reason:

Error exists in the bytecode

Bytecode:

00000000 b010 0212 03b6 0004 b1

at at java.lang.Class.getDeclaredMethods(Native Method)

at at java.lang.Class.privateDeclaredMethods(Class.java:2615)

at at java.lang.Class.getDeclaredMethods(Class.java:2856)

at at java.lang.Class.getMethod(Class.java:1668)

at at sun.launcher.LauncherHelper.mainMethod(LauncherHelper.java/) : 494

at at sun.launcher.LauncherHelper.checkAndLoadMain(LauncherHelper.java/) : 486
```

JVM 有一些与栈映射相关的其他检查。

好的，让我们通过移除对 `nag()` 的调用来以不同的方式进行补丁：

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```
: Segment type: Pure code
.method public static main([Ljava/lang/String;])U
.limit stack 2
.limit locals 1
.line 8
.getstatic java/lang/System.out Ljava/io/PrintStream;
load "Streings from the mega-software"
.invokevirtual java/io/PrintStream.println(Ljava/String;)U
.line 9
nop
nop
nop
nop
.line 10
return ==
```

![](img/4590a0c34d3b5b6ca77b4202d4036d48_903_0.png)

0 是 `NOP` 的操作码。

现在可以了！

### 第二个示例

另一个简单的 crackme 示例：

```java
public class password {
    public static void main(String[] args) {
        System.out.println("Please enter the password");
        String input = System.console().readLine();
        if (input.equals("secret")) {
            System.out.println("password is correct");
        else
            System.out.println("password is not correct");
    }
}
```

让我们将其加载到 IDA。

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```
; Segment type: Pure code
.method public static main([Ljava/lang/String;])V
.limit stack 2
limit locals 2
.line 1
178 000 002
    getstatic java/lang/System.out Ljava/io/PrintStream;
018 002 003
    ldc "enter the password"
182 000 004
    invokevirtual java/io/PrintStream.println(Ljava/String;)V
.line 2
184 000 005
    invokstatic java/System.console(Ljava/io/Console;)
182 000 006
    invokevirtual java/io/Console.readline(Ljava/String;)
    store_1; m002_slt
.line 3
018 000 007
    load_1; m002_slt
182 000 008
    invokevirtual java/io/String.equals(Ljava/Object;)Z
.line 4
153 000 014
    ifne
    getstatic java/lang/System.out Ljava/io/PrintStream;
178 000 002
    ldc "password is not correct"
182 000 004
    invokevirtual java/io/PrintStream.println(Ljava/String;)V
.line 5
167 007 011
    goto m002_a3
.line 6
    goto : CODE XREF:main+21
178 000 002
    stack locals
    locals Object java/lang/String
    .end_stack
    getstatic java/lang/System.out Ljava/io/PrintStream;
018 010 002
    ldc "password is not correct"
182 000 004
    invokevirtual java/io/PrintStream.println(Ljava/String;)V
.line 9
```

图 4.4: IDA

我们在这里看到 `ifeq` 指令起到了作用。

它的名字代表 if equal（相等），这是一个误称，更好的名字应该是 `ifz`（零），即如果 TOS 为零，则执行跳转。

在我们的示例中，如果密码不正确它就会跳转（`equals` 方法返回 False，即为 0）。

第一个想法是补丁这条指令。

`ifeq` 操作码有两个字节，它们编码了跳转偏移量。

要使这条指令变为 `NOP`，我们将值的第三个字节设置为 3（因为在当前地址加上 3 将始终跳转到下一条指令，因为 `ifeq` 指令的长度为 3 字节）；

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```
: Segment type: Pure code
.method public static main([Ljava/String;])V
.limit locals 2
.init locals 2
.line 2
  getstatic java/lang/System.out Ljava/io/PrintStream;
  id "Please enter the password"
  invokevirtual java/io/PrintStream.println(Ljava/String;)U
  invokestatic java/lang/System.console() Ljava/io/Console;
  invokevirtual java/io/Console.readline(Ljava/String;)String
  astack 1
  .line 5
  oad_1 = ifq_atloc_001
  id "secret"
  invokevirtual java/lang/String.equals(Ljava/Lang/Object;)Z
  ifq_ne_02_24
  .line 6
  getstatic java/lang/System.out Ljava/io/PrintStream;
  id "password is correct"
  invokevirtual java/io/PrintStream.println(Ljava/String;)U
  goto _02_43
  .line 8
  stack_1
  locals Object java/lang/String
.endstart
  getstatic java/lang/System.out Ljava/io/PrintStream;
  id "password is not correct"
  invokevirtual java/io/PrintStream.println(Ljava/String;)U
  .line 9
```

图 4.5: IDA

那不起作用（JRE 1.7）。

```
Exception in thread "main" java.lang.VerifyError: Expecting a stackmap \ frame at branch target 24

Exception Details:

Location:

password.main([Ljava/lang/String;)@21: ifeq

Reason:

Expected stackmap frame at this location.

Byte:

000000: b200 0212 03b6 0004 b000 05b6 0004

000010: a700 07b2 0004 0000:35 0212 03b6 0004

000020: 1207 06b0 0004 0000:20 0212 03b6 0004

000030: 09b9 0400 0000 0000:30 0212 03b6 0004

000040: 0c00 0500 0000 0000:40 0212 03b6 0004

000050: 0f00 0600 0000

Stack Table:

> at java.lang.Class.getDeclaredMethods(Native Method)

at at java.lang.Class.privateDeclaredMethods(Class.java:2615)

at at java.lang.Class.getDeclaredMethods(Class.java:2856)

at at java.lang.Class.getMethod(Class.java:1668)

at at sun.launcher.LauncherHelper.mainMethod(LauncherHelper.java/) : 494

at at sun.launcher.LauncherHelper.checkAndLoadMain(LauncherHelper.java/) : 486
```

JVM 有一些与栈映射相关的其他检查。

好的，让我们通过移除对 `nag()` 的调用来以不同的方式进行补丁：

看起来 JRE 1.7 中有更多的栈映射检查。

我们也可以尝试将对所有方法的调用替换为 `icost_1` 指令加上一组 `NOP`。
