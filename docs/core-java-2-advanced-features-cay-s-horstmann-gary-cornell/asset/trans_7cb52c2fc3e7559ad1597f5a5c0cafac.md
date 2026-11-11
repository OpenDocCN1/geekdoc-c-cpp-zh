
java.lang.String、java.lang.Integer 和 byte[]，并使用 `IsAssignableFrom` 函数对它们进行比较。

如果 `class1` 和 `class2` 是两个类引用，那么调用

```
(env)->IsAssignableFrom(env, class1, class2)
```

当 `class1` 和 `class2` 是同一个类，或者 `class1` 是 `class2` 的子类时，返回 `JNI_TRUE`。在这两种情况下，对 `class1` 对象的引用都可以转换为 `class2`。例如，当

```
(env)->IsAssignableFrom(env, (*env)->GetObjectClass(env, value), (*env)->FindClass(env, "[B"))
```

为真时，我们就知道 `value` 是一个 `byte` 数组。

以下是 `setValue` 方法中步骤的概述：

- 1. 打开注册表项以进行写入。
- 2. 查找要写入的值的类型。
- 3. 如果类型是 `String`，调用 `GetStringUTFChars` 获取字符的指针。
- 4. 如果类型是 `Integer`，调用 `intValue` 方法获取包装器对象中存储的整数。
- 5. 如果类型是 `byte[]`，调用 `GetByteArrayElements` 获取字节的指针。
- 6. 将数据和长度传递给注册表。
- 7. 关闭注册表项。
- 8. 如果类型是 `String` 或 `byte[]`，释放数据指针。

最后，让我们来讨论枚举键的原生方法。这些是 `Win32RegKeyNameEnumeration` 类的方法（参见清单 12.21）。当枚举过程开始时，我们必须打开键。在枚举期间，我们必须保留键句柄——也就是说，键句柄必须与枚举对象一起存储。键句柄的类型是 `DWORD`（一个 32 位数量），因此它可以存储在 Java 整数中。我们将其存储在枚举类的 `hkey` 字段中。当枚举开始时，该字段使用 `SetIntField` 初始化。后续调用使用 `GetIntField` 读取该值。

在此示例中，我们随枚举对象存储另外三个数据项。当枚举首次开始时，我们可以向注册表查询名称/值对的数量以及最长名称的长度，这些是我们在分配 C 字符数组以保存名称时所需的信息。这些值存储在枚举对象的 `count` 和 `maxsize` 字段中。最后，`index` 字段以 `-1` 初始化以表示枚举开始，一旦其他实例字段初始化完成，它就被设置为 `0`，并在每次枚举步骤之后递增。

让我们来仔细看看支持枚举的原生方法。`hasMoreElements` 方法很简单：

- 1. 获取 index 和 count 字段。
- 2. 如果 index 为 -1，则调用 `startNameEnumeration` 函数，该函数会打开键、查询数量和最大长度，并初始化 `hkey`、`count`、`maxsize` 和 `index` 字段。
- 3. 如果 index 小于 count，则返回 `JNI_TRUE`，否则返回 `JNI_FALSE`。

`nextElement` 方法需要多做一点工作：

- 1. 获取 index 和 count 字段。
- 2. 如果 index 为 -1，则调用 `startNameEnumeration` 函数，该函数会打开键、查询数量和最大长度，并初始化 `hkey`、`count`、`maxsize` 和 `index` 字段。
- 3. 如果 index 等于 count，则抛出 `NoSuchElementException`。
- 4. 从注册表读取下一个名称。
- 5. 递增 index。
- 6. 如果 index 等于 count，则关闭键。

在编译之前，记得对 `Win32RegKey` 和 `Win32RegKeyNameEnumeration` 运行 `javah`。微软编译器的完整命令行是

```
cl -I jdk\include -I jdk\include\win32 -LD Win32RegKey.c advapi32.lib -FeWin32RegKey.dll
```

在 Cygwin 下，使用

```
gcc -mno-cygwin -D __int64="long long" -I jdk\include -I jdk\include\win32
    -I C:\cygwin\usr\include\w32api -shared -Wl,--add-stdcall-alias -o Win32RegKey.dll
    Win32RegKey.c
```

由于注册表 API 是特定于 Windows 的，此程序在其他操作系统上将无法运行。

清单 12.23 展示了一个测试我们新注册表函数的程序。我们向键

```
HKEY_CURRENT_USER\Software\JavaSoft\Java Runtime Environment
```

添加三个名称/值对：一个字符串、一个整数和一个字节数组。然后我们枚举该键的所有名称并检索它们的值。程序将打印

```
Default user=Harry Hacker
Lucky number=13
Small primes=2 3 5 7 11 13
```

虽然向该键添加这些名称/值对可能不会造成损害，但在运行此程序后，您可能希望使用注册表编辑器删除它们。

## 清单 12.21 Win32Reg/Win32RegKey.java

```java
import java.util.*;

/**
 * A Win32RegKey object can be used to get and set values of a registry key in the Windows
 * registry.
 * @version 1.00 1997-07-01
 * @author Cay Horstmann
 */
public class Win32RegKey
{
    public static final int HKEY_CLASSES_ROOT = 0x80000000;
    public static final int HKEY_CURRENT_USER = 0x80000001;
    public static final int HKEY_LOCAL_MACHINE = 0x80000002;
    public static final int HKEY_USERS = 0x80000003;
    public static final int HKEY_CURRENT_CONFIG = 0x80000005;
    public static final int HKEY_DYN_DATA = 0x80000006;

    private int root;
    private String path;

    /**
     * Gets the value of a registry entry.
     * @param name the entry name
     * @return the associated value
     */
    public native Object getValue(String name);

    /**
     * Sets the value of a registry entry.
     * @param name the entry name
     * @param value the new value
     */
    public native void setValue(String name, Object value);

    /**
     * Construct a registry key object.
     * @param theRoot one of HKEY_CLASSES_ROOT, HKEY_CURRENT_USER, HKEY_LOCAL_MACHINE, HKEY_USERS,
     * HKEY_CURRENT_CONFIG, HKEY_DYN_DATA
     * @param thePath the registry key path
     */
    public Win32RegKey(int theRoot, String thePath)
    {
        root = theRoot;
        path = thePath;
    }

    /**
     * Enumerates all names of registry entries under the path that this object describes.
     * @return an enumeration listing all entry names
     */
    public Enumeration<String> names()
    {
        return new Win32RegKeyNameEnumeration(root, path);
    }

    static
    {
        System.loadLibrary("Win32RegKey");
    }
}

class Win32RegKeyNameEnumeration implements Enumeration<String>
{
    public native String nextElement();
    public native boolean hasMoreElements();
    private int root;
    private String path;
    private int index = -1;
    private int hkey = 0;
    private int maxsize;
    private int count;

    Win32RegKeyNameEnumeration(int theRoot, String thePath)
    {
        root = theRoot;
        path = thePath;
    }
}

class Win32RegKeyException extends RuntimeException
{
    public Win32RegKeyException()
    {
    }

    public Win32RegKeyException(String why)
    {
        super(why);
    }
}
```

## 清单 12.22（续）

```c
(*env)->ReleaseStringUTFChars(env, path, cpath);
cname = (*env)->GetStringUTFChars(env, name, NULL);

/* find the type and size of the value */
if (RegQueryValueEx(hkey, cname, NULL, &type, NULL, &size) != ERROR_SUCCESS)
{
    (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
                     "Query value key failed");
    RegCloseKey(hkey);
    (*env)->ReleaseStringUTFChars(env, name, cname);
    return NULL;
}

/* get memory to hold the value */
cret = (char*)malloc(size);

/* read the value */
if (RegQueryValueEx(hkey, cname, NULL, &type, cret, &size) != ERROR_SUCCESS)
{
    (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
                     "Query value key failed");
    free(cret);
    RegCloseKey(hkey);
    (*env)->ReleaseStringUTFChars(env, name, cname);
    return NULL;
}

/* depending on the type, store the value in a string,
   integer or byte array */
if (type == REG_SZ)
{
    ret = (*env)->NewStringUTF(env, cret);
}
else if (type == REG_DWORD)
{
    jclass class_Integer = (*env)->FindClass(env, "java/lang/Integer");
    /* get the method ID of the constructor */
    jmethodID id_Integer = (*env)->GetMethodID(env, class_Integer, "<init>", "(I)V");
    int value = *((int*) cret);
    /* invoke the constructor */
    ret = (*env)->NewObject(env, class_Integer, id_Integer, value);
}
else if (type == REG_BINARY)
{
    ret = (*env)->NewByteArray(env, size);
    (*env)->SetByteArrayRegion(env, (jarray) ret, 0, size, cret);
}
```

