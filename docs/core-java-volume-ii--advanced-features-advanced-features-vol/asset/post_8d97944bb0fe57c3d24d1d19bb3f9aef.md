
### Executing Java Methods (Continued)

- `jobject NewObject(JNIEnv *env, jclass cl, jmethodID id, args)`
- `jobject NewObjectA(JNIEnv *env, jclass cl, jmethodID id, jvalue args[])`
- `jobject NewObjectV(JNIEnv *env, jclass cl, jmethodID id, va_list args)`

calls a constructor. The method ID is obtained from GetMethodID with a method name of `"<init>"` and a return type of void. The first function has a variable number of arguments—simply append the method parameters after the method ID. The second function receives the method arguments in an array of jvalue. The third function receives the method parameters in a va_list, as defined in the C header stdarg.h.

## 12.7 Accessing Array Elements

All array types of the Java programming language have corresponding C types, as shown in Table 12.2.

**Table 12.2** Correspondence between Java Array Types and C Types

| Java Type | C Type | Java Type | C Type |
|---|---|---|---|
| boolean[] | jbooleanArray | long[] | jlongArray |
| byte[] | jbyteArray | float[] | jfloatArray |
| char[] | jcharArray | double[] | jdoubleArray |
| int[] | jintArray | Object[] | jobjectArray |
| short[] | jshortArray |  |  |

> **C++ NOTE:** In C, all these array types are actually type synonyms of `jobject`. In C++, however, they are arranged in the inheritance hierarchy shown in Figure 12.3. The type `jarray` denotes a generic array.

The `GetArrayLength` function returns the length of an array.

```c
jarray array = ...;
jsize length = (*env)->GetArrayLength(env, array);
```

How you access elements in an array depends on whether the array stores objects or values of a primitive type (`bool`, `char`, or a numeric type). To access elements in an object array, use the `GetObjectArrayElement` and `SetObjectArrayElement` methods.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_863_0.png)

Figure 12.3 Inheritance hierarchy of array types

```c
jobjectArray array = ...;
int i, j;
jobject x = (*env)->GetObjectArrayElement(env, array, i);
(*env)->SetObjectArrayElement(env, array, j, x);
```

### Manipulating Java Arrays (Continued)

- `void GetXxxArrayRegion(JNIEnv *env, jarray array, jint start, jint length, Xxx elems[])`  
  copies elements from a Java array to a C array. The field type `Xxx` is one of Boolean, Byte, Char, Short, Int, Long, Float, or Double.
- `void SetXxxArrayRegion(JNIEnv *env, jarray array, jint start, jint length, Xxx elems[])`  
  copies elements from a C array to a Java array. The field type `Xxx` is one of Boolean, Byte, Char, Short, Int, Long, Float, or Double.

## 12.8 Handling Errors

Native methods are a significant security risk to Java programs. The C runtime system has no protection against array bounds errors, indirection through bad pointers, and so on. It is particularly important that programmers of native methods handle all error conditions to preserve the integrity of the Java platform. In particular, when your native method diagnoses a problem it cannot handle, it should report this problem to the Java virtual machine.

Normally, you would throw an exception in this situation. However, C has no exceptions. Instead, you must call the `Throw` or `ThrowNew` function to create a new exception object. When the native method exits, the Java virtual machine throws that exception.

To use the `Throw` function, call `NewObject` to create an object of a subtype of `Throwable`. For example, here we allocate an `EOFException` object and throw it:

```c
jclass class_EOFException = (*env)->FindClass(env, "java/io/EOFException");
jmethodID id_EOFException = (*env)->GetMethodID(env, class_EOFException, "<init>", "()V");
/* ID of no-argument constructor */
jthrowable obj_exc = (*env)->NewObject(env, class_EOFException, id_EOFException);
(*env)->Throw(env, obj_exc);
```

It is usually more convenient to call `ThrowNew`, which constructs an exception object, given a class and a "modified UTF-8" byte sequence.

```c
(*env)->ThrowNew(env, (*env)->FindClass(env, "java/io/EOFException"),
    "Unexpected end of file");
```

Both `Throw` and `ThrowNew` merely post the exception; they do not interrupt the control flow of the native method. Only when the method returns does the Java virtual machine throw the exception. Therefore, every call to `Throw` and `ThrowNew` should be immediately followed by a `return` statement.

containing the native method. Notice that the native method does not immediately terminate when an exception occurs in the call to PrintWriter.print—it first frees the cstr buffer. When the native method returns, the virtual machine again raises the exception. The test program in Listing 12.19 demonstrates how the native method throws an exception when the formatting string is not valid.

**Listing 12.17** printf4/Printf4.c

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

**Listing 12.18** `printf4/Printf4.java`

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

**Listing 12.19** `printf4/Printf4Test.java`

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

### Handling Java Exceptions

- `jint Throw(JNIEnv *env, jthrowable obj)`  
  prepares an exception to be thrown upon exiting from the native code. Returns 0 on success, a negative value on failure.
- `jint ThrowNew(JNIEnv *env, jclass cl, const char msg[])`  
  prepares an exception of type cl to be thrown upon exiting from the native code. Returns 0 on success, a negative value on failure. msg is a "modified UTF-8" byte sequence denoting the String construction argument of the exception object.
- `jthrowable ExceptionOccurred(JNIEnv *env)`  
  returns the exception object if an exception is pending, or NULL otherwise.
- `jboolean ExceptionCheck(JNIEnv *env)`  
  returns true if an exception is pending.
- `void ExceptionClear(JNIEnv *env)`  
  clears any pending exceptions.

## 12.9 Using the Invocation API

Up to now, we have considered programs in the Java programming language that made a few C calls, presumably because C was faster or allowed access to functionality inaccessible from the Java platform. Suppose you are in the opposite situation. You have a C or C++ program and would like to make calls to Java code. The *invocation API* enables you to embed the Java virtual machine into a C or C++ program. Here is the minimal code that you need to initialize a virtual machine:

```c
JavaVMOption options[1];
JavaVMInitArgs vm_args;
JavaVM *jvm;
JNIEnv *env;

options[0].optionString = "-Djava.class.path=.";
```
