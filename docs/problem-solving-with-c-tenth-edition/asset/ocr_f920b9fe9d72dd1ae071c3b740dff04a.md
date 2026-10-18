worked in the function declaration also serves as the variable declaration. The following is the wrong way to start the function definition for fee as it declares minutesWorked twice:

```
double fee(int hoursWorked, int minutesWorked)
{
    int quarterHours;
    int minutesWorked;
    ...
}
```

Do NOT do this!

# Block Scope

The scope of a local variable refers to the part of a program that can directly access that variable and is sometimes referred to as local scope. Similarly, global identifiers declared at the beginning of your program, outside of the body of all the functions, are sometimes referred to as having global scope. Despite their differences, local and global identifiers are really examples of block scope described in Chapter 3. A block is some C++ code enclosed in braces, with the exception of the “global block,” which is an implied outermost block that encompasses all code. The scope rule states that identifiers declared within their block are local to that block and accessible only from the point they are defined to the end of their block. Blocks are commonly nested. For example, the braces of the main function defines a block and a for loop inside main defines a nested block.

The program outlined in Display 4.14 doesn’t compute anything interesting but illustrates the scope of identifiers declared in different blocks. In this example, the constant GLOBAL_CONST has global scope, along with the functions function1 and main, because they are declared outside the body of all functions. This allows us to access GLOBAL_CONST from both main and function1.

The main function declares the variables x and d that are local to main. Their scope extends to the end of main’s block. Similarly, the function function1 has a parameter param and a local variable y that have scope extending to the end of function1. Neither of these variables is directly accessible from outside their scope. The scope of local variables and parameters really uses the same rule of block scope, but in this case the block refers to the function in which the variables or parameters are declared.

The for loop in Display 4.14 illustrates the scope of a nested block. The variable i is declared inside the for loop and thus only has scope to the end of the loop block. Attempts to reference i anywhere outside its scope, even if we are still inside main (for example, on line 17) would result in a compiler error.

You can think of variables as being created when their scope begins and destroyed when their scope ends. For example, the local variable y in Display 4.14 is created and initialized to GLOBAL_CONST every time function1 is called. If code on line 23 changed the value stored in y, then these changes would be lost when the function exits and y goes out of scope because the variable y is