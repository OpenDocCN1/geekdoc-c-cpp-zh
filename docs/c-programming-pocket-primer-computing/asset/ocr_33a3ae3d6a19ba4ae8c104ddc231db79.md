variable. Notice the conditional logic: if the putenv() command fails, an error message is displayed.

The last portion of the main() function invokes the getenv() function again and displays the result, just to confirm that the PATH variable was updated correctly. The output (truncated for brevity) from compiling and executing the code in Listing 7.15 is here:

The current path is: /opt/spark/bin:/Users/owner/mongodb-osx-x86_64-3.4.2/bin:/Users/owner/anaconda2/bin:

The new path is: /:/home/userid

Keep in mind that after the program finishes execution, the PATH variable will retain its initial value (i.e., the change is temporary).

# STORAGE CLASS SPECIFIERS IN C

There are 5 storage class specifiers in C:

+   - auto
+   - extern
+   - static
+   - register
+   - _Thread_local

The auto storage specifier indicates a variable has automatic storage duration. This is rarely used since it is the default. The extern keyword has to do with external linkage and is primarily used when declaring global variables in a header file. The static keyword has different meanings depending on context. It may declare a variable with static storage duration, which means its value persists over multiple invocations of a function. It may also declare a variable to have internal linkage.