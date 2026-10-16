
For the purposes of this book, I will focus primarily on the #define, #ifdef, and other more commonly used preprocessor directives. The directives #pragma, #warning, #include, and #error are better served by viewing the GCC documentation.

## NOTE

One very common use of the #pragma directive is in adding IDE directives to your code for use by the IDE in labels. Apple uses this extensively in its own templates. In many of their templates, you’ll see the directive: #pragma mark Something. This will cause the IDE to display “Something” in the method name listing drop down list. Additionally, the special directive #pragma mark – causes a horizontal rule to be placed in the list.

## Defining constants

The first type of macro that I showed you in this chapter was used for the purposes of defining a constant that would then be reused in multiple places in your application. Indeed, this is perhaps one of the most common uses of macros. I myself use macros in this form for defining keys for accessing NSUserDefaults just like they showed in the previous example.

To define a constant, you use the preprocessor directive #define followed by the name of the constant you are defining the value for. After the name, separated by a space, you then provide the value you want the preprocessor to expand your macro to in your source code. The preprocessor expands the macro by using all of the remaining text in your line until it encounters the end of the line.

In cases where you want to make a macro such as this and spread its definition out over multiple lines, you can do this by entering a backslash and then pressing enter. This causes the compiler to consider the next line to be part of the current line for the purposes of evaluating this macro.

### Listing 9.7

### Defining constants with #define

```
#define FOO 1
#define BAR @"this is bar"
#define BAZ @"THIS IS A VERY LONG STRING \
AND IT CONTINUES DOWN HERE \
AND HERE."
#define BOZ BAR
```

An unspoken rule is to always name your macros using all capital letters. Doing this helps to distinguish macros in your source code from normal statements and makes your code easier to read. In the previous section, I mentioned that you should not use the double underscores for your own macro names. Additionally, you should not use underscores at the beginning or end of your macro names either because this is reserved for the compiler. It's perfectly safe to use underscores inside your macro names, and in fact, this is again another unspoken standard: separating multiple words in your macro names by using underscores instead of spaces since spaces are not legal anywhere in a macro name. Macro names must also begin with an alphabetic letter. Numbers are not allowed. You are free to use numbers after the first letter of the macro name but they cannot be used for the first letter.

As you found out in the previous section, macros can refer to other macros within their definition. In these cases, your macro will first be expanded to whatever you have defined, and then any macros inside of your macro definition will be expanded in place from there. For example, the macro BOZ above will ultimately expand to BAR, and then BAR will be expanded to @"this is bar".

The exception to this rule is that macros are not recursive. Meaning, you cannot refer to the macro that you are defining in its definition. For example, the macro #define FOO FOO won't work.

## Passing constants by compilation

I mention earlier in this chapter how you can define macros as part of your build settings. Listing 9.8 shows an example of an application that needs to be compiled to connect to a test server when it is being debugged and compiled to connect to the production server when it is not being debugged.

### Listing 9.8

### Conditional compilation based on build settings

```
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    NetworkConnection *conn = [[NetworkConnection alloc] init];
#ifdef DEBUGGING
    [conn connectToServer:@"http://develop.nowhere.com"];
#else
    [conn connectToServer:@"http://production.nowhere.com"];
#endif

    [pool drain];
    return 0;
}
```

Notice that the DEBUGGING macro is not actually being defined in this source file. In this particular case, I’m relying on the build settings to pass in that value when I do a debug build. If that value has been defined, then the application connects to the development server. If it is not, then it connects to the production server.

Figure 9.1 shows the build settings window and the parameter that you set in order to define values as part of your build settings.

The build setting that you use to define these preprocessor macros is the Preprocessor Macros setting. This particular setting takes a list of macro names and values separated by =. So, in other words, to define the preprocessor macro DEBUGGING, you would set this build setting to DEBUGGING=1. The given value here, 1, is more or less just setting it to any value (even 0 would be OK) so that the #ifdef statement returns true. If we used a #if with an expression, like #if DEBUGGING > 10 then we could have variable levels of debugging based on the compilation flag.

By setting this build setting on the debug build, the DEBUGGING macro will be set when the source code is compiled. When you switch to the Release build, which does not have this setting, then the normal, production code will be compiled and included.

## Using variables in macros

Although the syntactical capabilities of macros is much more primitive, macros are capable of taking parameters just like if when working with functions or methods. This enables you to create complex macros that actually do creative things with the contextual information available when the macro is being expanded.

For example, if you wanted to create a MAX macro to return the greater value of two parameters, you might create a macro such as Listing 9.9.

### Listing 9.9

### A macro for printing the value of a variable

```
#define MAX(X, Y): ((X) > (Y) ? (X) : (Y))
```

### Figure 9.1

The build settings window.

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_252_0.png)

In this example, the MAX macro takes two arguments, X and Y. It then compares these two arguments by using the ternary operator. If X is greater than Y, it returns X, alternatively, if Y is greater than X, it returns Y.

When using parameters with a macro the parameters are specified inside parentheses just as if you were defining parameters for procedures. There are, however, a few subtle differences.

First, you do not need to provide a data type for the parameters. This code will not be compiled. Instead, the macro will be expanded where it is used in the parameters will be inserted directly into the expanded macro code. Therefore, variable types are not necessary here.

Secondly, the opening parenthesis of the parameter list must come directly after the name of the macro. Notice when we have been defining other macros, that the value that we are defining for the macro is separated from the macro name by a space. Therefore, if you were to put a space between the macro name and the opening parenthesis of the parameter list, the preprocessor would assume that the parameter list is the beginning of the macro value instead of part of the macro name.

Another subtle difference between procedures and macros with arguments is in the handling of the values inside the body of the macro value. Notice in the example above that there are a lot of extra parentheses being used in the body of the macro. Again, this has to do with the fact that the macro will be expanded in the code and that the values will be expanded inside the macro in the code. To illustrate this point, consider the expansion of the code NSLog (@"Max Value: %ld", MAX ( x & 20, 10 ) ); . Without the additional parentheses, this might expand to NSLog (@"Max Value: %ld", (x & 20 > 10 ? x & 20 : 10 ) ); . In this case, order of operations dictates that the greater than comparison has higher precedence than the bitwise-AND operation and therefore would be performed on the 20 and the 10 rather than on x & 20 and the 10. By including the extra parentheses inside the body of the macro, you ensure that the order of operations is performed in exactly the way that you expect them to be. In other words, this code would actually expand to NSLog (@"Max Value: %ld", ( (x & 20) > (10) ? (x & 20) : (10) ) ); .

## Using stringification

One of the macro tricks that I like to use in my own code is in logging values of particular variables as my application is running. Doing this can be useful because I can see what the state of my application is without necessarily stopping it in the debugger and looking at particular values one at a time.

To do this, I have to create a macro that takes a variable as a parameter. Because I might use this macro in multiple locations on different variables I also need to get the variable name and print it alongside the value of that variable. To do this, I use a special macro capability called stringification.

Stringification takes whatever code is passed to it and converts it to a C string by enclosing it in quotes. So, for example, if given 'x + 10' as a parameter, it will turn it into " 'x + 10' ". This makes it ideal for solving this kind of problem.

Listing 9.10 shows the macro as I would define it.
