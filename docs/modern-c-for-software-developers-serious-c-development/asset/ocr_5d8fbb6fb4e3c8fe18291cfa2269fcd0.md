# Using Inline Variables

In C++17, the **inline** keyword permits us to define a global variable in a header file, even though this header file might be included in multiple implementation (.cpp) files.
The inclusion of the header file a multiple number of times does not create multiple definitions of the global variable.

Any inicialization of an inline variable will be performed by the first translation unit that includes the header file.

```
// some header file
class Foo {
public:
    // OK since C++17
    inline static std::string greet = "hello world";

// OK even if included in multiple implementation (.cpp) files
inline Foo foo;
```