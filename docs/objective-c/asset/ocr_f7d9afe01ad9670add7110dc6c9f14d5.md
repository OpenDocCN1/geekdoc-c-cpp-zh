For the purposes of this book, I will focus primarily on the #define, #ifdef, and other more commonly used preprocessor directives. The directives #pragma, #warning, #include, and #error are better served by viewing the GCC documentation.

# NOTE

One very common use of the #pragma directive is in adding IDE directives to your code for use by the IDE in labels. Apple uses this extensively in its own templates. In many of their templates, you’ll see the directive: #pragma mark Something. This will cause the IDE to display “Something” in the method name listing drop down list. Additionally, the special directive #pragma mark – causes a horizontal rule to be placed in the list.

# Defining constants

The first type of macro that I showed you in this chapter was used for the purposes of defining a constant that would then be reused in multiple places in your application. Indeed, this is perhaps one of the most common uses of macros. I myself use macros in this form for defining keys for accessing NSUserDefaults just like they showed in the previous example.

To define a constant, you use the preprocessor directive #define followed by the name of the constant you are defining the value for. After the name, separated by a space, you then provide the value you want the preprocessor to expand your macro to in your source code. The preprocessor expands the macro by using all of the remaining text in your line until it encounters the end of the line.

In cases where you want to make a macro such as this and spread its definition out over multiple lines, you can do this by entering a backslash and then pressing enter. This causes the compiler to consider the next line to be part of the current line for the purposes of evaluating this macro.

Listing 9.7 shows an example of several different constants being defined using the #define preprocessor directive.

# Listing 9.7

# Defining constants with #define

```
#define FOO 1
#define BAR @"this is bar"
#define BAZ @"THIS IS A VERY LONG STRING \
AND IT CONTINUES DOWN HERE \
AND HERE."
#define BOZ BAR
```