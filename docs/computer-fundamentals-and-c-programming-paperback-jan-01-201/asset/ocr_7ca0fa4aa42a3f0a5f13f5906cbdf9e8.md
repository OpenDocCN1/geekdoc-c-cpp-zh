# 4.5 EDITING, COMPILING AND EXECUTING `first_prog.c`

Make a separate directory on your system for the C programs that you’ll develop. Using a text editor, key in this program to create the source file, **first_prog.c**. We use a text editor instead of a word processing software like Microsoft Word because C source programs are text, and not binary, files. Using the following guidelines would stand you in good stead:

+   - Indent the text as shown in the program listing. Proper indentation helps in both understanding and maintenance, so use the [Tab] (↹) key to provide indentation.
+   - Don’t fail to provide the `;` which is seen at the end of most lines.
+   - Don’t terminate statements beginning with `#define` and `#include` with a semicolon.
+   - C is case-sensitive, so don’t use uppercase except where shown.
+   - Don’t use single quotes where double quotes have been specified, and vice versa.

After you have input your program, save it as **first_prog.c**. You are now ready to start the compilation process. Compiler-specific information follows next, so you will need to refer to either Section 4.3.1 or Section 4.3.2.

![](bbox=[0.088, 0.451, 0.125, 0.475])

**Caution:** Remember to terminate every C statement with the semicolon. A compiler generates errors if it doesn’t find it even though it may not properly identify the location where the semicolon should have been placed.

# 4.5.1 Using gcc (Linux)

To input your program, you may choose the **vim** or **emacs** editors, two of the most notable and powerful editors supported by Linux. (Versions for Windows are also freely available.) After saving the file, use the **gcc** command to compile **first_prog.c**:

```
```text
$ gcc first_prog.c
$ _                         Prompt returns; compilation successful
```
```

By default (as above), **gcc** first invokes the preprocessor (**cpp**), then does the job of compiling itself, and finally calls the linker (**ld**) to create the executable—all in a single invocation. The silent return of the prompt indicates that no syntax errors have been encountered and that the default executable file, **a.out**, has been created. Run the **ls** command now to verify the presence of this file.

You can now invoke the executable in this manner to produce the output shown after the program listing (Program 4.1):

```
```text
$ ./a.out
All numbers are stored in binary
Radius of circle = 5
Area of circle having radius 5 = 78.550003
```
```

The output is correct, which means there are no semantic errors in your program. In case you see syntactical error messages, note the line numbers of the offending locations from these messages. Correct the source code and recompile the program. Handling error messages is taken up in Section 4.6.