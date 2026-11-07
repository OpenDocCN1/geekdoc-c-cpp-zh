C++ has altered the rules for constant types to make life easier for you. Suppose, for example, that you have a set of constants that you'd like to place in a header file and that you use this header file in several files in the same program. After the preprocessor includes the header file contents in each source file, each source file will contain definitions like this:

```
```
const int fingers = 10;
const char * warning = "Wak!";
```
```

If global const declarations had external linkage as regular variables do, this would be an error because of the one definition rule. That is, only one file can contain the preceding declaration, and the other files have to provide reference declarations using the extern keyword. Moreover, only the declarations without the extern keyword would be able to initialize values:

```
```
// extern would be required if const had external linkage
extern const int fingers;        // can't be initialized
extern const char * warning;
```
```

So you would need one set of definitions for one file and a different set of declarations for the other files. Instead, because externally defined const data has internal linkage, you can use the same declarations in all files.

Internal linkage also means that each file gets its own set of constants rather than sharing them. Each definition is private to the file that contains it. This is why it's a good idea to put constant definitions in a header file. That way, as long as you include the same header file in two source code files, they receive the same set of constants.

If, for some reason, you want to make a constant have external linkage, you can use the extern keyword to override the default internal linkage:

```
```
extern const int states = 50;    // definition with external linkage
```
```

You then must use the extern keyword to declare the constant in all files that use the constant. This differs from regular external variables, in which you don't have to use the keyword extern when you define a variable, but you use extern in other files using that variable. Keep in mind, however, now that a single const is being shared among files, only one file can use initialization.

When you declare a const within a function or block, it has block scope, which means the constant is usable only when the program is executing code within the block. This means that you can create constants within a function or block and not have to worry about the names conflicting with constants defined elsewhere.

# ## Functions and Linkage

Like variables, functions have linkage properties, although the selection is more limited than for variables. C++, like C, does not allow you to define one function inside another, so all functions automatically have static storage duration, meaning they are all present as long as the program is running. By default, functions have external linkage, meaning they can be shared across files. You can, in fact, use the keyword extern in a function prototype