
```c
jthrowable obj_exc = (*env)->NewObject(env, class_EOFException, fid_EOFException);
(*env)->Throw(env, obj_exc);
```

通常更方便的是调用 *ThrowNew*，它在给定一个类和一个“修改版 UTF-8”字节序列的情况下构造异常对象。

```c
(*env)->ThrowNew(env, (*env)->FindClass(env, "java/io/EOFException"), "Unexpected end of file");
```

*Throw* 和 *ThrowNew* 都只是发布异常；它们不会中断本机方法的控制流。只有当方法返回时，Java 虚拟机才会抛出该异常。因此，每次调用 *Throw* 和 *ThrowNew* 后都应立即跟一个 return 语句。

> **C++ 注意：** 如果用 C++ 实现本机方法，则不能在 C++ 代码中抛出 Java 异常对象。在 C++ 绑定中，可以实现 C++ 异常与 Java 异常之间的转换；但是，目前尚未这样做。请使用 *Throw* 或 *ThrowNew* 在本机 C++ 方法中抛出 Java 异常，并确保你的本机方法不抛出任何 C++ 异常。

通常，本机代码无需关心捕获 Java 异常。但是，当本机方法调用 Java 方法时，该方法可能抛出异常。此外，许多 JNI 函数也会抛出异常。例如，如果索引越界，`SetObjectArrayElement` 会抛出 `ArrayIndexOutOfBoundsException`；如果被存储对象的类不是数组元素类的子类，则会抛出 `ArrayStoreException`。在这种情况下，本机方法应调用 `ExceptionOccurred` 方法来确定是否已抛出异常。以下调用

```c
jthrowable obj_exc = (*env)->ExceptionOccurred(env);
```

如果当前没有待处理的异常，则返回 `NULL`；否则返回对当前异常对象的引用。如果你只想检查是否已抛出异常，而不获取异常对象的引用，请使用

```c
jboolean occurred = (*env)->ExceptionCheck(env);
```

通常，当发生异常时，本机方法应直接返回，以便虚拟机可以将异常传播到 Java 代码。但是，本机方法*可以*分析异常对象，以确定它是否能处理该异常。如果可以，则必须调用函数

```c
(*env)->ExceptionClear(env);
```

来关闭该异常。

### 清单 12.17

```c
28    q = strchr(p, '%');
29    while (q != NULL && *(q + 1) == '%') /* skip %% */
30        q = strchr(q + 2, '%');
31    if (q != NULL) return NULL; /* % not unique */
32    q = p + strspn(p, "-0#"); /* skip past Flags */
33    q += strspn(q, "0123456789"); /* skip past field width */
34    if (*q == '.') { q++; q += strspn(q, "0123456789"); }
35        /* skip past precision */
36    if (strchr("eEfFgG", *q) == NULL) return NULL;
37        /* not a floating-point format */
38    return p;
39 }
40
41 JNIEXPORT void JNICALL Java_Printf4_fprint(JNIEnv *env, jclass cl,
42     jobject out, jstring format, jdouble x)
43 {
44    const char* cformat;
45    char* fmt;
46    jclass class_PrintWriter;
47    jmethodID id_print;
48    char* cstr;
49    int width;
50    int i;
51
52    if (format == NULL)
53    {
54        (*env)->ThrowNew(env,
55            (*env)->FindClass(env,
56            "java/lang/NullPointerException"),
57            "Printf4.fprint: format is null");
58        return;
59    }
60
61    cformat = (*env)->GetStringUTFChars(env, format, NULL);
62    fmt = find_format(cformat);
63
64    if (fmt == NULL)
65    {
66        (*env)->ThrowNew(env,
67            (*env)->FindClass(env,
68            "java/lang/IllegalArgumentException"),
69            "Printf4.fprint: format is invalid");
70        return;
71    }
72
73    width = atoi(fmt);
74    if (width == 0) width = DBL_DIG + 10;
75    cstr = (char*)malloc(strlen(cformat) + width);
77 if (cstr == NULL)
78 {
79     (*env)->ThrowNew(env,
80         (*env)->FindClass(env, "java/lang/OutOfMemoryError"),
81         "Printf4.fprint: malloc failed");
82     return;
83 }
84
85 sprintf(cstr, cformat, x);
86
87 (*env)->ReleaseStringUTFChars(env, format, cformat);
88
89 /* now call ps.print(str) */
90
91 /* get the class */
92 class_PrintWriter = (*env)->GetObjectClass(env, out);
93
94 /* get the method ID */
95 id_print = (*env)->GetMethodID(env, class_PrintWriter, "print", "(C)V");
96
97 /* call the method */
98 for (i = 0; cstr[i] != 0 && !(*env)->ExceptionOccurred(env); i++)
99     (*env)->CallVoidMethod(env, out, id_print, cstr[i]);
100
101 free(cstr);
102 }
```

### 清单 12.18 printf4/Printf4.java

```java
1 import java.io.*;
2
3 /**
4  * @version 1.10 1997-07-01
5  * @author Cay Horstmann
6  */
7 class Printf4
8 {
9     public static native void fprint(PrintWriter ps, String format, double x);
10
11     static
12     {
13         System.loadLibrary("Printf4");
14     }
15 }
```

### 清单 12.19 Printf4/Printf4Test.java

```java
1 import java.io.*;
2
3 /*
4  * @version 1.10 1997-07-01
5  * @author Cay Horstmann
6  */
7 class Printf4Test
8 {
9    public static void main(String[] args)
10   {
11      double price = 44.95;
12      double tax = 7.75;
13      double amountDue = price * (1 + tax / 100);
14      PrintWriter out = new PrintWriter(System.out);
15      /* This call will throw an exception--note the %% */
16      Printf4.fprint(out, "Amount due = %8.2f\n", amountDue);
17      out.flush();
18   }
19 }
```

### 处理 Java 异常

- `jint Throw(JNIEnv *env, jthrowable obj)` 准备一个在退出本机代码时抛出的异常。成功时返回 0，失败时返回负值。
- `jint ThrowNew(JNIEnv *env, jclass cl, const char msg[])` 准备一个类型为 cl 的异常，在退出本机代码时抛出。成功时返回 0，失败时返回负值。msg 是一个“修改版 UTF-8”字节序列，表示异常对象的 String 构造参数。
- `jthrowable ExceptionOccurred(JNIEnv *env)` 如果有待处理的异常，则返回异常对象；否则返回 NULL。
- `jboolean ExceptionCheck(JNIEnv *env)` 如果有待处理的异常，则返回 true。
- `void ExceptionClear(JNIEnv *env)` 清除任何待处理的异常。

## 12.9 使用调用 API

到目前为止，我们考虑的都是 Java 编程语言程序进行少量 C 调用的情况，推测是因为 C 更快，或者允许访问 Java 平台无法访问的功能。假设你处于相反的情况：你有一个 C 或 C++ 程序，并希望调用 Java 代码。*调用 API* 使你能够将 Java 虚拟机嵌入 C 或 C++ 程序。下面是初始化虚拟机所需的最少代码：

```c
JavaVMOption options[1];
JavaVMInitArgs vm_args;
JavaVM *jvm;
JNIEnv *env;

options[0].optionString = "-Djava.class.path=.";

memset(&vm_args, 0, sizeof(vm_args));
vm_args.version = JNI_VERSION_1_2;
vm_args.nOptions = 1;
vm_args.options = options;

JNI_CreateJavaVM(&jvm, (void**) &env, &vm_args);
```

对 `JNI_CreateJavaVM` 的调用会创建虚拟机，并填充指向虚拟机的指针 `jvm` 以及指向执行环境的指针 `env`。

你可以向虚拟机提供任意数量的选项。只需增大 `options` 数组的大小和 `vm_args.nOptions` 的值。例如，

```c
options[1].optionString = "-Djava.compiler=NONE";
```

会停用即时编译器。

> **提示：** 当你遇到问题、程序崩溃、拒绝初始化 JVM 或无法加载类时，请打开 JNI 调试模式。将选项设置为
>
> ```c
> options[1].optionString = "-verbose:jni";
> ```
>
> 你将看到大量消息，指示初始化 JVM 的进度。如果你没有看到类被加载，请检查路径和类路径设置。

设置好虚拟机后，就可以像前面几节所述那样调用 Java 方法。只需按常规方式使用 `env` 指针。

