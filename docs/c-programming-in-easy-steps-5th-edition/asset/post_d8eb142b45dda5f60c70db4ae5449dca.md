
values and the variable name have been substituted in the output statements

```cpp
using namespace std;

int main()
{
    string longgerline = "They carried a net";
    longgerline += "and their hearts were set";

    cout << "In a bowl to sea went wise men three" << endl;
    cout << "On a brilliant night in June" << endl;
    cout << longgerline << endl;
    cout << "On fishing up the moon." << endl;

    return 0;
}
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_164_0.png)

Notice that the second statement contains multiple spaces, which will be removed by the stringizing operator.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_164_1.png)

The merging operator is alternatively known as the “token-pasting” operator, as it pastes two “tokens” together.

## Debugging assertions

It is sometimes helpful to use preprocessor directives to assist with debugging program code – by defining an **ASSERT** macro function to evaluate a specified condition for a Boolean value.

The condition to be evaluated will be passed from the caller as the **ASSERT** function argument. The function can then execute appropriate statements according to the result of the evaluation. Multiple statements can be included in the macro function definition by adding a backslash `\` at the end of each line, allowing the definition to continue on the next line.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_165_0.png)

You can comment out sections of code when debugging using C-style `/* */` comment operators.

Numerous statements calling the **ASSERT** function can be added to the program code to monitor a condition as the program proceeds. For example, to check the value of a variable as it changes.

Usefully, an **ASSERT** function can be controlled by a **DEBUG** macro. This allows debugging to be easily turned on and off simply by changing the value of the **DEBUG** control macro:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_165_1.png)

- 1. Start a new program by defining a **DEBUG** macro with an “on” value of one – to control an **ASSERT** function.

```cpp
#define DEBUG 1
```

- 2. Next, add a macro `if`-`elif` statement block to define the **ASSERT** function according to the control value.

```cpp
#if ( DEBUG == 1 )
        // Definition for “on” goes here.
#elif ( DEBUG == 0 )
        // Definition for “off” goes here.
#endif
```

- 3. In the top part of the **ASSERT** function statement block, insert a definition for when the debugging control is set to “on” – to output failure details from predefined macros.

```cpp
#define ASSERT( expr ) \
cout << #expr << "..." << num; \
if ( expr != true ) \
{ \
    cout << " Fails in file:" << __FILE__; \
    cout << " at line:" << __LINE__ << endl; \
} \
else cout << " Succeeds" << endl;
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_165_2.png)

Do not place a backslash continuation character on the last line of the definition, and remember to use the `#` stringizing operator to output the expression as a string.

- 4. In the bottom part of the **ASSERT** function statement block, insert a definition for when the debugging control is set to “off” – to simply output the current variable value.

```cpp
#define ASSERT( result ) \
cout << "Number is " << num << endl;
```

- 5. After the macro definitions, specify the library classes to include, and a namespace prefix to use.

```cpp
#include <iostream>
using namespace std;
```

- 6. Add a `main` function containing a final return statement.

```cpp
int main()
{
    // Program code goes here.
    return 0;
}
```

- 7. At the start of the `main` function block, declare and initialize an integer variable, then call the macro ASSERT function to check its value as it gets incremented.

```cpp
int num = 9;    ASSERT( num < 10 );
num++;          ASSERT( num < 10 );
```

- 8. Save, compile, and run the program to see the output.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_166_0.png)

- 9. Edit the program to turn debugging off by changing the control value, then recompile and re-run the program.

```cpp
#define DEBUG 0
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_166_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_166_2.png)

Predefined macro names are prefixed by a double underscore and suffixed by a double underscore.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_166_3.png)

Additionally, the current date and time can be output from the `__DATE__` and `__TIME__` predefined macros.

## Summary

- The C++ compiler’s **-save-temps** option saves the temporary files created during the compilation process for examination.
- Compilation first writes program code and included library code into a single **.ii** text file, which is then translated into low-level Assembly language as a **.s** text file.
- Assembly language **.s** files are translated to machine code as **.o** object files, which are used to create the executable program.
- A **#define** directive defines a macro name and a value that the preprocessor should substitute for that name in program code.
- The preprocessor can be made to perform conditional tests using **#ifdef**, **#ifndef**, and **#endif** directives.
- Preprocessor alternatives can be provided using **#if**, **#else**, and **#elif** directives, and a definition can be removed using **#undef**.
- Each header file should use inclusion guards to prevent accidental multiple definition of the same class or function.
- The macro name of an inclusion guard is an uppercase version of the file name, but with the dot replaced by an underscore.
- A **#define** directive may also define a macro function that will be substituted in program code in place of the macro name.
- Inline functions are usually preferable to macro functions because, unlike macro functions, they perform type-checking.
- The preprocessor **#** stringizing operator converts a series of characters passed as a macro argument into a string value.
- Two terms can be combined into a single term by the preprocessor **##** merging operator.
- An **ASSERT** macro function is useful for debugging code, and may be controlled by a **DEBUG** macro to easily turn debugging on or off.

## Starting a Universal project

Windows 10 introduced the **Universal Windows Platform (UWP)** that enables you to create a single application that will run on any modern Windows-based device – phone, tablet, or PC.

The interface layout of a UWP application uses the **eXtensible Application Markup Language (XAML)** to specify components.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_169_0.png)

The example in this chapter is for Visual Studio 2015 on Windows 10 – it won't work with earlier versions.

In order to develop apps for the UWP, you should be running the latest version of Windows 10, and your Visual Studio IDE must include the **Universal Windows App Development Tools**:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_169_1.png)

Universal

- 1. Open **Control Panel, Programs and Features**, then right-click on the Visual Studio item and select **Change** – to launch the Visual Studio installer.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_169_2.png)

- 2. Select all options in the **Universal Windows App Development Tools** category, then click the **Next** button – to download and install the tools.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_169_3.png)

- 3. After installation of the tools, open the Visual Studio IDE.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_169_4.png)

A UWP application is also known as a “UWA” – Universal Windows Application.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_170_0.png)

Depending upon your choices when you installed Visual Studio, you may see the options checked when the installer launches, to indicate you already have the Universal Windows App Development Tools.

- 4. Next, select **File**, **New**, **Project** and create a new **Blank App (Universal Windows)** project called “Universal”.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_170_1.png)

- 5. When asked to select the target and minimal platform versions, simply click **OK** to accept the default options.

- 6. After Visual Studio creates the new project, select **View**, **Solution Explorer** to examine the generated files:

  - A set of logo images in an **Assets** folder.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_170_2.png)

  - Internal XAML and C++ **App** files.
  - XAML and C++ files for the **MainPage** – here is where you will create interface components and functional code.
  - Other miscellaneous **Package** files.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_170_3.png)

In Windows 10, you should ensure that the **Developer Mode** option is enabled in **Settings**, **Update & Security**, **For developers**.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_170_4.png)

These files are essential to all UWP apps using C++, and exist in every project Visual Studio creates to target the Universal Windows Platform with C++.
