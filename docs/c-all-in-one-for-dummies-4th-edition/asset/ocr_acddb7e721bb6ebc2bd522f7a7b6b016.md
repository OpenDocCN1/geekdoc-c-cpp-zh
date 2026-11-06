```
```cpp
{
    std::cout << "Hello world!" << std::endl;
    return 0;
}
```
```

Then, after the preprocessor finishes its preprocessing, it creates a temporary fixed-up file (which has the lines from the `iostream` file inserted into the `MyProgram.cpp` file where the `#include` line had been) to look like this:

```
```cpp
int hello = 10;
int goodbye = 20;

int main()
{
    std::cout << "Hello world!" << std::endl;
    return 0;
}
```
```

In other words, the preprocessor replaced the `#include` line with the contents of that file. Now, the `iostream` file could have `#include` lines, and those lines would be replaced by the contents of the files they refer to. As you may imagine, what started out as a simple application with just a few lines could actually have hundreds of lines after the preprocessor gets through with it.

# ## Creating constants and macros with #define

The preprocessor also provides you with a lot of other directives besides `#include`. One of the more useful ones is the `#define` directive. Here's a sample `#define` line:

```
```cpp
#define MYSPECIALNUMBER 42
```
```

After the preprocessor sees this line, every time it encounters the word `MYSPECIALNUMBER`, it replaces it with the word `42` (that is, whatever sequence of letters, numbers, and other characters follow the definition). In this case, `#define` creates a kind of constant where the word is easier to understand than the value associated with it. But `#define` also lets you create what are called *macros*, which are a sort of script. This line defines the `oldmax()` macro:

```
```cpp
#define oldmax(x, y) ((x)>(y)?(x):(y))
```
```

Using Advanced C++ Features