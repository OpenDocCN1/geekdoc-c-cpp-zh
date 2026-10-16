# Listing 9.8 (continued)

```
#endif

    [pool drain];
    return 0;
}
```

Notice that the DEBUGGING macro is not actually being defined in this source file. In this particular case, I’m relying on the build settings to pass in that value when I do a debug build. If that value has been defined, then the application connects to the development server. If it is not, then it connects to the production server.

Figure 9.1 shows the build settings window and the parameter that you set in order to define values as part of your build settings.

The build setting that you use to define these preprocessor macros is the Preprocessor Macros setting. This particular setting takes a list of macro names and values separated by =. So, in other words, to define the preprocessor macro DEBUGGING, you would set this build setting to DEBUGGING=1. The given value here, 1, is more or less just setting it to any value (even 0 would be OK) so that the #ifdef statement returns true. If we used a #if with an expression, like #if DEBUGGING > 10 then we could have variable levels of debugging based on the compilation flag.

By setting this build setting on the debug build, the DEBUGGING macro will be set when the source code is compiled. When you switch to the Release build, which does not have this setting, then the normal, production code will be compiled and included.

# Using variables in macros

Although the syntactical capabilities of macros is much more primitive, macros are capable of taking parameters just like if when working with functions or methods. This enables you to create complex macros that actually do creative things with the contextual information available when the macro is being expanded.

For example, if you wanted to create a MAX macro to return the greater value of two parameters, you might create a macro such as Listing 9.9.

# Listing 9.9

# A macro for printing the value of a variable

```
#define MAX(X, Y): ((X) > (Y) ? (X) : (Y))
```