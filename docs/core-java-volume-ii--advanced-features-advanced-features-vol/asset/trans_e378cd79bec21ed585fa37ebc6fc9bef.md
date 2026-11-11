
### 执行 Java 方法（续）

- `jobject NewObject(JNIEnv *env, jclass cl, jmethodID id, args)`
- `jobject NewObjectA(JNIEnv *env, jclass cl, jmethodID id, jvalue args[])`
- `jobject NewObjectV(JNIEnv *env, jclass cl, jmethodID id, va_list args)`

调用构造函数。方法 ID 通过 GetMethodID 获取，方法名为 `"<init>"`，返回类型为 void。第一个函数具有可变数量的参数——只需在方法 ID 后追加方法参数。第二个函数在 jvalue 数组中接收方法参数。第三个函数在 va_list 中接收方法参数，如 C 头文件 stdarg.h 所定义。

## 12.7 访问数组元素

Java 编程语言的所有数组类型都有对应的 C 类型，如表 12.2 所示。

**表 12.2** Java 数组类型与 C 类型之间的对应关系

| Java 类型 | C 类型 | Java 类型 | C 类型 |
|---|---|---|---|
| boolean[] | jbooleanArray | long[] | jlongArray |
| byte[] | jbyteArray | float[] | jfloatArray |
| char[] | jcharArray | double[] | jdoubleArray |
| int[] | jintArray | Object[] | jobjectArray |
| short[] | jshortArray |  |  |

> **C++ 注意：** 在 C 中，所有这些数组类型实际上都是 `jobject` 的类型同义词。然而，在 C++ 中，它们按照图 12.3 所示的继承层次结构排列。类型 `jarray` 表示泛型数组。

`GetArrayLength` 函数返回数组的长度。

```c
jarray array = ...;
jsize length = (*env)->GetArrayLength(env, array);
```

如何访问数组中的元素取决于该数组存储的是对象还是基本类型（`bool`、`char` 或数值类型）的值。要访问对象数组中的元素，请使用 `GetObjectArrayElement` 和 `SetObjectArrayElement` 方法。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_863_0.png)

图 12.3 数组类型的继承层次结构

```c
jobjectArray array = ...;
int i, j;
jobject x = (*env)->GetObjectArrayElement(env, array, i);
(*env)->SetObjectArrayElement(env, array, j, x);
```

### 操作 Java 数组（续）

- `void GetXxxArrayRegion(JNIEnv *env, jarray array, jint start, jint length, Xxx elems[])`  
  将元素从 Java 数组复制到 C 数组。字段类型 `Xxx` 是 Boolean、Byte、Char、Short、Int、Long、Float 或 Double 之一。
- `void SetXxxArrayRegion(JNIEnv *env, jarray array, jint start, jint length, Xxx elems[])`  
  将元素从 C 数组复制到 Java 数组。字段类型 `Xxx` 是 Boolean、Byte、Char、Short、Int、Long、Float 或 Double 之一。

## 12.8 处理错误

本地方法对 Java 程序构成重大安全风险。C 运行时系统对数组越界错误、通过错误指针进行间接访问等没有保护。本地方法的程序员处理所有错误条件以保持 Java 平台的完整性尤为重要。特别是，当你的本地方法诊断出它无法处理的问题时，应将该问题报告给 Java 虚拟机。

通常，在这种情况下你会抛出异常。然而，C 没有异常。相反，你必须调用 `Throw` 或 `ThrowNew` 函数来创建新的异常对象。当本地方法退出时，Java 虚拟机会抛出该异常。

要使用 `Throw` 函数，请调用 `NewObject` 创建 `Throwable` 的子类型的对象。例如，这里我们分配一个 `EOFException` 对象并抛出它：

```c
jclass class_EOFException = (*env)->FindClass(env, "java/io/EOFException");
jmethodID id_EOFException = (*env)->GetMethodID(env, class_EOFException, "<init>", "()V");
/* ID of no-argument constructor */
jthrowable obj_exc = (*env)->NewObject(env, class_EOFException, id_EOFException);
(*env)->Throw(env, obj_exc);
```

通常更方便的是调用 `ThrowNew`，它在给定类和“修改版 UTF-8”字节序列的情况下构造异常对象。

```c
(*env)->ThrowNew(env, (*env)->FindClass(env, "java/io/EOFException"),
    "Unexpected end of file");
```

`Throw` 和 `ThrowNew` 都只是发布异常；它们不会中断本地方法的控制流。只有当方法返回时，Java 虚拟机才会抛出异常。因此，每次调用 `Throw` 和 `ThrowNew` 后都应立即跟随一条 `return` 语句。

包含该本地方法。注意，当调用 PrintWriter.print 发生异常时，本地方法不会立即终止——它会先释放 cstr 缓冲区。当本地方法返回时，虚拟机会再次引发该异常。清单 12.19 中的测试程序演示了当格式字符串无效时，本地方法如何抛出异常。

**清单 12.17** printf4/Printf4.c

```c
1 /**
2    @version 1.10 1997-07-01
3    @author Cay Horstmann
4 */
5
6 #include "Printf4.h"
7 #include <string.h>
8 #include <stdlib.h>
9 #include <float.h>
10
11 /**
12    @param format a string containing a printf format specifier
13    (such as "%8.2f"). Substrings "%s" are skipped.
14    @return a pointer to the format specifier (skipping the '%')
15    or NULL if there wasn't a unique format specifier
16 */
17 char* find_format(const char format[])
18 {
19    char* p;
20    char* q;
21
22    p = strchr(format, '%');
23    while (p != NULL && *(p + 1) == '%') /* skip %% */
24       p = strchr(p + 2, '%');
25    if (p == NULL) return NULL;
26    /* now check that % is unique */
27    p++;
28    q = strchr(p, '%');
29    while (q != NULL && *(q + 1) == '%') /* skip %% */
30       q = strchr(q + 2, '%');
31    if (q != NULL) return NULL; /* % not unique */
32    q = p + strspn(p, " -0+#"); /* skip past flags */
33    q += strspn(q, "0123456789"); /* skip past field width */
34    if (*q == '.') { q++; q += strspn(q, "0123456789"); }
35       /* skip past precision */
36    if (strchr("eEfFgG", *q) == NULL) return NULL;
37       /* not a floating-point format */
38    return p;
39 }
89  /* now call ps.print(str) */
90
91  /* get the class */
92  jclass class_PrintWriter = (*env)->GetObjectClass(env, out);
93
94  /* get the method ID */
95  jmethodID id_print = (*env)->GetMethodID(env, class_PrintWriter, "print", "(C)V");
96
97  /* call the method */
98  for (i = 0; str[i] != 0 && !(*env)->ExceptionOccurred(env); i++)
99      (*env)->CallVoidMethod(env, out, id_print, str[i]);
100
101  free(str);
102  }
```

**清单 12.18** `printf4/Printf4.java`

```java
1  import java.io.*;
2
3  /**
4   * @version 1.10 1997-07-01
5   * @author Cay Horstmann
6   */
7  class Printf4
8  {
9      public static native void fprintf(PrintWriter ps, String format, double x);
10
11     static
12     {
13         System.loadLibrary("Printf4");
14     }
15 }
```

**清单 12.19** `printf4/Printf4Test.java`

```java
1  import java.io.*;
2
3  /**
4   * @version 1.11 2018-05-01
5   * @author Cay Horstmann
6   */
7  class Printf4Test
8  {
9      public static void main(String[] args)
10     {
double price = 44.95;
double tax = 7.75;
double amountDue = price * (1 + tax / 100);
var out = new PrintWriter(System.out);
/* This call will throw an exception--note the % */
Printf4.fprintf(out, "Amount due = $%.2f%n", amountDue);
out.flush();
}
}
```

### 处理 Java 异常

- `jint Throw(JNIEnv *env, jthrowable obj)`  
  准备一个在退出本地代码时抛出的异常。成功时返回 0，失败时返回负值。
- `jint ThrowNew(JNIEnv *env, jclass cl, const char msg[])`  
  准备一个类型为 cl 的异常，在退出本地代码时抛出。成功时返回 0，失败时返回负值。msg 是一个“修改版 UTF-8”字节序列，表示异常对象的 String 构造参数。
- `jthrowable ExceptionOccurred(JNIEnv *env)`  
  如果有待处理的异常，则返回异常对象，否则返回 NULL。
- `jboolean ExceptionCheck(JNIEnv *env)`  
  如果有待处理的异常，则返回 true。
- `void ExceptionClear(JNIEnv *env)`  
  清除任何待处理的异常。

## 12.9 使用调用 API

到目前为止，我们考虑的是 Java 编程语言程序进行少量 C 调用的情况，大概是因为 C 更快，或者允许访问 Java 平台无法访问的功能。假设你处于相反的情况。你有一个 C 或 C++ 程序，并希望调用 Java 代码。*调用 API* 使你能够将 Java 虚拟机嵌入 C 或 C++ 程序。以下是初始化虚拟机所需的最少代码：

```c
JavaVMOption options[1];
JavaVMInitArgs vm_args;
JavaVM *jvm;
JNIEnv *env;

options[0].optionString = "-Djava.class.path=.";
```
