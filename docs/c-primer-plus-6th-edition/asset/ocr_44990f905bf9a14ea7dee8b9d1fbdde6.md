# Storage Duration, Scope, and Linkage

function, for example, uses the local definition of warming when it displays the value of warming.
C++ goes a step beyond by offering the scope-resolution operator (::). When it is fixed to the name of a variable, this operator means to use the global version of that variable. Thus, local() displays warming as 0.8, but it displays ::warming as 0.4. You'll encounter this operator again in namespaces and. In terms of clarity and avoidance, it would have been better and safer to use ::warming in the update() function instead of just using warming and relying on scope rules.

# Global Versus Local Variables

Now that you have a choice of using global or local variables, which should you use? At first, global variables have a seductive appeal—because all functions have access to a global variable, you do not have to bother passing arguments. But this easy access has a heavy price: unreliable programs. Computing experience has shown that the better your program does of isolating from unnecessary, the better the program does in preserving the integrity of the data. Most, you should use local variables and functions on a need-know basis rather than make data available indiscriminately by using global variables. As you see, OOP takes this isolation a step further.
Global variables have their uses, For example, you might have a block of data that's to be used by several functions, such as an array of month names or the atomic weights of the elements. The external storage class is particularly suited to protecting constant data by you use the keyword const to protect the data from change:

```
const char * const months[12] = {
    "January", "February", "March", "April", "May",
    "June", "July", "August", "September", "October",
    "November", "December"
};
```

In this example, the first const protects the string from change, and the second const makes sure that each pointer points to the same string which it initialized.

# Static Duration, Internal Linkage

Applying the static modifier to a file-scope variable gives it internal linkage. The difference between internal linkage and external linkage becomes meaningful in multifile programs. In this context, a variable with internal linkage means it is local to the file that it contains. But a regular external variable has external linkage, meaning that it can be used in different files, as the previous example showed.

What if you want to use the same name to denote different variables in different files? Can you just omit the extern?