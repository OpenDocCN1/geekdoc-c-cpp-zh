After 10 values have been input, the loop terminates, and line 32 displays the number of passes and failures. The `if` statement in lines 35–37 determines whether more than eight students passed the exam and, if so, outputs the message "Bonus to instructor!" Figure 3.3 shows the input and output from two sample executions. During the first, the condition at line 35 is true—more than eight students passed the exam, so the program outputs a message to give the instructor a bonus.

# ### 3.10.7 Preventing Narrowing Conversions with Braced Initialization

Consider the braced initialization in line 10 of Fig. 3.3:

```
    int studentCounter{1};
```

which also can be written as

```
    int studentCounter = 1;
```

For fundamental-type variables, braced initializers prevent **narrowing conversions** that could result in data loss. For example, the following declaration attempts to assign the `double` value `12.6` to the `int` variable `x`:

```
    int x = 12.6;
```

Here, C++ converts the `double` value to an `int` by truncating the floating-point part (`.6`), so this declaration assigns `12` to `x`. The narrowing conversion loses data. Compilers typically issue a warning for this but still compile the code.

However, using braced initialization, as in

```
    int x{12.6};
```

yields a **compilation error**, helping you avoid a potentially subtle logic error. You'll still get a **compilation error** if you specify a whole-number `double` value, like `12.0`. The initializer's type (`double`), not its value (`12.0`), determines whether a compilation error occurs.

![](bbox=[0.833, 0.559, 0.858, 0.579])

The C++ standard document does not specify error-message wording. For the preceding declaration, Visual Studio gives the error

```
    conversion from 'double' to 'int' requires a narrowing conversion
```

GNU C++ gives the error

```
    error: narrowing conversion of '1.26e+1' from
    'double' to 'int' [-Wnarrowing]
```

and the clang++ compiler gives the error

```
    error: type 'double' cannot be narrowed to 'int' in initializer list
    [-Wc++11-narrowing]
```

followed by more explanation

```
    warning: implicit conversion from 'double' to 'int' changes value
    from 12.6 to 12 [-Wliteral-conversion]
```

We'll discuss additional braced-initializer features in later chapters.