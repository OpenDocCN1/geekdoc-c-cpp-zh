Here are the specific steps:

+   1. **Edit the source code to match Listing 3-5.**
+   That's not a misprint. The source code is blank, empty. If you're using Code::Blocks, erase the skeleton provided.
+   2. **Save the source code.**
+   3. **Build.**
+   Nothing happens or you see a linker error message.

# LISTING 3-5: A Simple Program That Does Nothing

Because the source code is empty, no object code is generated. Even if a program is created, it's empty and does nothing. That's what you told the compiler to do, and the resulting program did it well.

# Setting the main() function

All C programs have a main() function. It's the first function that's run when a program starts. As a function, it requires parentheses for its arguments but also curly brackets to hold the function's statements in a block, as shown in Listing 3-6.

**Continue with Exercise 3-1:** Rebuild the source code `ex0301.c`, as shown in Listing 3-6. Save the project. Build and run.

# LISTING 3-6: The main() Function

```
main() {}
```

You may see a warning because the main() function lacks a data type. That's okay. Otherwise, the program generates no output — which is great! You didn't direct the code to do anything, and it did it well. What you see is the minimum C program. It's also known as the dummy program.