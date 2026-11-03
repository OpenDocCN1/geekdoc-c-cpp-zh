quality of the random sequence produced and some implementations are known to produce sequences with *distressingly* non-random low-order bits.² The CERT guideline MSC30-C indicates that implementation-specific random-number generation functions must be used to ensure that the random numbers produced are *not predictable*—this is extremely important, for example, in cryptography and other security applications. The guideline presents several platform-specific random-number generators that are considered to be secure. For example, Microsoft Windows provides the CryptGenRandom function, and POSIX based systems (such as Linux) provide a random function that produces more secure results. For more information, see guideline MSC30-C at https://www.securecoding.cert.org. If you are building industrial-strength applications that require random numbers, you should investigate for your platform the recommended function(s) to use.

# ## Summary

# ### Section 5.1 Introduction

+   - The best way to develop and maintain a large program is to divide (p. 190) it into several smaller pieces, each more manageable than the original program.

# ### Section 5.2 Modularizing Programs in C

+   - A function (p. 190) is invoked by a function call (p. 191). The function call specifies the function by name and provides information (as arguments) that the called function needs to perform its task.
+   - The purpose of *information hiding* is to give functions access only to the information they need to complete their tasks. This is a means of implementing the **principle of least privilege**, one of the most important principles of good software engineering.

# ### Section 5.3 Math Library Functions

+   - A function is normally invoked in a program by writing the function's name followed by a left parenthesis followed by the argument (or a comma-separated list of arguments) of the function followed by a right parenthesis.
+   - Each argument of a function may be a constant, a variable, or an expression.

# ### Section 5.4 Functions

+   - A local variable (p. 193) is known only in a function definition. Other functions are not allowed to know the names of a function's local variables, nor is any function allowed to know the implementation details of any other function.

# ### Section 5.5 Function Definitions

+   - The general format for a function definition is

```
    return-value-type function-name(parameter-list)
    {
        statements
    }
```

The *return-value-type* states the type of the value returned to the calling function. If a function does not return a value, the *return-value-type* is declared as void. The *function-name* is any valid identifier. The *parameter-list* (p. 195) is a comma-separated list containing the definitions of the variables that will be passed to the function. If a function does not receive any values, *parameter-list* is declared as void.