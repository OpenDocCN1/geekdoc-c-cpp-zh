
- Supply a class object, not an implicit parameter object, when invoking the method.

As an example of this, let’s make the call to the static method

```java
System.getProperty("java.class.path")
```

from a native method. The return value of this call is a string that gives the current class path.

First, we have to find the class to use. As we have no object of the class System readily available, we use FindClass rather than GetObjectClass.

```c
jclass class_System = (*env)->FindClass(env, "java/lang/System");
```

Next, we need the ID of the static getProperty method. The encoded signature of that method is

```
"(Ljava/lang/String;)Ljava/lang/String;"
```

because both the parameter and the return value are strings. Hence, we obtain the method ID as follows:

```c
jmethodID id_getProperty = (*env)->GetStaticMethodID(env, class_System, "getProperty",
    "(Ljava/lang/String;)Ljava/lang/String;");
```

Finally, we can make the call. Note that the class object is passed to the CallStaticObjectMethod function.

```c
jobject obj_ret = (*env)->CallStaticObjectMethod(env, class_System, id_getProperty,
    (*env)->NewStringUTF(env, "java.class.path"));
```

The return value of this method is of type jobject. If we want to manipulate it as a string, we must cast it to jstring:

```c
jstring str_ret = (jstring) obj_ret;
```

> **C++ NOTE:** In C, the types jstring and jclass, as well as the array types to be introduced later, are all type-equivalent to jobject. The cast of the preceding example is therefore not strictly necessary in C. But in C++, these types are defined as pointers to “dummy classes” that have the correct inheritance hierarchy. For example, assigning a jstring to a jobject is legal without a cast in C++, but an assignment from a jobject to a jstring requires a cast.

## 12.6.3 Constructors

A native method can create a new Java object by invoking its constructor. Invoke the constructor by calling the NewObject function.

```c
jobject obj_new = (*env)->NewObject(env, class, methodID, construction parameters);
```

You can obtain the method ID needed for this call from the `GetMethodID` function by specifying the method name as `"<init>"` and the encoded signature of the constructor (with return type `void`). For example, here is how a native method can create a `FileOutputStream` object:

```c
const char fileName[] = ". . .";
jstring str_fileName = (*env)->NewStringUTF(env, fileName);
jclass class_FileOutputStream = (*env)->FindClass(env, "java/io/FileOutputStream");
jmethodID id_FileOutputStream
    = (*env)->GetMethodID(env, class_FileOutputStream, "<init>", "(Ljava/lang/String;)V");
jobject obj_stream
    = (*env)->NewObject(env, class_FileOutputStream, id_FileOutputStream, str_fileName);
```

Note that the signature of the constructor takes a parameter of type `java.lang.String` and has a return type of `void`.

## 12.6.4 Alternative Method Invocations

Several variants of the JNI functions can be used to call a Java method from native code. These are not as important as the functions that we already discussed, but they are occasionally useful.

The `CallNonvirtualXxxMethod` functions receive an implicit argument, a method ID, a class object (which must correspond to a superclass of the implicit argument), and explicit arguments. The function calls the version of the method in the specified class, bypassing the normal dynamic dispatch mechanism.

All call functions have versions with suffixes `"A"` and `"V"` that receive the explicit parameters in an array or a `va_list` (as defined in the C header `stdarg.h`).

**Listing 12.14** printf3/Printf3Test.java

```java
import java.io.*;

/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */

class Printf3Test
{
    public static void main(String[] args)
    {
        double price = 44.95;
        double tax = 7.75;
        double amountDue = price * (1 + tax / 100);

        PrintWriter out = new PrintWriter(System.out);
        Printf3.fprintf(out, "Amount due = %8.2f\n", amountDue);
        out.flush();
    }
}
```

**Listing 12.15** printf3/Printf3.java

```java
import java.io.*;

/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */
class Printf3
{
    public static native void fprintf(PrintWriter out, String format, double x);

    static
    {
        System.loadLibrary("Printf3");
    }
}
```

**Listing 12.16** printf3/Printf3.c

```c
/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */

#include "Printf3.h"
#include <string.h>
#include <stdlib.h>
#include <float.h>

/**
   @param format a string containing a printf format specifier
   (such as "%8.2f"). Substrings "%%" are skipped.
   @return a pointer to the format specifier (skipping the '%')
   or NULL if there wasn't a unique format specifier
*/
char* find_format(const char format[])
{
    char* p;
    char* q;

    p = strchr(format, '%');
    while (p != NULL && *(p + 1) == '%') /* skip %% */
        p = strchr(p + 2, '%');
    if (p == NULL) return NULL;
    /* now check that % is unique */
    p++;
    q = strchr(p, '%');
    while (q != NULL && *(q + 1) == '%') /* skip %% */
        q = strchr(q + 2, '%');
    if (q != NULL) return NULL; /* % not unique */
    q = p + strspn(p, "-0+"); /* skip past flags */
    q += strspn(q, "0123456789"); /* skip past field width */
    if (*q == '.') { /* skip past precision */
        q++;
        while (isdigit(*q)) q++;
    }
    if (strchr("efEgG", *q) == NULL) return NULL;
    /* not a floating-point format */
    return p;
}

JNIEXPORT void JNICALL Java_Printf3_printf(JNIEnv* env, jclass cl,
    jobject out, jstring format, jdouble x)
{
    const char* cformat;
    char* fmt;
    jstring str;
    jclass class_PrintWriter;
    jmethodID id_print;

    cformat = (*env)->GetStringUTFChars(env, format, NULL);
    fmt = find_format(cformat);
    if (fmt == NULL)
        str = format;
    else
    {
        char* cstr;
        int width = atoi(fmt);
        if (width == 0) width = DBL_DIG + 10;
        cstr = (char*) malloc(strlen(format) + width);
        sprintf(cstr, format, x);
        str = (*env)->NewStringUTF(env, cstr);
        free(cstr);
    }
    (*env)->ReleaseStringUTFChars(env, format, cformat);

    /* now call ps.print(str) */

    /* get the class */
    class_PrintWriter = (*env)->GetObjectClass(env, out);

    /* get the method ID */
    id_print = (*env)->GetMethodID(env, class_PrintWriter, "print", "(Ljava/lang/String;)V");

    /* call the method */
    (*env)->CallVoidMethod(env, out, id_print, str);
}
```

## Executing Java Methods

- `jmethodID GetMethodID(JNIEnv *env, jclass cl, const char name[], const char methodSignature[])`

  returns the identifier of a method in a class.

- `Xxx CallXxxMethod(JNIEnv *env, jobject obj, jmethodID id, args)`
- `Xxx CallXxxMethodA(JNIEnv *env, jobject obj, jmethodID id, jvalue args[])`
- `Xxx CallXxxMethodV(JNIEnv *env, jobject obj, jmethodID id, va_list args)`

calls a method. The return type `Xxx` is one of `Object`, `Boolean`, `Byte`, `Char`, `Short`, `Int`, `Long`, `Float`, or `Double`. The first function has a variable number of arguments—simply append the method parameters after the method ID. The second function receives the method arguments in an array of `jvalue`, where `jvalue` is a union defined as

```c
typedef union jvalue
{
    jboolean z;
    jbyte b;
    jchar c;
    jshort s;
    jint i;
    jlong j;
    jfloat f;
    jdouble d;
    jobject l;
} jvalue;
```

The third function receives the method parameters in a `va_list`, as defined in the C header `stdarg.h`.

- `Xxx CallNonvirtualXxxMethod(JNIEnv *env, jobject obj, jclass cl, jmethodID id, args)`
- `Xxx CallNonvirtualXxxMethodA(JNIEnv *env, jobject obj, jclass cl, jmethodID id, jvalue args[])`
- `Xxx CallNonvirtualXxxMethodV(JNIEnv *env, jobject obj, jclass cl, jmethodID id, va_list args)`

calls a method, bypassing dynamic dispatch. The return type `Xxx` is one of `Object`, `Boolean`, `Byte`, `Char`, `Short`, `Int`, `Long`, `Float`, or `Double`. The first function has a variable number of arguments—simply append the method parameters after the method ID. The second function receives the method arguments in an array of `jvalue`. The third function receives the method parameters in a `va_list`, as defined in the C header `stdarg.h`.
