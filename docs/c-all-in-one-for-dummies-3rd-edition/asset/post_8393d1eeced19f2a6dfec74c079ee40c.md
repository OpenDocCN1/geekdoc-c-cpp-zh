
anything but numbers because it called our EnterOnlyNumbers() routine. And finally, we entered a password, and you can see that the computer displayed asterisks when we pressed each key. Then the application kept the secret password and wrote it on the screen anyway.

## Understanding Preprocessor Directives

When you compile an application, the first thing the compiler does is run your code through something called a preprocessor. The preprocessor simply looks for certain statements in your code that start with the # symbol. You have already seen one such statement in every one of your applications: #include. These preprocessor statements are known as directives because they tell the preprocessor to do something; they direct it.

Think of the preprocessor as just a machine that transforms your code into a temporary, fixed-up version that's all ready to be compiled. For example, take a look at this preprocessor directive:

```cpp
#include <iostream>
```

If the preprocessor sees this line, it inserts the entire text from the file called iostream (yes, that's a filename; it has no extension) into the fixed-up version of the source code.

Suppose that the file called iostream looks like this:

```cpp
int hello = 10;
int goodbye = 20;
```

Just two lines are all that's in it. (Of course, the real iostream file is much more sophisticated.) And suppose that your own source file, MyProgram.cpp, has this in it (as found in the Preprocessor example):

```cpp
#include <iostream>
int main()
{
    cout << "Hello" << endl;
}
```

Then, after the preprocessor finishes its preprocessing, it creates a temporary fixed-up file (which has the lines from the iostream file inserted into the MyProgram.cpp file where the #include line had been) to look like this:

```cpp
int hello = 10;
int goodbye = 20;
int main()
{
    cout << "Hello" << endl;
}
```

In other words, the preprocessor replaced the `#include` line with the contents of that file. Now, the source file itself could have `#include` lines, and those lines would be replaced by the contents of the files they refer to. As you may imagine, what started out as a simple application with just a few lines could actually have hundreds of lines after the preprocessor gets through with it. (In fact, that's a conservative estimate: We ran the default `Code::Blocks` code through the preprocessor, and it contained 25,613 lines! You can see the output in `Main.txt`, which is included in the `Preprocessor` folder of the downloadable source code. Many of those are blank lines, for various reasons, but nevertheless, it's a very big file!)

![](img/6ba99460b0feb3585671a4612ff5fabb_241_0.png)

Don't worry: Your original source code file doesn't change when the preprocessor goes at it. The preprocessor builds a *temporary* file, and *that's* what the compiler compiles. Also, you don't have to run the preprocessor manually; the compiler runs it for you.

![](img/6ba99460b0feb3585671a4612ff5fabb_241_1.png)

Although you don't have to run the preprocessor yourself, you can, if you're curious to see what its output looks like. The `Code::Blocks` compiler actually calls on `gcc.exe` to perform the compilation process. However, `gcc` is just a small application that launches the compiler. But before it launches the compiler, it runs the preprocessor. The preprocessor command is `cpp` (for C preprocessor). If your paths are set up correctly and you want to try it out, just type `cpp`, the name of your source file, the redirection symbol (`>>`), and the name of an output file at the command line, such as `cpp main.cpp >> main.txt`. In most cases, you can set up the path correctly by typing the following line at the command line and pressing Enter:

```
path=C:\CodeBlocks\MinGW\bin;%path%
```

Prepare yourself for a *lot* of lines. But seeing the output and how your code looks when it's ready to be pushed through the compiler is interesting.

The preprocessor also provides you with a lot of other directives besides `#include`. One of the more useful ones is the `#define` directive. Here's a sample `#define` line:

```cpp
#define MYSPECIALNUMBER 42
```

After the preprocessor sees this line, every time it encounters the word `MYSPECIALNUMBER`, it replaces it with the word *42* (that is, whatever sequence of letters, numbers, and other characters follow the definition). But `#define` also lets you create what are called *macros*. Take a look at this line:

```cpp
#define oldmax(x, y) ((x) > (y) ? (x) : (y))
```

After the preprocessor learns this line, every time it sees the word `oldmax` followed by two things in parentheses separated by a comma, it replaces it with the form `((x) > (y) ? (x) : (y))`, substituting the thing before the comma for *x* and the thing after the comma for *y*. For example, if you then have this line

whichever compiler you use. (In Code::Blocks, you choose Project>Build Options. In the Project Build Options dialog box that opens, click the Compiler Settings tab, followed by the #defines subtab, as shown in Figure 9-1. You type your compiler options as shown in the figure.) To define the DEBUG symbol through a command-line option, you add the following line to your command:

```
-D DEBUG
```

either in the gcc command or in the Project Build Options dialog box in Code::Blocks. Then, when you include this compiler option, the DEBUG symbol is defined throughout your application, just as though you had included a #define DEBUG line at the beginning.

![](img/6ba99460b0feb3585671a4612ff5fabb_243_0.png)

**Figure 9-1:** Provide the compiler options you want to use to change the application output.

Now, when the preprocessor starts going through your application and gets to the `#ifdef DEBUG` line, it checks whether the DEBUG symbol is defined. If the symbol is defined, it spits out into its fixed-up file the lines that follow, up until the `#else` line. Then it skips any lines that follow that, up until the `#endif` line.

But if the DEBUG symbol is *not* defined, the preprocessor skips over the lines up until the `#else`, and spits out the lines that follow, up until the `#endif`.

Thus, for the example we gave earlier in this section, if DEBUG is defined, the block of code starting with `#ifdef DEBUG` through the `#endif` is replaced by the stuff in the first half of the block:

```cpp
cout << "The value of i is " << i << endl;
```

But if DEBUG is not defined, it is replaced by the stuff following the `#else` line:

```cpp
cout << s << endl;
```

![](img/6ba99460b0feb3585671a4612ff5fabb_244_0.png)

When the preprocessor goes through your file, it is only creating a new source code file to be used by the compiler. That means these `#ifdef` lines affect your application only when the compiler fires off the preprocessor. When your application is compiled and you run it, these `#ifdef` lines are nowhere to be found. So remember that these `#ifdef` lines do not affect how your application runs — only how it compiles.

![](img/6ba99460b0feb3585671a4612ff5fabb_244_1.png)

Using preprocessor directives, you can have two different versions of your application. In the example we gave, we're gearing up for two versions: a debug version and a release version. To tell the compiler which version to build, we then modify the command-line options by either removing or adding the -D DEBUG line.

![](img/6ba99460b0feb3585671a4612ff5fabb_244_2.png)

The -D option works either with or without a space after the D. Thus, you can either use -DDEBUG or -D DEBUG. They both do the same thing.

The Preprocessor2 example, shown in Listing 9-3, demonstrates all the topics we cover in this section.

### Listing 9-3: Using Many Different Preprocessor Directives

```cpp
#include <iostream>

using namespace std;

#define UNIVAC
const int total = 200;
const string compname = "UNIVAC";
#if defined(HAL2000)
const int total = 300;
const string compname = "HAL2000";
#else
const int total = 400;
const string compname = "My Computer";
#endif
// This is outdated, but you might
// see it on occasion. Don't write
// code yourself that does this!
#define oldmax(x, y) ((x)>(y) ? (x) : (y))
#define MYSPECIALNUMBER 42

int main()
{
    cout << "Welcome to " << compname << endl;
    cout << "Total is: " << endl;
    cout << total << endl;

    // Try out the outdated things.
    cout << "*** max ***" << endl;
    cout << oldmax(5, 10) << endl;
    cout << oldmax(20, 15) << endl;
    cout << MYSPECIALNUMBER << endl;
}
```
