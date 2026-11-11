
```c
jthrowable obj_exc = (*env)->NewObject(env, class_EOFException, fid_EOFException);
(*env)->Throw(env, obj_exc);
```

It is usually more convenient to call *ThrowNew*, which constructs an exception object, given a class and a "modified UTF-8" byte sequence.

```c
(*env)->ThrowNew(env, (*env)->FindClass(env, "java/io/EOFException"), "Unexpected end of file");
```

Both *Throw* and *ThrowNew* merely post the exception; they do not interrupt the control flow of the native method. Only when the method returns does the Java virtual machine throw the exception. Therefore, every call to *Throw* and *ThrowNew* should always be immediately followed by a return statement.

> **C++ NOTE:** If you implement native methods in C++, you cannot throw a Java exception object in your C++ code. In a C++ binding, it would be possible to implement a translation between exceptions in C++ and Java; however, this is not currently done. Use *Throw* or *ThrowNew* to throw a Java exception in a native C++ method, and make sure your native methods throw no C++ exceptions.

Normally, native code need not be concerned with catching Java exceptions. However, when a native method calls a Java method, that method might throw an exception. Moreover, a number of the JNI functions throw exceptions as well. For example, `SetObjectArrayElement` throws an `ArrayIndexOutOfBoundsException` if the index is out of bounds, and an `ArrayStoreException` if the class of the stored object is not a subclass of the element class of the array. In situations like these, a native method should call the `ExceptionOccurred` method to determine whether an exception has been thrown. The call

```c
jthrowable obj_exc = (*env)->ExceptionOccurred(env);
```

returns `NULL` if no exception is pending, or a reference to the current exception object. If you just want to check whether an exception has been thrown, without obtaining a reference to the exception object, use

```c
jboolean occurred = (*env)->ExceptionCheck(env);
```

Normally, a native method should simply return when an exception has occurred so that the virtual machine can propagate it to the Java code. However, a native method *may* analyze the exception object to determine if it can handle the exception. If it can, then the function

```c
(*env)->ExceptionClear(env);
```

must be called to turn off the exception.

### Listing 12.17

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

### Listing 12.18 printf4/Printf4.java

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

### Listing 12.19 Printf4/Printf4Test.java

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

### Handling Java Exceptions

- `jint Throw(JNIEnv *env, jthrowable obj)` prepares an exception to be thrown upon exiting from the native code. Returns 0 on success, a negative value on failure.
- `jint ThrowNew(JNIEnv *env, jclass cl, const char msg[])` prepares an exception of type cl to be thrown upon exiting from the native code. Returns 0 on success, a negative value on failure. msg is a "modified UTF-8" byte sequence denoting the String construction argument of the exception object.
- `jthrowable ExceptionOccurred(JNIEnv *env)` returns the exception object if an exception is pending, or NULL otherwise.
- `jboolean ExceptionCheck(JNIEnv *env)` returns true if an exception is pending.
- `void ExceptionClear(JNIEnv *env)` clears any pending exceptions.

## 12.9 Using the Invocation API

Up to now, we have considered programs in the Java programming language that made a few C calls, presumably because C was faster or allowed access to functionality inaccessible from the Java platform. Suppose you are in the opposite situation. You have a C or C++ program and would like to make calls to Java code. The *invocation API* enables you to embed the Java virtual machine into a C or C++ program. Here is the minimal code that you need to initialize a virtual machine:

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

The call to `JNI_CreateJavaVM` creates the virtual machine and fills in a pointer `jvm` to the virtual machine and a pointer `env` to the execution environment.

You can supply any number of options to the virtual machine. Simply increase the size of the `options` array and the value of `vm_args.nOptions`. For example,

```c
options[1].optionString = "-Djava.compiler=NONE";
```

deactivates the just-in-time compiler.

> **TIP:** When you run into trouble and your program crashes, refuses to initialize the JVM, or can't load your classes, turn on the JNI debugging mode. Set an option to
>
> ```c
> options[1].optionString = "-verbose:jni";
> ```
>
> You will see a flurry of messages that indicate the progress in initializing the JVM. If you don't see your classes loaded, check both your path and class path settings.

Once you have set up the virtual machine, you can call Java methods as described in the preceding sections. Simply use the `env` pointer in the usual way.
