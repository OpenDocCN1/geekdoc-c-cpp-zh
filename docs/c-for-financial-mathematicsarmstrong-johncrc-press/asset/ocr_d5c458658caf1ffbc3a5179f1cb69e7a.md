+   Try to remember to use **static** for functions and variables that aren't in the header file.

+   For every **.h** file there should be one **.cpp** file that defines everything the **.h** file declares.

+   In addition you should have one header called **stdafx.h** that includes the standard libraries you're using. It saves typing to put most of your **#include** statements into one file. It is also possible to use special compiler settings to "pre-compile" this shared header file, which allows you to compile your code more quickly. By convention on Windows this file is called **stdafx.h** and we have decided to use the same convention on all operating systems for simplicity.

+   You should have a **main.cpp** file for testing.

+   The first line of the **.cpp** files should **#include** the corresponding **.h** file.

+   Don't write **using namespace** in a header file. You don't want to force the user of your library to use specific namespaces, it should be their choice. If you were to break this rule and use a namespace in a header file all users of that library will have to use that namespace. This would defeat the entire purpose of the namespace.