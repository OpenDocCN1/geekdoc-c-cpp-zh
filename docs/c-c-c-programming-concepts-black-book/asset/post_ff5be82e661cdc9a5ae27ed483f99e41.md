
![](img/43c5f409f9b17790a628c4b4df854b61_316_0.png)

## 11 Cross Compilation in C

| If you need an Information on: | See page: |
|---|---:|
| Compiling C Code in Linux Environment | 276 |
| Cross Compilation | 277 |

A cross compiler is capable of creating executable codes for a platform that is different from the one on which the compiler itself is running. Cross compilers are used when it is not feasible to compile the code on the platform where the code would be executed. It might happen that an organization wants to run the code on multiple platforms. In such case, a single build environment could be used along with a cross compiler. Usually, cross compilers are used for the embedded systems.

In this chapter, we learn how to compile a C code in the Linux environment. Then, the chapter discusses the basics of cross compilation.

### Compiling C Code in Linux Environment

Before cross compilation, we must learn how the C code are compiled using various options with the compiler. For this, let's consider the Linux environment. To compile the C code in Linux, we need to first create a C file in Linux using a text editor, such as vim. Consider the following sample program called hello.c created in the Linux environment:

```c
#include<stdio.h>
int main()
{
    printf("\n This is test ");
    return();
}
```

Compilation of C programs is done by using a standard gcc compiler. The hello.c program can be compiled by using the following command:

```bash
gcc hello.c -o hello
```

The preceding command compiles the hello.c program into an executable file, named hello. This executable file can be run from the command line by just typing the word hello.

The hello.c program can also be compiled by using the following commands:

```bash
gcc -c hello.c
gcc hello.o -o hello
```

The first command performs the compilation and creates the assembly of the source file without linking it. Output of the first command will be an object code file, hello.o. The second command links the hello.o file with the standard library functions and the system libraries to produce the final executable. The intermediate file, hello.o, will be deleted in this process.

Various options can be used with the gcc compiler during compilation. For instance, the -g option instructs the compiler to include the debugging information in the generated code. The -g option can be used as follows:

```bash
gcc -g testProg.c -o testProg
```

Using the -g option, the object code is generated in such a way that it will contain symbols that could be used while running the code with the gdb debugger.

Another important option is -Wall, which displays all the warnings that are possible in the code. The warnings can arise in the code due to several reasons, such as uninitialized variables, unused variables, and mismatched return types. The -Wall option can be used as follows:

```bash
gcc -g -Wall testProg.c -o testProg
```

The gcc compiler also allows programmers to mention the optimization level while using the -g option. The optimization level is mentioned by using the -o option, shown as follows:

```bash
gcc -O testProg.c -o testProg
```

Various levels of optimization are possible with the -o option. The range of optimization goes from -O1 to -O3. These levels of optimization are used for speed. For instance, the -O0 value is used for no optimization. While debugging a code, it is advised not to have any sort of optimizations in the code, as the optimized code would not have proper debug symbols, which are required by the standard gnu debuggers for debugging.

The -I option is used to include the header files in the object code. This option can be used as follows:

```bash
gcc testProg.c -o testProg -lm
```

The -I option informs the gcc compiler where to look for the header files used in the code.

It is also possible to compile a program that contains multiple source files. The command used for compiling this type of program is given as follows:

```bash
gcc file1.c file2.c -o myprog
```

As the file1.c and file2.c files contain the source code, both the files need to be compiled before creating an object file. A similar result could have been achieved if the code was compiled with the following options:

```bash
gcc -c file1.c
gcc -c file2.c
gcc file1.o file2.o -o myprog
```

The advantage of the third command is that it compiles each of the source files separately. It might happen that the file1.c file is modified when the compiler tries to create the myprog file. In this scenario, only file1.c will be recompiled but not file2.c. This will speed up the compilation to some extent.

Next, let’s learn about cross compilation.

### Cross Compilation

Whenever we build a code in the Linux environment, the host and target platforms should always be same. This is because the binary, which is created after the compilation, runs on the same platform. Now, suppose we want to run the binary on a different platform. In such case, we cannot directly load the binary into the target platform and expect it to execute. For this, we need to compile the code keeping in mind the architecture of the target platform. This sort of compilation is known as cross compilation.

The gcc compiler is frequently used for cross compilation. This compiler requires that the compiled copy of binary is available for each target platform. For this, the binary needs to be compiled with the correct --target option. In addition, the gcc compiler needs to be properly configured with the same --target option. After this, the gcc compiler can run normally.

Cross compilation in gcc requires some portions of the target platform’s C library functions to be available on the host system as well. Instead of compiling the full standard library, some part of it could be compiled. Another useful method is to use the newlib option, which is a small C library that contains only the essential information.

Cross compilation can be done easily with the help of GNU Autotools packages. The Autotools packages have an option of mentioning a build platform, a target platform, and a host platform. The build platform is the platform where the compiler is compiled. Generally, it is left unaltered, as it is default for the host platform. The host platform is the platform where the output of the source code is executed. On the other hand, the target platform is required for the cross compilation. It represents what type of object code the package itself will produce.

Now, consider a scenario where we want to cross compile a code so that it can run on the Intel PowerPC driven system. Perform the following steps to cross compile the code:

- 1. Download the binutils-2.14, gcc-3.3.2, glibc-2.3.2, glibc-linuxthreads-2.3.2, and gdb-6.0 (optional) bundles from the http://gcc.gnu.org/releases.html link.
- 2. Build all the bundles. It is advised to build the bundles at a different directory from where it was unzipped. Now, mention powerpc as the target while configuring the binutils. This is done by setting the --target option to powerpc-linux. Use the following commands to build the bundles:

```bash
mkdir build-binutils && cd build-binutils
../binutils-2.14/configure --target=powerpc-linux --prefix=/opt/buckeye/powerpc-linux
make all install
```

- 3. Add the cross-compiled binaries into the path, shown as follows:

```bash
export PATH=$PATH:/opt/buckeye/powerpc-linux
mkdir build-gcc && cd build-gcc
../gcc-3.3.2/configure --target=powerpc-linux --prefix=/opt/buckeye/powerpc-linux \
--disable-shared --disable-threads \
--enable-languages=c --with-newlib
make all-gcc install-gcc
```

After setting the path, we can start cross compiling with minimal gcc.

Now, we need to cross compile glibc as well.

- 4. Download glibc-linuxthreads to build glibc for cross compilation. Use the following command for cross compiling glibc:

```bash
mkdir build-glibc && cd build-glibc
tar xvzf ../glibc-linuxthreads-2.3.2.tar.gz ../glibc-2.3.2/
../glibc-2.3.2/configure --prefix=/opt/buckeye/powerpc-linux --target=powerpc-linux \
--enable-add-ons=linuxthreads \
--with-headers=${PATH_to_your_powerpc_linux_kernel_tree}/linuxppc_2_4_devel/include \
--with-binutils=/opt/buckeye/powerpc-linux/powerpc-linux/bin
make all install
```

glibc can give an error for glibc-2.3.2/stdio-common/sscanf.c ...; therefore, we need to change the signature of the file as follows:

```c
int sscanf (const char *s, const char *format, ...)
```

- 5. Reconfigure the gcc compiler as follows:

```bash
../gcc-3.3.2/configure --target=powerpc-linux --prefix=/opt/buckeye/powerpc-linux \
--enable-shared --enable-threads \
--enable-languages=c
make all install
```

Let's now summarize the main points discussed in the chapter.

### Summary

In this chapter, we have learned how to compile a C code in the Linux environment by using various options, such as -g and -o. Further, we have learned about the basics of cross compilation.

### Quick Revise

#### Multiple Choice Questions

- Q1. Which of the following option is used to raise all the warnings in a code?
    - i. -Wall
    - ii. -Werror
    - iii. -O
    - iv. None of the above

- Q2. Which of the following option is used to instruct the compiler to include the debug symbols?
    - i. -g
    - ii. -O
    - iii. -P
    - iv. -w

#### Subjective Questions

- Q1. Explain the process of cross compilation.

- Q2. Devise a scheme to perform cross compilation on the x86_64 platform by taking the help from the steps shown in the chapter.
