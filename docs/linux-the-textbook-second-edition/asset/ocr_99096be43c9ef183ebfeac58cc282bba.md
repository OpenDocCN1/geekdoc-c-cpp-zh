Static analysis tools allow you to measure these parameters as well as report bugs that the compiler does not catch such as finding memory leaks, invalid pointers, and other memory problems. Some of the commonly used Linux tools for this purpose are cppcheck, valgrind, and memcheck. Some of the valgrind tools can profile your programs in detail in addition to automatically detecting memory-related bugs. gprof also allows you to profile your program comprehensively. All of these tools supplement a source code debugger (discussed in Section 14.7).

In the following sections, we discuss briefly cppcheck and gprof that allow you to perform these analyses.

# 14.6.1 Verifying Code for Portability with cppcheck

Most C compilers do fairly well at checking for type mismatches, but few handle portability. You can use cppcheck, which is a static analysis tool that comes preinstalled on Linux Mint 18. It is also integrated in many popular program development environments including Code::Blocks, Eclipse, git, and Visual Studio.

You can use it to identify bugs in your C/C++ software that compilers normally do not detect. It is one of the most useful tools in Linux for developing high-quality, clean, and portable C software. It detects program features that are likely to be bugs, nonportable, or wasteful of system resources. However, it reports real bugs and no false warnings. It also does not report structural problems, such variables declared but not used and unreachable code. cppcheck can detect various types of bugs in your code and reports accordingly, including the following:

+   - Out of bounds checking
+   - Memory leaks
+   - Null pointer dereferences
+   - Use of obsolete or unsafe functions

You can use the `cppcheck --doc` command to display the list of checks performed by cppcheck. Although cppcheck can handle various compiler extensions, inline assembly code, and preprocessor files, the discussion here is limited to its use with C program files. The following is a brief description of the cppcheck command.

**Syntax:**

`cppcheck [options] [file(s) or path(s)]`

**Purpose:** Analyze the given source file(s), or files in case of directory, for errors that a compiler may not catch

**Commonly used options/features:**

| Option | Description |
|---|---|
| `--doc` | Display the list of checks performed by cppcheck |
| `-inconclusive` | Report error even if analysis is inconclusive; false positives are possible in this case |
| `-v` | Report more detailed errors |

If the specified path is a directory, cppcheck recursively checks for all source files and analyzes them. We demonstrate the use of cppcheck with simple programs shown in the following session to illustrate that it reports out-of-bounds problem, null pointer dereferencing, and memory leaks. We have used the nl command with -ba option to number all the source lines (including blank lines), because the line numbers reported in cppcheck’s error messages include blank lines.

```
```bash
$ nl -ba buggy1.c
```
```c
1  /* Out of bounds check */
2  #define SIZE 10
3
4  int main()
```
```