documenting a program. In fact, after you've finished debugging your program, you will probably not relish the idea of going back to the program to insert comments. Inserting comments while developing the program makes this sometimes-tedious task a bit easier to handle.

This next line of Program 2.1 tells the compiler to locate and process a file named Foundation.h:

```
#import <Foundation/Foundation.h>
```

This is a system file—that is, not a file that you created. #import says to import or include the information from that file into the program, exactly as if the contents of the file were typed into the program at that point. You imported the file Foundation.h because it has information about other classes and functions that are used later in the program.

In Program 2.1, this line specifies that the name of the program is main:

```
int main (int argc, const char * argv[])
```

main is a special name that indicates precisely where the program is to begin execution. The reserved word int that precedes main specifies the type of value returns, which is an integer (more about that). We ignore what appears between the open and closed parentheses for now; these have to do with command-line arguments, a topic we address in Chapter 13, "Underlying C Language Features."

Now that you have identified main to the system, you are ready to specify precisely what this routine is to perform. This is done by enclosing all the program statements of the routine within a pair of curly braces. In the simplest case, a statement is just an expression that is terminated with a semicolon. The system treats all