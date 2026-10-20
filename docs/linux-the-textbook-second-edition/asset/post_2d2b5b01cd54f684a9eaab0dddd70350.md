
Static analysis tools allow you to measure these parameters as well as report bugs that the compiler does not catch such as finding memory leaks, invalid pointers, and other memory problems. Some of the commonly used Linux tools for this purpose are cppcheck, valgrind, and memcheck. Some of the valgrind tools can profile your programs in detail in addition to automatically detecting memory-related bugs. gprof also allows you to profile your program comprehensively. All of these tools supplement a source code debugger (discussed in Section 14.7).

In the following sections, we discuss briefly cppcheck and gprof that allow you to perform these analyses.

## 14.6.1 Verifying Code for Portability with cppcheck

Most C compilers do fairly well at checking for type mismatches, but few handle portability. You can use cppcheck, which is a static analysis tool that comes preinstalled on Linux Mint 18. It is also integrated in many popular program development environments including Code::Blocks, Eclipse, git, and Visual Studio.

You can use it to identify bugs in your C/C++ software that compilers normally do not detect. It is one of the most useful tools in Linux for developing high-quality, clean, and portable C software. It detects program features that are likely to be bugs, nonportable, or wasteful of system resources. However, it reports real bugs and no false warnings. It also does not report structural problems, such as variables declared but not used and unreachable code. cppcheck can detect various types of bugs in your code and reports accordingly, including the following:

- Out of bounds checking
- Memory leaks
- Null pointer dereferences
- Use of obsolete or unsafe functions

You can use the `cppcheck --doc` command to display the list of checks performed by cppcheck. Although cppcheck can handle various compiler extensions, inline assembly code, and preprocessor files, the discussion here is limited to its use with C program files. The following is a brief description of the cppcheck command.

**Syntax:** `cppcheck [options] [file(s) or path(s)]`

**Purpose:** Analyze the given source file(s), or files in case of directory, for errors that a compiler may not catch

**Commonly used options/features:**

| Option | Description |
|---|---|
| `--doc` | Display the list of checks performed by cppcheck |
| `--inconclusive` | Report error even if analysis is inconclusive; false positives are possible in this case |
| `-v` | Report more detailed errors |

If the specified path is a directory, cppcheck recursively checks for all source files and analyzes them. We demonstrate the use of cppcheck with simple programs shown in the following session to illustrate that it reports out-of-bounds problem, null pointer dereferencing, and memory leaks. We have used the nl command with `-ba` option to number all the source lines (including blank lines), because the line numbers reported in cppcheck’s error messages include blank lines.

```bash
$ nl -ba buggy1.c
1  /* Out of bounds check */
2  #define SIZE 10
3
4  int main()
5  {
6      char str[SIZE];
7
8      str[SIZE] = '\0';
9      return 0;
10 }
$ gcc buggy1.c -o buggy1
$ cppcheck buggy1.c
Checking buggy1.c...
[buggy1.c:8]: (error) Array 'str[10]' accessed at index 10, which is out of bounds.
$
```

In the following buggy2.c program, we show how cppcheck reports the null pointer dereferencing error that gcc couldn't detect.

```bash
$ cat buggy2.c
/* Null pointer dereferencing error */
int main()
{
    char *str;

    *str = '\0';
}
$ gcc buggy2.c
$ cppcheck buggy2.c
Checking buggy2.c...
[buggy2.c:6]: (error) Uninitialized variable: str
$
```

The following example illustrates the memory leak that wasn't reported by gcc but caught by cppcheck.

```bash
$ cat buggy3.c
/* Memory leak bug */
#include <stdlib.h>

struct student {
    char name[100];
    int ID;
};

int main()
{
    struct student s;
    char *s1, *s2;
    int size;
    size = sizeof(s);
    s1 = malloc(size);
    s2 = malloc(size);
    free(s1);

    return 0;
}
$ gcc buggy3.c
$ cppcheck buggy3.c
Checking buggy3.c...
[buggy3.c:20]: (error) Memory leak: s2
$
```

You can specify multiple files in the command line, as shown in the following session.

```bash
$ cppcheck buggy1.c buggy2.c buggy3.c
Checking buggy1.c...
[buggy1.c:8]: (error) Array 'str[10]' accessed at index 10, which is out of bounds.
1/3 files checked 25% done
Checking buggy2.c...
[buggy2.c:6]: (error) Uninitialized variable: str
2/3 files checked 43% done
Checking buggy3.c...
[buggy3.c:20]: (error) Memory leak: s2
3/3 files checked 100% done
$
```

### Exercise 14.12

Go through all the sessions presented in this section to appreciate how cppcheck works. Does cppcheck produce the same error messages on your system for all the buggy programs discussed in this section?

### Exercise 14.13

Run the `cppcheck --doc` command to find out the types of errors that cppcheck reports.

We strongly recommend that you create a make rule for running the cppcheck utility on your modules before compiling them. The following is an example make rule and its execution:

```bash
$ cat makefile
SOURCES = compute.c input.c main.c
CPPCHECKFLAGS =
...
cppcheck:    $(SOURCES)
	cppcheck $(CPPCHECKFLAGS) $(SOURCES)
...
$ make cppcheck
cppcheck compute.c input.c main.c
...
$
```

## 14.6.2 Source Code Metrics with gprof

Software profiling is important because it allows you to identify function call sequences and portions of your software that are time consuming. This information allows you to focus more closely on those code portions or functions that are causing bottlenecks in the software. You can rewrite such pieces of code to make them more time efficient and make your programs execute faster. With profiling, you can also identify functions in your program that are being called with higher or lower frequency than expected. This information may help you identify bugs in your program that might have gone unnoticed otherwise.

The profiler builds its data based on the actual execution of a program. Thus, while profiling a complex or a large program, it is important that you run it with input that invokes all of its features during execution. If the program input does not invoke a set of program features, no profile information will be collected for them.

To obtain a profile of a program and analyze it, you need to perform the following steps:

1. Compile and link your software with profiling enabled
2. Run the software to collect profile information in a file
3. Analyze the profile information by running a profiling tool with the profile file as input

With the profiling option enabled, the compiler inserts appropriate code in the object module to count the number of times each function is executed, construct function call sequences, and gather the time spent in each function. The profiling tool may generate output in the form of a flat profile, call graph, or annotated source code file.

The flat profile output shows the amount of time each function took when the program executed. The call graph shows the function call sequence and the amount of time taken by a function and children (i.e., the called functions). This allows you to identify function call sequences that may cause bottlenecks in the program. Lastly, in the annotated source code file each function is labeled with its call frequency (i.e., the number of times it was called).

Several profiling tools are available for Linux, however, gprof and perf are most famous. Whereas perf is mostly used to profile the use of hardware components, commands, and processes, gprof is meant for source code profiling. Although gprof is a powerful tool with a whole array of options for performing various types of analyses on the profile data file, we briefly describe its use with a small example. Here is a brief description of gprof:

**Syntax:** `gprof [options]`

**Purpose:** Produces execution profile of programs written in C and a few other languages

**Commonly used options/features:**

- `-A` — Display profile of the program as annotated source code
- `-c` — Display the function names and the number of times each was called
- `-p` — Display flat profile
- `-q` — Display profile as a call graph

We use a small C program in the gprof_test.c file to illustrate the use of gprof. First, we compile the program with the `-pg` option to enable profiling in the resultant executable file. We also use the `-Wall` option so that the compiler reports all sorts of warnings. Second, we run the program to generate the profile data file, gmon.out. Finally, we run the gprof command to analyze the data in gmon.out and display the profile information in one of the three forms discussed earlier. In order to generate the annotated source file, you must compile the source code with the `-g` option, in addition to the `-pg` option.

The following session shows an example C program and the steps required to generate the profile information. In this case, we save the profile information in the file called prof.out. Note that without an option, gprof generates the flat profile followed by call graph, as shown by the cat command at the end of the session. The terminology used in the output is also explained in the output (that we have truncated to save space). The flat profile shows that functions f1, f2, and f3 were called 1, 1025, and 1074790401 times, respectively. It further shows that the total time taken by the program to complete was 0.87 s, out of which 0.47 s (i.e., 54.12% of the total time—see column of the output) was taken by f3.

```bash
$ cat gprof_test.c
/* Example for gprof */
#include <stdio.h>

#define COUNT1 1024
#define COUNT2 1048576 /* 1024 x 1024 */

void f1(int);
void f2(int);
void f3(void);

int main(void)
{
    f1(COUNT1);
    f2(COUNT2);
    f3();
```
