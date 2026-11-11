
You’ll need the `jvm` pointer only to call other functions in the invocation API. Currently, there are only four such functions. The most important one is the function to terminate the virtual machine:

`(*jvm)->DestroyJavaVM(jvm);`

Unfortunately, under Windows, it has become difficult to dynamically link to the `JNI_CreateJavaVM` function in the `jre/bin/client/jvm.dll` library, due to the changed linking rules in Vista and Oracle’s reliance on an older C runtime library. Our sample program overcomes this problem by loading the library manually. This is the same approach used by the Java program—see the file `launcher/java_md.c` in the `src.jar` file that is a part of the JDK.

The C program in Listing 12.20 sets up a virtual machine and calls the main method of the `Welcome` class, which was discussed in Volume I, Chapter 2. (Make sure to compile the `Welcome.java` file before starting the invocation test program.)

```c
/*
 * @version 1.20 2007-10-26
 * @author Cay Horstmann
 */

#include <jni.h>
#include <stdlib.h>

#ifdef _WINDOWS

#include <windows.h>
static HINSTANCE loadJVMLibrary(void);
typedef jint (JNICALL *CreateJavaVM)(JavaVM **, void **, JavaVMInitArgs *);

#endif

int main()
{
   JavaVMOption options[2];
   JavaVMInitArgs vm_args;
   JavaVM *jvm;
   JNIEnv *env;
   long status;

   jclass class_Welcome;
   jclass class_String;
   jobjectArray args;
```

*Listing 12.20* `invocation/InvocationTest.c`

**Listing 12.20 (Continued)**

```c
static HINSTANCE loadJVMLibrary(void)
{
    HINSTANCE h1, h2;
    char msvcdll[MAX_PATH];
    char javadll[MAX_PATH];
    GetModuleFileName(NULL, msvcdll, MAX_PATH);
    strcpy(javadll, msvcdll);
    strncat(msvcdll, "\\bin\\msvcr71.dll", MAX_PATH - strlen(msvcdll));
    msvcdll[MAX_PATH - 1] = '\0';
    strncat(javadll, "\\bin\\client\\jvm.dll", MAX_PATH - strlen(javadll));
    javadll[MAX_PATH - 1] = '\0';

    h1 = LoadLibrary(msvcdll);
    if (h1 == NULL)
    {
        fprintf(stderr, "Can't load library msvcr71.dll\n");
        exit(1);
    }

    h2 = LoadLibrary(javadll);
    if (h2 == NULL)
    {
        fprintf(stderr, "Can't load library jvm.dll\n");
        exit(1);
    }

    return h2;
}

#endif
```

To compile this program under Linux, use

```bash
gcc -I jdk/include -I jdk/include/linux -o InvocationTest
    -L jdk/jre/lib/i386/client -ljvm InvocationTest.c
```

Under Solaris, use

```bash
cc -I jdk/include -I jdk/include/solaris -o InvocationTest
    -L jdk/jre/lib/sparc -ljvm InvocationTest.c
```

When compiling in Windows with the Microsoft compiler, use the command line

```bat
cl -D_WINDOWS -I jdk\include -I jdk\include\win32 InvocationTest.c jdk\lib\jvm.lib advapi32.lib
```

You will need to make sure that the INCLUDE and LIB environment variables include the paths to the Windows API header and library files.

Using Cygwin, compile with

```bash
gcc -D_WINDOWS -mno-cygwin -I jdk\include -I jdk\include\win32 -D_int64="long long"
    -I c:\cygwin\usr\include\w32api -o InvocationTest
```

Before you run the program under Linux/UNIX, make sure that the `LD_LIBRARY_PATH` contains the directories for the shared libraries. For example, if you use the bash shell on Linux, issue the following command:

```bash
export LD_LIBRARY_PATH=jdk/jre/lib/i386/client:$LD_LIBRARY_PATH
```

### Invocation API Functions

- `jint JNI_CreateJavaVM(JavaVM** p_jvm, void** p_env, JavaVMInitArgs* vm_args)`  
  Initializes the Java virtual machine. The function returns `0` if successful, `JNI_ERR` on failure.

  | Parameters | Description |
  |---|---|
  | `p_jvm` | Filled with a pointer to the invocation API function table |
  | `p_env` | Filled with a pointer to the JNI function table |
  | `vm_args` | The virtual machine arguments |

- `jint DestroyJavaVM(JavaVM* jvm)`  
  Destroys the virtual machine. Returns `0` on success, a negative number on failure. This function must be called through a virtual machine pointer, that is, `(*jvm)->DestroyJavaVM(jvm)`.

## 12.10 A Complete Example: Accessing the Windows Registry

In this section, we describe a full, working example that covers everything we discussed in this chapter: using native methods with strings, arrays, objects, constructor calls, and error handling. We’ll show you how to put a Java platform wrapper around a subset of the ordinary C-based APIs used to work with the Windows registry. Of course, the Windows registry being a Windows-specific feature, such a program is inherently nonportable. For that reason, the standard Java library has no support for the registry, and it makes sense to use native methods to gain access to it.

### 12.10.1 Overview of the Windows Registry

The Windows registry is a data depository that holds configuration information for the Windows operating system and application programs. It provides a single point for administration and backup of system and application preferences. On the downside, the registry is also a single point of failure—if you mess up the registry, your computer could malfunction or even fail to boot!

We don't suggest that you use the registry to store configuration parameters for your Java programs. The java preferences API is a better solution (see Volume I, Chapter 13 for more information). We'll simply use the registry to demonstrate how to wrap a nontrivial native API into a Java class.

The principal tool for inspecting the registry is the *registry editor*. Because of the potential for error by naive but enthusiastic users, there is no icon for launching the registry editor. Instead, start a DOS shell (or open the Start → Run dialog box) and type `regedit`. Figure 12.4 shows the registry editor in action.

![](img/7dd923a566750151a3aab0dacd0cdaa5_1006_0.png)

**Figure 12.4** The registry editor

The left side shows the keys, which are arranged in a tree structure. Note that each key starts with one of the `HKEY` nodes like

- HKEY_CLASSES_ROOT
- HKEY_CURRENT_USER
- HKEY_LOCAL_MACHINE
- . . .

The right side shows the name/value pairs associated with a particular key. For example, if you installed Java SE 7, the key

```
HKEY_LOCAL_MACHINE\Software\JavaSoft\Java Runtime Environment
```

contains a name/value pair such as

```
CurrentVersion="1.7.0_10"
```

In this case, the value is a string. The values can also be integers or arrays of bytes.

### 12.10.2 A Java Platform Interface for Accessing the Registry

We create a simple interface to access the registry from Java code, and then implement this interface with native code. Our interface allows only a few registry operations; to keep the code size down, we omitted some important operations such as adding, deleting, and enumerating keys. (It should be easy to add the remaining registry API functions.)

Even with the limited subset that we supply, you can

- Enumerate all names stored in a key
- Read the value stored with a name
- Set the value stored with a name

Here is the Java class that encapsulates a registry key:

```java
public class Win32RegKey
{
   public Win32RegKey(int theRoot, String thePath) { . . . }
   public Enumeration names() { . . . }
   public native Object getValue(String name);
   public native void setValue(String name, Object value);

   public static final int HKEY_CLASSES_ROOT = 0x80000000;
   public static final int HKEY_CURRENT_USER = 0x80000001;
   public static final int HKEY_LOCAL_MACHINE = 0x80000002;
   . . .
}
```

The names method returns an enumeration that holds all the names stored with the key. You can get at them with the familiar hasMoreElements/nextElement methods. The getValue method returns an object that is either a string, an Integer object, or a byte array. The value parameter of the setValue method must also be of one of these three types.

### 12.10.3 Implementation of Registry Access Functions as Native Methods

We need to implement three actions:

- Get the value of a name
- Set the value of a name
- Iterate through the names of a key

Fortunately, you have seen essentially all the tools that are required, such as the conversion between Java strings and arrays and those of C. You also saw how to raise a Java exception in case something goes wrong.

Two issues make these native methods more complex than the preceding examples. The getValue and setValue methods deal with the type Object, which can be one of String, Integer, or byte[]. The enumeration object stores the state between successive calls to hasMoreElements and nextElement.

Let us first look at the getValue method. The method (shown in Listing 12.22) goes through the following steps:

1. Opens the registry key. To read their values, the registry API requires that keys be open.
2. Queries the type and size of the value associated with the name.
3. Reads the data into a buffer.
4. Calls NewStringUTF to create a new string with the value data if the type is REG_SZ (a string).
5. Invokes the Integer constructor if the type is REG_DWORD (a 32-bit integer).
6. Calls NewByteArray to create a new byte array, then SetByteArrayRegion to copy the value data into the byte array, if the type is REG_BINARY.
7. If the type is none of these or if an error occurred when an API function was called, throws an exception and releases all resources that had been acquired up to that point.
8. Closes the key and returns the object (String, Integer, or byte[]) that had been created.

As you can see, this example illustrates quite nicely how to generate Java objects of different types.

In this native method, coping with the generic return type is not difficult. The jstring, jobject, or jarray reference is simply returned as a jobject. However, the setValue method receives a reference to an Object and must determine the Object’s exact type to save the object as a string, integer, or byte array. We can make this determination by querying the class of the value object, finding the class references for
