# USING THE PREPROCESSOR

In Chapter 13, you saw how you can use the C preprocessor (cpp) to create separators that show up in the Jump Bar and aid code navigation. If you're unfamiliar with the preprocessor, it may surprise you to know that it's far more powerful than that. It has a lot more to offer than the simple pragma mark directive.

TIP: To learn more about what the C preprocessor can do for you, visit http://xcodebook.com/cpp.

# MACROS

One of the simplest ways to use the preprocessor is to define macros. Since the preprocessor does as its name suggests—processes the text prior to compilation—macros are automatically expanded for the compiler. This means you can use the #define command to create a kind of “lazy man’s constant” or to compress a set of nested method calls down to a simple stand-in symbol.

# WHERE TO PUT THEM

It’s usually preferable to define macros in a header file so they can be imported elsewhere without needing to repeat them. Many developers use a global header file for this. The default .pch file found under your project’s Supporting Files group is included everywhere and is a great place to keep global macros.

# DEFINING A MACRO

A macro is defined using the #define directive and a macro name (such as PlaceholderString or TRUNCATED_PI), followed by the expanded text for the macro. For example, the following defines a macro:

```
#define TRUNCATED_PI 3.14
```

Any time the preprocessor encounters TRUNCATED_PI in source files, the value will be “expanded to” (or replaced by) 3.14.

In Cocoa applications, it’s commonplace to use uniform type identifiers (such as com.mycompany.TestApp.testappdocument) to identify data types such as documents, pasteboard drag types, and more. As with constants, the benefit of using a macro is to cut down on the number of opportunities you might mis-type a string constant (which the compiler cannot verify for you). Since a macro, like a symbol,

![](bbox=[0.75, 0.14, 1.0, 0.38])