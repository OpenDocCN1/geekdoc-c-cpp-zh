# 3.3. Using OneCompiler

# 3.3.3 Debugging Practice

Just to see what will happen, let's make a couple of mistakes on purpose.

+   1. Use the delete key to erase the closing " (double quote character) after the word world in your program. Now try to compile and run the program. The Compilation should fail and several errors are listed. This is common – one mistake may cause several error messages. You should be try to fix the first error (which is usually indicated by the first or first few messages) and re-run. In this case, the first error mentions "missing terminating " and a line number (line 4 if you typed in the program as shown) which will usually indicate the location of the error.
2. Now deleting the semicolon at the end of the line. Run. You see the same error even when we know there are two errors. This often happens: one "hides" another. Restore the " but leave the ; missing. Run. Now you see the message "error expected '; before 'return'.
3. Restore the program to its original form then change the character string to "\n, world". That's a backslash before the n. Run the program. Notice there is now a back line at the top of the output. The sequence "\n" makes the output down one line.
4. Try again using a forward slash to see what will happen.
5. Try displaying "Hello" and "world" on different lines.
6. Misspell the main word. Make it "maain". Run. A Linker error should show up in the Compile Info. Read the displayed message. This illustrates that some error messages are not entirely clear.
7. Finally, try displaying "Hello," and "world" on different lines.

# 3.3.4 Another Version of Hello World

Reload the editor for a new project. Google for a Hello World program in C on the Internet. It might look like this:

```
#include <stdio.h>
/* My first program */
int main() {
    printf("Hello, World!\n"); // prints Hello, World!
    return 0;
}
```

Copy this code and paste it into the editor. You can also access it online at https://onecompiler.com/c/423rmrj3. Let's explore how this is different from the default Hello World program on OneCompiler.

```
#include <stdio.h>
```

This line is exactly the same as before. We need this line to use printf().

```
/* My first program */
```