
## Chapter 11

The application class is endowed with quite a number of data members defined in the base class, many of which correspond to variables used as arguments in Windows API functions. For example, the member `m_pszAppName` stores a pointer to a string that defines the name of the application. The member `m_nCmdShow` specifies how the application window is to be shown when the application starts up. You don't need to go into all the inherited data members now. You'll see how they are used as the need arises in developing application-specific code.

In deriving your own application class from `CWinApp`, you must override the virtual function `InitInstance()`. Your version is called by the version of `WinMain()` that's provided for you by MFC, and you'll include code in the function to create and display your application window. However, before you write `InitInstance()`, I should introduce you to a class in the MFC library that defines a window.

### The Window Class

Your MFC application needs a window as the interface to the user, referred to as a frame window. You derive a window class for the application from the MFC class `CFrameWnd`, which is designed specifically for this purpose. Because the `CFrameWnd` class provides everything for creating and managing a window for your application, all you need to add to the derived window class is a constructor. This enables you to specify a title bar for the window to suit the application context:

```cpp
class COurWnd: public CFrameWnd
{
public:
    // Constructor
    COurWnd()
    {
        Create(0, L"Our Dumb MFC Application");
    }
};
```

The `Create()` function that you call in the constructor is inherited from the base class. It creates the window and attaches it to the `COurWnd` object that is being created. Note that the `COurWnd` object is not the same thing as the window that is displayed by Windows — the class object and the physical window are distinct entities.

The first argument value for the `Create()` function, 0, specifies that you want to use the base class default attributes for the window — you'll recall that you needed to define window attributes in the previous example in this chapter that used the Windows API directly. The second argument specifies the window name that is used in the window title bar. You won't be surprised to learn that there are other parameters to the function `Create()`, but they all have default values which are quite satisfactory, so you can afford to ignore them here.

### Completing the Program

Having defined a window class for the application, you can write the `InitInstance()` function in our `COurApp` class:

```cpp
BOOL COurApp::InitInstance(void)
{
    // Construct a window object in the free store
    m_pMainWnd = new COurWnd;
    m_pMainWnd->ShowWindow(m_nCmdShow);      // ...and display it
    return TRUE;
}
```

This overrides the virtual function defined in the base class `CWinApp`, and as I said previously, it is called by the `WinMain()` function that's automatically supplied by the MFC library. The `InitInstance()` function constructs a main window object for the application in the free store by using the operator `new`. You store the address that is returned in the variable `m_pMainWnd`, which is an inherited member of your class `COurApp`. The effect of this is that the window object is owned by the application object. You don't even need to worry about freeing the memory for the object you have created — the supplied `WinMain()` function takes care of any cleanup necessary.

The only other item you need for a complete, albeit rather limited, program is to define an application object. An instance of our application class, `COurApp`, must exist before `WinMain()` is executed, so you must declare it at global scope with the statement:

```cpp
COurApp AnApplication;       // Define an application object
```

The reason that this object needs to exist at global scope is that it is the application, and the application needs to exist before it can start executing. The `WinMain()` function that is provided by MFC calls the `InitInstance()` function member of the application object to construct the window object and, thus, implicitly assumes the application object already exists.

### The Finished Product

Now that you've seen all the code, you can add it to the `Ex11_02.cpp` source file in the project. In a Windows program, the classes are usually defined in `.h` files, and the member functions that are not defined within the class definitions are defined in `.cpp` files. Your application is so short, though, that you may as well put it all in a single `.cpp` file. The merit of this is that you can view the whole lot together. The program code is structured as follows:

```cpp
// Ex11_02.cpp
// An elementary MFC program
#include <afxwin.h>                         // For the class library

// Application class definition
class COurApp:public CWinApp
{
public:
    virtual BOOL InitInstance();
};

// Window class definition
class COurWnd:public CFrameWnd
{
public:
    // Constructor
    COurWnd()
    {
        Create(0, L"Our Dumb MFC Application");
    }
};
```

### Using Windows Forms

A Windows form is an entity that represents a window of some kind. By a window I mean a window in its most general sense, being an area on the screen that can be a button, a dialog, a regular window, or any other kind of visible GUI component. A Windows form is encapsulated by a subclass of the `System::Windows::Forms::Form` class, but you don't need to worry about this much initially, because all the code to create a form is created automatically. To see just how easy it's going to be, create a basic window using Windows Forms that has a standard menu.

### Try It Out: A Windows Forms Application

Choose the CLR project type in the New Project dialog and select the Windows Forms Application as the template for the project. The New Project dialog window is shown in Figure 11-7.

![](img/2359b0c604600c58fba3539c738a356e_686_0.png)

Figure 11-7

Enter the project name as Ex11_03. When you click the OK button, the Application Wizard generates the code for the Windows Forms application and displays the design window containing the form as it is displayed by the application. This is shown in Figure 11-8.

![](img/2359b0c604600c58fba3539c738a356e_687_0.png)

Figure 11-8

You can now make changes to the form in the design pane graphically, and the changes are automatically reflected in the code that creates the form. For a start, you can drag the bottom corner of the form with the mouse cursor to increase the size of the form window. You can also change the text in the title bar — right-click in the client area of the form and select Properties from the context menu. This displays the Properties window that allows you to change the properties for the form. From the list of properties to the right of the design pane, select Text, and then enter the new title bar text in the adjacent column showing the property value — I entered A Simple Form Window. When you press the Enter key, the new text appears in the title bar of the form.

Just to see how easy it really is to add to the form window, display the Toolbox pane by selecting the tab on the right of the window if it is present, or by pressing Ctrl+Alt+X, or by selecting Toolbox from the View menu. Find the MenuStrip option in the list and drag it on to the form window in the Design tab pane. Right-click the `MenuStrip1` that appears below the form window and select Insert Standard Items from the pop-up. You'll then have the menu in the form window populated with the standard File, Edit, Tools, Help menus, each complete with its drop-down list of menu items. The result of this operation is shown in Figure 11-9.

If you build the project by pressing Ctrl+Shift+B and then execute it by pressing Ctrl+F5, you'll see the form window displayed complete with its menus. Naturally the menu items don't do anything because you haven't added any code to deal with the events that result from clicking on them, but the icons at the right end of the title bar work so you can close the application. You'll look into how to develop a Windows Forms application further, including handling events, later in the book.

![](img/2359b0c604600c58fba3539c738a356e_688_0.png)

Figure 11-9

### Summary

In this chapter you've seen three different ways of creating an elementary Windows application with Visual C++ 2005 and you should now have a feel for the essential differences between these three approaches. In the remaining chapters of the book, you'll be exploring in more depth how you develop applications using the MFC and using Windows Forms.
