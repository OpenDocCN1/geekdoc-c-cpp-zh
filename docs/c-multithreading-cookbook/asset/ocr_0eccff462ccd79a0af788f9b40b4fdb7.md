# Introduction to C++ Concepts and Features

We implement WndProc later but for the declaration is enough. Now, we need an application entry point. Unlike a console application, the main function in Win32 applications has a slightly different prototype, as shown in the following code:

```
int WINAPI WinMain(HINSTANCE hThis, HINSTANCE hPrev, LPSTR szCmdLine,
               int iCmdShow);
```

After the return type (int), you will notice the WINAPI macro. It represents a calling convention.
WINAPI or stdcall a stack will call the clean. WinMain is the name and must have four parameters in a given order. The first parameter, hThis, is a handle to the current instance of the application. The second parameter, hPrev, is a handle to the previous instance of the application. If you refer to the MSDN documentation (http://microsoft.com/en-us/library/windows/ms33559%28-vs.85), you'll notice that the hPrev parameter is always NULL, so I guess that this has been left for compatibility with previous versions of window operating systems, as it can't have values in current trendy. The third parameter is szCmdLine or the command line for the application, the program name. The final parameter controls how the window is to be.

It can have one or more values combining bit values with the OR (()) operator (more information on MSDN).
We will use the UNREFERENCED_PARAMETER macro to tell the compiler that we will not use parameters so that we can do additional optimization. Using the following code:

```
UNREFERENCED_PARAMETER( hPrev);
UNREFERENCED_PARAMETER( szCmdLine );
```

Next, we need to instantiate the WNDCLASS window structure. This is an object with details of future windows, such as stack size, handle to current application instance, window style, window color, icon, and mouse pointer. The code to instantiate the WNDCLASS window structure is as follows:

```
WNDCLASS wndEx = { 0 };
```

The number of extras to allocate after instantiating the window class structure can be defined by using the following code:
The size, in bytes, of this structure can be defined by using the following code:

```
WndEx.cbClExtra = 0;
wndEx.cbSize = sizeof( wndEx );
```