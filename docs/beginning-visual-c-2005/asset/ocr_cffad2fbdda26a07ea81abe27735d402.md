brush is a Windows object used to fill an area, in this case the client area of the window. The function GetStockObject() returns a generic type for all stock objects, so you need to cast it to type HBRUSH. In the preceding example it returns a handle to the standard gray brush, and the background color for our window is thus set to gray. This function can also be used to obtain other standard objects for a window, such as fonts for example. You could also set the hIcon and hCursor members to null, in which case Windows would provide the default icon and cursor. If you set hbrBackground to null, your program expects to paint the window background and messages are sent to your application whenever this becomes necessary.

The lpzMenuName member is set to the name of a resource defining the window menu, or to zero if there is no menu for the window. You will look into creating and using menu resources when you use the AppWizard.

The lpzClassName member of the struct stores the name that you supply to identify this particular class of window. You would usually use the name of the application for this. You need to keep track of this name because you will need it again when a window is created. This member would therefore be typically set with the statements:

```
static char szAppName[] = "OFWin";      // Define window class name
WindowClass.lpszClassName = szAppName;    // Set class name
```

The last member is hIconSm, which identifies a small icon associated with the window class. If you specify this as null, Windows searches for a small icon related to the hIcon member and use that.

In fact, the WNDCLASSEX structure replaces another structure, WNDCLASS that was used for the same purpose. The old structure did not include the cbSize member that stores the size of the structure in bytes or the hIconSm member.

# Creating a Program Window

After all the members of your WNDCLASSEX structure have been set to the values required, the next step is to tell Windows about it. You do this using the Windows API function RegisterClassEx(). Given that your structure is WindowClass, the statement to do this would be:

```
RegisterClassEx(&WindowClass);
```

Easy, isn’t it? The address of the struct is passed to the function, and Windows extracts and squirrels away all the values that you have set in the structure members. This process is called registering the window class. Just to remind you, the term class here is used in the sense of classification and is not the same as the idea of a class in C++, so don’t confuse the two. Each instance of the application must make sure that it registers the window classes that it needs. If you were using the obsolete WNDCLASS structure that I mentioned, you would have to use a different function here, RegisterClass().

After Windows knows the characteristics of the window that you want, and the function that is going to handle messages for it, you can go ahead and create it. You use the function CreateWindow() for this. The window class that you’ve already created determines the broad characteristics of a window, and further arguments to the function CreateWindow() add additional characteristics. Because an application may have several windows in general, the function CreateWindow() returns a handle to the window created that you can store to enable you to refer to that particular window later. There are many API calls that require you to specify the window handle as a parameter if you want to use them. You will look at a typical use of the CreateWindow() function at this point. This might be: