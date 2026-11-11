You can also use the freely available Cygwin programming environment from www.cygwin.com. It contains the GNU C compiler and libraries for UNIX-style programming on Windows. With Cygwin, use the command

```
```bash
gcc -mno-cygwin -D __int64="long long" -I jdk/include/ -I jdk/include/win32 \\
    -shared -Wl,--add-stdcall-alias -o HelloNative.dll HelloNative.c
```
```

> **NOTE:** The Windows version of the header file `jni_md.h` contains the type declaration
> 
> ```c
> typedef __int64 jlong;
> ```
> 
> which is specific to the Microsoft compiler. If you use the GNU compiler, you might want to edit that file, for example,
> 
> ```c
> #if defined __GNUC__
>     typedef long long jlong;
> #else
>     typedef __int64 jlong;
> #endif
> ```
> 
> Alternatively, compile with `-D __int64="long long"`, as shown in the sample compiler invocation.

Finally, add a call to the System.loadLibrary method in your program. To ensure that the virtual machine will load the library before the first use of the class, use a static initialization block, as in Listing 12.4.

```
Listing 12.4  `helloNative/HelloNativeTest.java`

```java
/**
 * @version 1.11 2007-10-26
 * @author Cay Horstmann
 */
class HelloNativeTest
{
    public static void main(String[] args)
    {
        HelloNative.greeting();
    }

    static
    {
        System.loadLibrary("HelloNative");
    }
}
```
```