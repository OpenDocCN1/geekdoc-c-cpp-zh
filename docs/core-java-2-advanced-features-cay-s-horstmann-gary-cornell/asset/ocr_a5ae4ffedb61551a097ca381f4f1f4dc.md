With the Microsoft compiler under Windows, the command is

```
cl -I jdk\include -I jdk\include\win32 -LD HelloNative.c -FeHelloNative.dll
```

Here, jdk is the directory that contains the JDK.

> **TIP:** If you use the Microsoft compiler from a command shell, first run a batch file such as vcvars32.bat or vcvarsall.bat. That batch file sets up the path and the environment variables needed by the compiler. You can find it in the directory c:\Program Files\Microsoft Visual Studio 14.0\Common\Tools, or a similar monstrosity. Check the Visual Studio documentation for details.

You can also use the freely available Cygwin programming environment from www.cygwin.com. It contains the GNU C compiler and libraries for UNIX-style programming on Windows. With Cygwin, use the command

```
gcc -mno-cygwin -D __int64="long long" -I jdk/include/ -I jdk/include/win32
-shared -Wl,--add-stdcall-alias -o HelloNative.dll HelloNative.c
```

Type the entire command on a single line.

> **NOTE:** The Windows version of the header file jni_md.h contains the type declaration
> 
> typedef __int64 jlong;
> 
> which is specific to the Microsoft compiler. If you use the GNU compiler, you might want to edit that file, for example,
> 
> #ifdef __GNUC__
> typedef long long jlong;
> #else
> typedef __int64 jlong;
> #endif
> 
> Alternatively, compile with -D __int64="long long", as shown in the sample compiler invocation.

Finally, add a call to the System.loadLibrary method in your program. To ensure that the virtual machine will load the library before the first use of the class, use a static initialization block, as in Listing 12.4.

Figure 12.1 gives a summary of the native code processing.

After you compile and run this program, the message “Hello, Native World!” is displayed in a terminal window.