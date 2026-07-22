![](image_rsrc1MJ.jpg)

Windows Programming with C and C++

Table of contents

[Chapter 1](#part0003.xhtml)

[Introduction to Windows Programming](#part0003.xhtml_a1KY)

[Chapter 2](#part0004.xhtml)

[Basic Windows Concepts](#part0004.xhtml_a1KN)

[Chapter 3](#part0005.xhtml)

[User Interface Basics](#part0005.xhtml_a1KM)

[Chapter 4](#part0006.xhtml)

[Graphics and Drawing](#part0006.xhtml_a1KJ)

[Chapter 5](#part0007.xhtml)

[File and Data Management](#part0007.xhtml_a1KP)

[Chapter 6](#part0008.xhtml)

[Multithreading and Concurrency](#part0008.xhtml_a1M3)

[Chapter 7](#part0009.xhtml)

[Network Programming](#part0009.xhtml_a1M0)

[Chapter 8](#part0010.xhtml)

[Advanced Windows Programming](#part0010.xhtml_a1KW)

[Chapter 9](#part0011.xhtml)

[Debugging and Testing](#part0011.xhtml_a1KX)

[Chapter 10](#part0012.xhtml)

[Deployment and Distribution](#part0012.xhtml_a1KH)

# Chapter 1

## Introduction to Windows Programming

Windows Operating System

The Windows operating system is a complicated system made to do many different jobs effectively. It offers a visual way to interact with the system, allows running multiple tasks at the same time, and works with many different hardware and software parts. At its core, Windows is based on processes and threads. Each application runs as its own process, and within each process, several threads can work at the same time.

Key Components

Kernel: The main part of the operating system that handles important tasks like managing memory, scheduling processes and threads, and allowing the software to work with hardware.

User Mode: This is where apps run, including parts like Win32, . NET, and other tools that apps use.

Hardware Abstraction Layer (HAL): It creates a standard way for the operating system (OS) to communicate with the hardware. This allows Windows to work on different types of hardware without needing any changes.

File System: In charge of arranging and keeping data on storage devices. NTFS (New Technology File System) is the main way Windows organizes and stores files.

Device Drivers: Programs that help the operating system talk to hardware. Every piece of equipment has its own software that helps it work.

Knowing these parts is important for good Windows programming. It helps developers work better with the system and make the most of what it can do.

Differences Between C and C++ in Windows Programming

C is a programming language that focuses on procedures and allows direct access to memory and hardware, which makes it good for working on systems. It is the language used to create the Windows API, which is the main set of tools for working with the operating system.

C++ is a version of C that adds features for working with objects. It helps create code that is easier to organize and use again, which is helpful for complicated Windows programs.

Key Differences in Windows Programming

Object-Oriented Programming (OOP):

C++ allows you to use important programming ideas like keeping data safe (encapsulation), sharing features between classes (inheritance), and using the same function in different ways (polymorphism). These features help you organize big programs and build applications in parts.

C uses a style of programming called procedural programming, which can be easier to understand. However, it can become messy when the program gets bigger.

Standard Library:

C++ has something called the Standard Template Library (STL), which gives you helpful tools for organizing data and solving problems. This can make many usual programming jobs easier.

C has a smaller set of built-in tools, which often means you have to create more data structures and algorithms by yourself.

RAII (Resource Acquisition Is Initialization):

C++ uses RAII to handle resources, automatically freeing them when they are no longer needed. This helps stop wasting resources.

In C, you have to manage resources yourself. This means you have to clearly set aside memory and free it up when you're done. If you don't do this carefully, you might end up with memory leaks.

Choosing Between C and C++

Choosing between C and C++ for Windows programming usually depends on what the project needs. C is often used for parts of a system that need to be fast and work closely with hardware. C++ is usually better for developing applications where it’s important to be able to easily update and reuse the code.

Setting Up Your Development Environment

Choosing an IDE

A good Integrated Development Environment (IDE) can really help you work better by giving you tools to write, fix, and organize your code. The most popular program for Windows coding with C and C++ is Microsoft Visual Studio.

Installing Visual Studio

Download: Go to the Visual Studio website and get the installer.

To install, run the installer and pick the "Desktop development with C++" option. This will set up the tools and software needed for developing on Windows.

Settings: After you install Visual Studio, adjust it to your liking by choosing the theme, font size, and other settings.

Understanding the Development Environment

Solution Explorer: Organizes your projects and files.

Editor: A place where you create and change your code.

Output Window: Shows messages about building and running programs.

Debugger: Helps find and fix problems in your code.

Setting Up a New Project

Make a New Project: Click on "File," then "New," and choose "Project. " Pick "Windows Desktop Application" for a standard GUI app.

Set up your project by giving it a name, choosing a location, and adjusting other settings like the target system type (x86 or x64).

Project Templates: Visual Studio offers ready-made setups for various kinds of projects, like console apps, desktop apps, and DLLs. Pick the one that works best for you.

Building and Running Your Project

Make Code: Use the editor to write the code for your app.

To create your program, click on "Build" and then select "Build Solution" to turn your code into a working program.

To run your application, click on "Debug" and then select "Start Without Debugging. "

Understanding the Windows API

What is the Windows API?

The Windows API is a set of functions and tools that Microsoft gives to help people use the Windows operating system. It helps developers create windows, handle what users type, manage memory, and connect to hardware.

Key Components of the Windows API

Kernel32dll: Has tools for managing memory, handling processes and threads, and reading/writing files.

User32dll: It helps create and manage windows, deal with messages, and handle user input.

Gdi32dll: Holds tools for graphic tasks, like writing text, drawing shapes, and displaying images.

Advapi32dll: Offers tools for advanced tasks like managing security and the system registry.

Using the Windows API in C and C++

To use the Windows API in your programs, add the right header files and connect to the needed libraries. The most frequently used headers are windows. h for basic functions and winuser. h for functions related to the user interface.

Creating a Simple Windows Application

Here is an example of an easy Windows program made using C:

#include <windows.h>

LRESULT CALLBACK WindowProc(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam) {

switch (uMsg) {

case WM_DESTROY:

PostQuitMessage(0);

return 0;

default:

return DefWindowProc(hwnd, uMsg, wParam, lParam);

}

}

int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow) {

const char CLASS_NAME[] = "Sample Window Class";

WNDCLASS wc = {};

wc.lpfnWndProc = WindowProc;

wc.hInstance = hInstance;

wc.lpszClassName = CLASS_NAME;

RegisterClass(&wc);

HWND hwnd = CreateWindowEx(

0,

CLASS_NAME,

"Learn to Program Windows",

WS_OVERLAPPEDWINDOW,

CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT,

NULL,

NULL,

hInstance,

NULL

);

if (hwnd == NULL) {

return 0;

}

ShowWindow(hwnd, nCmdShow);

MSG msg = {};

while (GetMessage(&msg, NULL, 0, 0)) {

TranslateMessage(&msg);

DispatchMessage(&msg);

}

return 0;

}

Explanation of the Code

Adding Headers: The windows. h file is included to use Windows API functions.

Window Procedure: The WindowProc function handles messages sent to the window. In this example, it responds to the WM_DESTROY message to close the app.

WinMain Function: The starting point for a Windows app. It sets up a window type, makes a window, and starts the message loop.

To register a window class, you use something called the WNDCLASS structure. This tells the system about the window class, including how the window should behave, what program it's part of, and what the class is named.

Making a Window: The CreateWindowEx function makes a window with the given class name, title, and style.

Showing the Window: The ShowWindow function makes the window visible.

Message Loop: The message loop gets and sends messages to the window.

This basic example shows how a Windows application is set up. It includes making a window, managing messages, and running a loop to handle those messages. From here, you can make more advanced apps by adding new features and working with other parts of the Windows system.

# Chapter 2

## Basic Windows Concepts

The Windows Message System

The Windows operating system uses messages to manage user actions and system events. Every time you move the mouse or press a key, it creates a message. These messages are sent to the right handler, which deals with them as needed.

Message Loop

Every Windows app relies on a message loop to function. This loop gets messages from the application's message queue and sends them to the right window functions. Let's take a closer look at the message loop:

MSG msg;

while (GetMessage(&msg, NULL, 0, 0)) {

TranslateMessage(&msg);

DispatchMessage(&msg);

}

GetMessage: Gets a message from the list. It waits until a message is ready.

TranslateMessage: Changes keyboard key messages into character messages.

DispatchMessage: Sends the message to the window's handler.

Window Procedure

The window procedure is a function that takes care of messages for a window. Each window has its own way of doing things. This involves handling messages like WM_PAINT, which helps to draw on the window, and WM_DESTROY, which helps to free up resources when the window is closed.

LRESULT CALLBACK WindowProc(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam) {

switch (uMsg) {

case WM_PAINT:

// Handle painting

break;

case WM_DESTROY:

PostQuitMessage(0);

return 0;

default:

return DefWindowProc(hwnd, uMsg, wParam, lParam);

}

}

Common Messages

WM_CREATE: This message is sent when a window is being made.

WM_CLOSE: This message is sent when a window is about to be closed.

WM_PAINT: This message is sent when the window needs to be redrawn.

WM_DESTROY: This message is sent when the window is closing.

The WinMain Function

Purpose of WinMain

The WinMain function is where a Windows program starts. It starts the application, creates the main window, and runs the message loop.

Structure of WinMain

int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow) {

// Step 1: Register the window class

WNDCLASS wc = {};

wc.lpfnWndProc = WindowProc;

wc.hInstance = hInstance;

wc.lpszClassName = "SampleWindowClass";

RegisterClass(&wc);

// Step 2: Create the window

HWND hwnd = CreateWindowEx(

0,                              // Optional window styles

"SampleWindowClass",            // Window class

"Learn to Program Windows",     // Window text

WS_OVERLAPPEDWINDOW,            // Window style

CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, // Size and position

NULL,       // Parent window

NULL,       // Menu

hInstance,  // Instance handle

NULL        // Additional application data

);

if (hwnd == NULL) {

return 0;

}

ShowWindow(hwnd, nCmdShow);

// Step 3: Run the message loop

MSG msg = {};

while (GetMessage(&msg, NULL, 0, 0)) {

TranslateMessage(&msg);

DispatchMessage(&msg);

}

return 0;

}

Parameters of WinMain

hInstance: A reference to the current version of the application.

hPrevInstance: Always set to NULL in current Windows apps.

lpCmdLine: The command line inputs as one string.

nCmdShow: A marker that indicates if the main window will be small, big, or displayed normally.

Creating a Simple Window

Registering a Window Class

Before you can make a window, you need to set up a window class first. This means completing a WNDCLASS form and then using RegisterClass.

WNDCLASS wc = {};

wc.lpfnWndProc = WindowProc;

wc.hInstance = hInstance;

wc.lpszClassName = "SampleWindowClass";

RegisterClass(&wc);

Creating the Window

Use CreateWindowEx to make a window. This function uses inputs to set up the window's type, name, appearance, size, and location.

HWND hwnd = CreateWindowEx(

0,                              // Optional window styles

"SampleWindowClass",            // Window class

"Learn to Program Windows",     // Window text

WS_OVERLAPPEDWINDOW,            // Window style

CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, // Size and position

NULL,       // Parent window

NULL,       // Menu

hInstance,  // Instance handle

NULL        // Additional application data

);

Showing the Window

After the window is made, use ShowWindow and UpdateWindow to make it appear.

ShowWindow(hwnd, nCmdShow);

UpdateWindow(hwnd);

Handling Messages

Set up the window procedure to manage messages that are sent to the window. This is where you handle actions like painting the window or shutting it.

LRESULT CALLBACK WindowProc(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam) {

switch (uMsg) {

case WM_PAINT:

PAINTSTRUCT ps;

HDC hdc = BeginPaint(hwnd, &ps);

// All painting occurs here

EndPaint(hwnd, &ps);

break;

case WM_DESTROY:

PostQuitMessage(0);

break;

default:

return DefWindowProc(hwnd, uMsg, wParam, lParam);

}

return 0;

}

Handling Messages

Managing messages is an important part of Windows programming. Every window has a specific way to handle messages that the system sends to it.

Defining the Window Procedure

The way to handle a window is explained like this:

LRESULT CALLBACK WindowProc(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam);

hwnd: A label for the window getting the message.

uMsg: The message ID.

wParam: Extra information about the message (specific to the message).

lParam: Extra information about the message (specific to the message).

Common Messages and Their Handling

WM_CREATE: Sent when the window is being created.

case WM_CREATE:

// Initialization code

break;

WM_PAINT: Sent when the window needs to be repainted.

case WM_PAINT:

PAINTSTRUCT ps;

HDC hdc = BeginPaint(hwnd, &ps);

// Drawing code

EndPaint(hwnd, &ps);

break;

WM_CLOSE: Sent when the user clicks the close button.

case WM_CLOSE:

DestroyWindow(hwnd);

break;

WM_DESTROY: Sent when the window is being destroyed.

c

Copy code

case WM_DESTROY:

PostQuitMessage(0);

break;

The Default Window Procedure

If a message isn’t handled in the window procedure, it should be sent to the default window procedure using DefWindowProc. This makes sure that all messages are taken care of properly.

default:

return DefWindowProc(hwnd, uMsg, wParam, lParam);

Example: Handling Mouse Clicks

To manage mouse clicks, process the WM_LBUTTONDOWN message in the window function.

case WM_LBUTTONDOWN:

int xPos = GET_X_LPARAM(lParam);

int yPos = GET_Y_LPARAM(lParam);

// Handle mouse click at (xPos, yPos)

break;

Example: Handling Keyboard Input

To manage keyboard input, take care of the WM_KEYDOWN message in the window function.

case WM_KEYDOWN:

switch (wParam) {

case VK_LEFT:

// Handle left arrow key press

break;

case VK_RIGHT:

// Handle right arrow key press

break;

// Handle other keys

}

break;

Advanced Message Handling

To manage messages better, you can use PeekMessage. This lets you check for messages without stopping your application, so it can keep doing other tasks while waiting for new messages.

while (true) {

if (PeekMessage(&msg, NULL, 0, 0, PM_REMOVE)) {

TranslateMessage(&msg);

DispatchMessage(&msg);

} else {

// Perform background tasks

}

}

Conclusion

In this chapter, we talked about the basics of Windows programming. We learned about the Windows message system, the WinMain function, how to create a simple window, and how to deal with messages. These basics give you a strong base to create more complicated Windows apps. As you keep learning, you will learn about more complicated topics like how to use buttons and menus, graphics, handling files, and doing many things at once. These all connect to the main ideas we've discussed. By learning these basic skills, you will be able to make strong and quick Windows programs using C and C++.

# Chapter 3

## User Interface Basics

Introduction to Windows Controls

Windows controls, or widgets, are the basic parts that make up the user interfaces in Windows apps. They have buttons, text fields, labels, lists, and other things. These controls are very important for making applications that are easy to use and interactive.

Types of Windows Controls

Static Controls: Used to show text or pictures that the user does not need to interact with, like labels.

Button Controls: Used to do things when you click them, like command buttons.

Edit Controls: These are used for typing text, like single-line boxes and boxes where you can write multiple lines.

List Controls: These are used to show lists of things, like list boxes and combo boxes.

Scroll Bars: Used to move through content in a window.

Group Boxes: Used to keep similar controls together.

Creating and Using Controls

You make controls by using the CreateWindow or CreateWindowEx function and by choosing the right class name for the type of control you want. For instance, to make a button:

HWND hButton = CreateWindow(

"BUTTON",       // Predefined class; Unicode assumed

"Click Me",     // Button text

WS_TABSTOP | WS_VISIBLE | WS_CHILD | BS_DEFPUSHBUTTON,  // Styles

10,             // x position

10,             // y position

100,            // Button width

30,             // Button height

hWnd,           // Parent window

NULL,           // No menu.

(HINSTANCE)GetWindowLongPtr(hWnd, GWLP_HINSTANCE),

NULL            // Pointer not needed.

);

Handling Control Messages

Controls send messages to the main window when things happen. These messages are handled in the window process. For example, to manage when a button is clicked:

case WM_COMMAND:

if (HIWORD(wParam) == BN_CLICKED) {

int id = LOWORD(wParam);

if (id == BUTTON_ID) {

// Handle button click

}

}

break;

Working with Buttons, Text Boxes, and Labels

Button Controls

Buttons are one of the most common features in Windows programs. They are used to do things when the user clicks on them. You can make buttons using the CreateWindow or CreateWindowEx function with the BUTTON type.

Creating a Button

HWND hButton = CreateWindow(

"BUTTON",        // Button class

"Click Me",      // Button text

WS_TABSTOP | WS_VISIBLE | WS_CHILD | BS_DEFPUSHBUTTON,  // Button styles

50,              // x position

50,              // y position

100,             // Button width

30,              // Button height

hWnd,            // Parent window

(HMENU)ID_BUTTON, // Button ID

hInstance,       // Application instance

NULL             // Additional application data

);

Handling Button Clicks

Button clicks are managed in the main window's message handler using the WM_COMMAND message.

case WM_COMMAND:

if (LOWORD(wParam) == ID_BUTTON && HIWORD(wParam) == BN_CLICKED) {

// Handle button click

MessageBox(hWnd, "Button clicked!", "Notification", MB_OK);

}

break;

Text Boxes (Edit Controls)

Text boxes, also called edit boxes, let users type in text. They can be one line or many lines.

Creating a Single-Line Text Box

HWND hEdit = CreateWindow(

"EDIT",          // Edit class

"",              // Initial text

WS_CHILD | WS_VISIBLE | WS_BORDER | ES_LEFT,  // Edit styles

50,              // x position

100,             // y position

200,             // Edit width

25,              // Edit height

hWnd,            // Parent window

(HMENU)ID_EDIT,  // Edit ID

hInstance,       // Application instance

NULL             // Additional application data

);

Creating a Multi-Line Text Box

HWND hEdit = CreateWindow(

"EDIT",          // Edit class

"",              // Initial text

WS_CHILD | WS_VISIBLE | WS_BORDER | ES_LEFT | ES_MULTILINE | ES_AUTOVSCROLL,  // Edit styles

50,              // x position

150,             // y position

300,             // Edit width

100,             // Edit height

hWnd,            // Parent window

(HMENU)ID_EDIT,  // Edit ID

hInstance,       // Application instance

NULL             // Additional application data

);

Handling Text Box Input

You can get the text from a text box using the GetWindowText function.

case WM_COMMAND:

if (LOWORD(wParam) == ID_EDIT && HIWORD(wParam) == EN_CHANGE) {

char buffer[256];

GetWindowText(hEdit, buffer, sizeof(buffer));

// Handle text change

}

break;

Label Controls (Static Controls)

Labels, also called static controls, show text that people don't need to click on or interact with.

Creating a Label

HWND hLabel = CreateWindow(

"STATIC",        // Static class

"Enter text:",   // Label text

WS_CHILD | WS_VISIBLE,  // Label styles

50,              // x position

20,              // y position

100,             // Label width

25,              // Label height

hWnd,            // Parent window

NULL,            // No menu

hInstance,       // Application instance

NULL             // Additional application data

);

Labels stay the same and don’t need to send messages to the main window, so you don't need to do anything extra.

Using Dialog Boxes

Dialog boxes are special windows that ask users for information or action. They are often used for things like opening files, saving files, or showing messages.

There are two kinds of dialog boxes: modal and modeless.

Modal dialog boxes need the user to close them before they can use the main window.

Modeless dialog boxes let users work with both the dialog box and the main window at the same time.

Creating Modal Dialog Boxes

Modal dialog boxes are usually made with a dialog template from a resource file and opened using the DialogBox function.

Dialog Resource Template

IDD_DIALOG1 DIALOGEX 0, 0, 276, 95

STYLE DS_SETFONT | DS_MODALFRAME | WS_POPUP | WS_CAPTION | WS_SYSMENU

CAPTION "Sample Dialog"

FONT 8, "MS Shell Dlg"

BEGIN

LTEXT           "Enter name:",IDC_STATIC,7,14,50,8

EDITTEXT        IDC_EDIT1,7,24,262,12,ES_AUTOHSCROLL

PUSHBUTTON      "OK",IDOK,110,74,50,14

PUSHBUTTON      "Cancel",IDCANCEL,163,74,50,14

END

Invoking the Dialog Box

INT_PTR CALLBACK DialogProc(HWND hDlg, UINT message, WPARAM wParam, LPARAM lParam) {

switch (message) {

case WM_INITDIALOG:

return (INT_PTR)TRUE;

case WM_COMMAND:

if (LOWORD(wParam) == IDOK || LOWORD(wParam) == IDCANCEL) {

EndDialog(hDlg, LOWORD(wParam));

return (INT_PTR)TRUE;

}

break;

}

return (INT_PTR)FALSE;

}

void ShowDialog(HWND hWnd) {

DialogBox(hInstance, MAKEINTRESOURCE(IDD_DIALOG1), hWnd, DialogProc);

}

Creating Modeless Dialog Boxes

Modeless dialog boxes are made with the CreateDialog function and need to be displayed using the ShowWindow function.

Creating and Showing a Modeless Dialog Box

HWND hDlg = CreateDialog(hInstance, MAKEINTRESOURCE(IDD_DIALOG1), hWnd, DialogProc);

ShowWindow(hDlg, SW_SHOW);

Handling Dialog Box Messages

Dialog boxes manage messages like normal windows, but their message handling functions give back TRUE if they deal with a message and FALSE if they don’t.

INT_PTR CALLBACK DialogProc(HWND hDlg, UINT message, WPARAM wParam, LPARAM lParam) {

switch (message) {

case WM_INITDIALOG:

return (INT_PTR)TRUE;

case WM_COMMAND:

if (LOWORD(wParam) == IDOK || LOWORD(wParam) == IDCANCEL) {

EndDialog(hDlg, LOWORD(wParam));

return (INT_PTR)TRUE;

}

break;

}

return (INT_PTR)FALSE;

}

Managing Menus and Toolbars

Menus are an important part of the user interface, helping users find commands and features. Menus are usually found at the top of the screen and can have smaller menus and options inside them.

Creating Menus

Menus are set up in a file and are added to the app while it's running.

Menu Resource Definition

IDR_MENU1 MENU

BEGIN

POPUP "&File"

BEGIN

MENUITEM "&Open", ID_FILE_OPEN

MENUITEM "E&xit", ID_FILE_EXIT

END

POPUP "&Help"

BEGIN

MENUITEM "&About", ID_HELP_ABOUT

END

END

Loading and Attaching Menus

Menus are added with the LoadMenu function and connected to the window using the SetMenu function.

HMENU hMenu = LoadMenu(hInstance, MAKEINTRESOURCE(IDR_MENU1));

SetMenu(hWnd, hMenu);

Handling Menu Commands

Menu commands are managed in the window procedure with a WM_COMMAND message.

case WM_COMMAND:

switch (LOWORD(wParam)) {

case ID_FILE_OPEN:

// Handle file open

break;

case ID_FILE_EXIT:

DestroyWindow(hWnd);

break;

case ID_HELP_ABOUT:

MessageBox(hWnd, "About this application", "About", MB_OK);

break;

}

break;

Overview of Toolbars

Toolbars have buttons that let you quickly use common commands. They are usually found right under the menu bar.

Creating Toolbars

You can make toolbars using the CreateWindowEx function and the TOOLBARCLASSNAME class.

HWND hToolbar = CreateWindowEx(0, TOOLBARCLASSNAME, NULL, WS_CHILD | WS_VISIBLE | TBSTYLE_WRAPABLE, 0, 0, 0, 0, hWnd, NULL, hInstance, NULL);

Adding Buttons to the Toolbar

You can add toolbar buttons by using the TBADDBUTTONS message.

TBBUTTON tbButtons[] = {

{ MAKELONG(STD_FILENEW, 0), ID_FILE_NEW, TBSTATE_ENABLED, BTNS_BUTTON, {0}, 0, (INT_PTR)"New" },

{ MAKELONG(STD_FILEOPEN, 0), ID_FILE_OPEN, TBSTATE_ENABLED, BTNS_BUTTON, {0}, 0, (INT_PTR)"Open" },

{ MAKELONG(STD_FILESAVE, 0), ID_FILE_SAVE, TBSTATE_ENABLED, BTNS_BUTTON, {0}, 0, (INT_PTR)"Save" }

};

SendMessage(hToolbar, TB_ADDBUTTONS, sizeof(tbButtons)/sizeof(TBBUTTON), (LPARAM)&tbButtons);

Handling Toolbar Commands

Toolbar commands work like menu commands in the window procedure by using the WM_COMMAND message.

case WM_COMMAND:

switch (LOWORD(wParam)) {

case ID_FILE_NEW:

// Handle new file

break;

case ID_FILE_OPEN:

// Handle open file

break;

case ID_FILE_SAVE:

// Handle save file

break;

}

break;

Conclusion

In this chapter, we learned the basics of creating user interfaces for Windows apps using C and C++. We talked about important controls such as buttons, text boxes, and labels. We talked about how to create and use dialog boxes, menus, and toolbars.

Knowing these basic parts is important for making apps that are easy to use and interactive. In the next chapter, we will explore more advanced user interface features and methods. This includes creating custom controls, managing input from different devices, and making the user experience better with animations and visual effects.

# Chapter 4

## Graphics and Drawing

Introduction to GDI (Graphics Device Interface)

The Graphics Device Interface (GDI) is an important part of the Windows operating system that helps programs show images and graphics. It offers tools to create text, shapes, and pictures on screens and printers.

GDI Components

Device Context (DC): A system that describes a group of visual elements and their features, along with the settings that influence how things appear on the screen.

Pens: Used to make lines and shapes.

Brushes: Used to color in shapes.

Fonts: They are used to create letters and words.

Bitmaps: Used for handling pictures.

Getting a Device Context

You get a device context by using the GetDC function for a window or by using the BeginPaint function when handling the WM_PAINT message.

HDC hdc = GetDC(hwnd);

After using the device context, make sure to free it by using ReleaseDC.

ReleaseDC(hwnd, hdc);

Drawing Basics

Drawing Lines and Shapes

Drawing in GDI is done using functions that work with a device context.

Drawing Lines

You draw lines using the MoveToEx and LineTo functions.

MoveToEx(hdc, 10, 10, NULL);  // Move to starting point

LineTo(hdc, 100, 100);        // Draw line to endpoint

Drawing Rectangles

You can make rectangles using the Rectangle function.

Rectangle(hdc, 50, 50, 200, 150);  // Draw a rectangle from (50, 50) to (200, 150)

Drawing Ellipses

You can draw ellipses using the Ellipse tool.

Ellipse(hdc, 60, 60, 180, 120);  // Draw an ellipse within the bounding rectangle (60, 60) to (180, 120)

Using Pens and Brushes

Pens and brushes create the look of lines and colors.

Making and Choosing a Pen

Make a pen using the CreatePen function and put it into the device context with SelectObject.

HPEN hPen = CreatePen(PS_SOLID, 2, RGB(255, 0, 0));  // Create a solid red pen with a width of 2

SelectObject(hdc, hPen);

Creating and Selecting a Brush

Make a brush with the CreateSolidBrush function and use SelectObject to add it to the device context.

HBRUSH hBrush = CreateSolidBrush(RGB(0, 255, 0));  // Create a solid green brush

SelectObject(hdc, hBrush);

Drawing Text

Text is drawn using the TextOut function.

TextOut(hdc, 10, 10, "Hello, GDI!", strlen("Hello, GDI!"));  // Draw text at (10, 10)

Handling the WM_PAINT Message

The WM_PAINT Message

The WM_PAINT message is sent to a window when it needs to be redrawn. To work with this message, you need to use the BeginPaint and EndPaint functions to get and then release the drawing area.

case WM_PAINT: {

PAINTSTRUCT ps;

HDC hdc = BeginPaint(hwnd, &ps);

// Perform drawing operations here

EndPaint(hwnd, &ps);

break;

}

Example: Drawing in the WM_PAINT Handler

case WM_PAINT: {

PAINTSTRUCT ps;

HDC hdc = BeginPaint(hwnd, &ps);

// Draw a rectangle

Rectangle(hdc, 50, 50, 200, 150);

// Draw an ellipse

Ellipse(hdc, 60, 60, 180, 120);

// Draw text

TextOut(hdc, 10, 10, "Hello, GDI!", strlen("Hello, GDI!"));

EndPaint(hwnd, &ps);

break;

}

Working with Bitmaps

Loading and Displaying Bitmaps

Bitmaps are often used for pictures in Windows programs. They can be taken from resources or files and shown using GDI functions.

Loading a Bitmap from a Resource

HBITMAP hBitmap = LoadBitmap(hInstance, MAKEINTRESOURCE(IDB_BITMAP1));

Showing a Bitmap

To show a bitmap, you first need to choose it for a memory area and then use BitBlt to move it to the device where you want to display it.

HDC hdcMem = CreateCompatibleDC(hdc);

SelectObject(hdcMem, hBitmap);

BitBlt(hdc, 0, 0, bmpWidth, bmpHeight, hdcMem, 0, 0, SRCCOPY);

DeleteDC(hdcMem);

Example: Displaying a Bitmap in WM_PAINT

case WM_PAINT: {

PAINTSTRUCT ps;

HDC hdc = BeginPaint(hwnd, &ps);

HBITMAP hBitmap = LoadBitmap(hInstance, MAKEINTRESOURCE(IDB_BITMAP1));

HDC hdcMem = CreateCompatibleDC(hdc);

SelectObject(hdcMem, hBitmap);

BITMAP bitmap;

GetObject(hBitmap, sizeof(bitmap), &bitmap);

BitBlt(hdc, 0, 0, bitmap.bmWidth, bitmap.bmHeight, hdcMem, 0, 0, SRCCOPY);

DeleteDC(hdcMem);

DeleteObject(hBitmap);

EndPaint(hwnd, &ps);

break;

}

Advanced Drawing Techniques

Using Regions

Regions are areas made up of shapes like rectangles, polygons, or ellipses. They are helpful for complicated cutting and checking actions.

Creating and Using Regions

HRGN hRgn = CreateEllipticRgn(50, 50, 200, 150);  // Create an elliptical region

SelectClipRgn(hdc, hRgn);  // Select the region into the device context for clipping

Double Buffering

Double buffering is a method that helps eliminate flickering by first drawing images in a hidden area and then quickly showing them on the screen.

Using Double Buffering

Make a device context and bitmap that work well together.

Draw on the device that works with it.

Show the contents on the screen.

HDC hdcMem = CreateCompatibleDC(hdc);

HBITMAP hbmMem = CreateCompatibleBitmap(hdc, width, height);

SelectObject(hdcMem, hbmMem);

// Perform drawing operations on hdcMem

BitBlt(hdc, 0, 0, width, height, hdcMem, 0, 0, SRCCOPY);

DeleteObject(hbmMem);

DeleteDC(hdcMem);

Using Alpha Blending

Alpha blending lets you draw with transparency by mixing two images together using alpha values.

Implementing alpha blending

BLENDFUNCTION blendFunction;

blendFunction.BlendOp = AC_SRC_OVER;

blendFunction.BlendFlags = 0;

blendFunction.SourceConstantAlpha = 128;  // Half transparency

blendFunction.AlphaFormat = 0;

AlphaBlend(hdc, xDest, yDest, width, height, hdcSrc, xSrc, ySrc, width, height, blendFunction);

GDI+ for Advanced Graphics

GDI+ is a graphics tool that adds more options to GDI. It includes things like smooth colors, better image quality, and the ability to work with more types of images.

Setting Up GDI+

To use GDI+, you need to set it up when your app starts and turn it off when your app closes.

GdiplusStartupInput gdiplusStartupInput;

ULONG_PTR gdiplusToken;

GdiplusStartup(&gdiplusToken, &gdiplusStartupInput, NULL);

// Perform GDI+ operations

GdiplusShutdown(gdiplusToken);

Drawing with GDI+

GDI+ offers a way to draw using objects. Some common classes are Graphics, Pen, Brush, and Bitmap.

Drawing Shapes with GDI+

Graphics graphics(hdc);

Pen pen(Color(255, 0, 0, 255));  // Red pen

graphics.DrawLine(&pen, 10, 10, 100, 100);  // Draw a line

SolidBrush brush(Color(255, 0, 255, 0));  // Green brush

graphics.FillRectangle(&brush, 50, 50, 150, 100);  // Draw a filled rectangle

Drawing Images with GDI+

Bitmap bitmap(L"example.jpg");

graphics.DrawImage(&bitmap, 0, 0, bitmap.GetWidth(), bitmap.GetHeight());

Anti-Aliasing

GDI+ helps make the edges of shapes and text smoother so they look nicer.

graphics.SetSmoothingMode(SmoothingModeAntiAlias);

graphics.SetTextRenderingHint(TextRenderingHintAntiAlias);

Conclusion

In this chapter, we have looked at the basic and advanced methods of graphics and drawing in Windows apps. We've explained important ideas and provided code examples, starting from simple drawing with GDI to more complex tools with GDI+, to help you make great graphical interfaces. In the next chapter, we will look at how to work with input from different devices and how to manage user interactions well to improve the user experience.

# Chapter 5

## File and Data Management

Introduction to File Handling in Windows

File handling in Windows means doing things with files, like making them, opening them, writing in them, and organizing them. The Windows API has tools that help programs manage files on the computer.

File operation

Making a File: This means starting a new file or opening a file that already exists if it’s not already there.

Reading from a file means getting the information inside a file so you can use it.

Writing to a file means changing or adding information to a file.

Closing a file makes sure that everything is saved correctly and frees up any resources used.

File Functions in Windows

The main tasks for handling files are CreateFile (to make a file), ReadFile (to open and read a file), WriteFile (to add or change information in a file), and CloseHandle (to close the file when done).

Creating and Opening Files

The CreateFile

The CreateFile function is used to make a new file or open an existing one. It provides a handle that you can use for more tasks.

HANDLE hFile = CreateFile(

"example.txt",       // File name

GENERIC_READ | GENERIC_WRITE,  // Desired access

0,                   // Share mode

NULL,                // Security attributes

CREATE_ALWAYS,       // Creation disposition

FILE_ATTRIBUTE_NORMAL,  // Flags and attributes

NULL                 // Template file

);

File Name: The location of the file.

Desired Access: The kind of access you want for the file (like reading or writing).

Share Mode: Shows how the file can be shared.

Creation Disposition: Decides how the file is made or accessed.

Flags and Attributes: Shows the file's features (like if it’s a regular file).

Error Handling

Make sure that CreateFile worked by checking if the handle is INVALID_HANDLE_VALUE.

if (hFile == INVALID_HANDLE_VALUE) {

DWORD error = GetLastError();

// Handle error

}

Reading from Files

The ReadFile Function

The ReadFile function reads data from a file into a buffer.

CHAR buffer[1024];

DWORD bytesRead;

BOOL result = ReadFile(

hFile,           // File handle

buffer,          // Buffer to receive data

sizeof(buffer),  // Number of bytes to read

&bytesRead,      // Number of bytes read

NULL             // Overlapped structure

);

Buffer: The place where data that is read is kept.

Bytes Read: The total amount of data taken from the file.

Checking for Errors

Make sure to see if ReadFile doesn't work by looking at what it returns, and use GetLastError to find out what the error is.

if (!result) {

DWORD error = GetLastError();

// Handle error

}

Writing to Files

The WriteFile Function

The WriteFile function saves data from a storage area to a file.

const CHAR *data = "Hello, World!";

DWORD bytesWritten;

BOOL result = WriteFile(

hFile,           // File handle

data,            // Data to write

strlen(data),    // Number of bytes to write

&bytesWritten,   // Number of bytes written

NULL             // Overlapped structure

);

Data: The temporary storage holding the information that needs to be written.

Bytes Written: The total amount of data written to the file.

Checking for Errors

Just like when you're reading, check if WriteFile has an error by looking at the return value, and use GetLastError to get more details about the error.

if (!result) {

DWORD error = GetLastError();

// Handle error

}

Closing Files

The CloseHandle Function

The CloseHandle function shuts down an open file and frees up its resources.

CloseHandle(hFile);

Always remember to close file handles after you're done using them to avoid wasting resources.

File Attributes and Operations

Getting Info About Files

The GetFileAttributes function gets the details about a file or folder.

DWORD attributes = GetFileAttributes("example.txt");

if (attributes == INVALID_FILE_ATTRIBUTES) {

DWORD error = GetLastError();

// Handle error

}

Changing File Settings

The SetFileAttributes function changes the settings of a file or folder.

BOOL result = SetFileAttributes("example.txt", FILE_ATTRIBUTE_READONLY);

if (!result) {

DWORD error = GetLastError();

// Handle error

}

Deleting a File

The DeleteFile function deletes a specified file.

BOOL result = DeleteFile("example.txt");

if (!result) {

DWORD error = GetLastError();

// Handle error

}

Working with Directories

Creating and Removing Directories

Making a Folder: Use CreateDirectory to make a new folder.

BOOL result = CreateDirectory("new_directory", NULL);

if (!result) {

DWORD error = GetLastError();

// Handle error

}

To delete a folder, use RemoveDirectory if the folder is empty.

BOOL result = RemoveDirectory("new_directory");

if (!result) {

DWORD error = GetLastError();

// Handle error

}

Enumerating Files and Directories

Use the FindFirstFile and FindNextFile functions to list files and folders.

WIN32_FIND_DATA findFileData;

HANDLE hFind = FindFirstFile("*.txt", &findFileData);

if (hFind == INVALID_HANDLE_VALUE) {

DWORD error = GetLastError();

// Handle error

} else {

do {

// Process file or directory

} while (FindNextFile(hFind, &findFileData) != 0);

FindClose(hFind);

}

Working with File Mappings

File mappings let programs read and use the data from a file directly in memory. This method can make working with big files or accessing things often faster.

Creating a File Mapping

Use CreateFileMapping to make a file mapping object.

HANDLE hMapping = CreateFileMapping(

hFile,          // File handle

NULL,           // Security attributes

PAGE_READWRITE, // Protection

0,              // Maximum size high

fileSize,       // Maximum size low

NULL            // Name of the mapping object

);

Mapping a View of the File

Use MapViewOfFile to make a part of the file visible in the program's memory.

LPVOID pMapView = MapViewOfFile(

hMapping,    // Mapping handle

FILE_MAP_ALL_ACCESS, // Desired access

0,           // File offset high

0,           // File offset low

fileSize      // Number of bytes to map

);

Accessing the Mapped File

You can use the pointer from MapViewOfFile to get the file data.

memcpy(pMapView, "New Data", 8); // Write data to the file

Removing the File Mapping

Use UnmapViewOfFile to remove the file from memory and CloseHandle to close the mapping object.

UnmapViewOfFile(pMapView);

CloseHandle(hMapping);

Error Handling and Diagnostics

Dealing with Mistakes

Good error handling is very important when managing files and data. Use GetLastError to get the error number when a function doesn't work.

DWORD error = GetLastError();

Using Tools to Figure Things Out

Error Codes: Check Windows instructions to understand error codes.

Debugging: Use tools to follow file activities and find problems.

Conclusion

In this chapter, we talked about the important parts of handling files and data in Windows programming. We looked into making files, reading them, writing in them, and closing them. We also learned how to manage file details, folders, and how files relate to each other. Knowing these ideas is essential for managing files and data well in your apps. In the next chapter, we will explore multi-threading and concurrency, looking at ways to improve how well applications work and respond.

# Chapter 6

## Multithreading and Concurrency

Introduction to Multithreading

Multithreading is a way of programming that allows many threads to run at the same time in one program. Threads use the same resources but run separately. This method can make applications run better by using multiple processor cores and providing a smoother experience for users.

Important Ideas

Thread: The smallest part of a program that can run on its own.

Process: A running program that has one or more threads inside it.

Concurrency means the system can do many tasks at the same time.

Advantages of Using Multithreading

Responsiveness: Keeps apps working smoothly by moving tasks like background work to other places.

Performance: Uses several CPU cores to do calculations at the same time.

Resource Sharing: Lets threads use memory and resources together in a process effectively.

Creating and Managing Threads

The CreateThread Function

In Windows, you make threads using the CreateThread function. This function creates a new thread and gives you a way to access it.

DWORD WINAPI ThreadFunction(LPVOID lpParam) {

// Thread code here

return 0;

}

HANDLE hThread = CreateThread(

NULL,                   // Default security attributes

0,                      // Default stack size

ThreadFunction,         // Thread function

NULL,                   // Parameter to thread function

0,                      // Default creation flags

NULL                    // Pointer to thread identifier

);

Thread Function: The task that the thread will do.

Thread Handle: Used to control the thread (for example, to wait until it finishes).

Waiting for Threads

To wait for a thread to finish, use the WaitForSingleObject function.

WaitForSingleObject(hThread, INFINITE);  // Wait indefinitely for the thread to complete

"Shutting Down Thread Handles"

Use CloseHandle to close thread handles and free up resources.

CloseHandle(hThread);

Synchronization Techniques

Synchronization makes sure that several threads can use shared resources safely, avoiding conflicts or problems with the data. Common ways to manage synchronization include locks (mutexes), critical areas, and semaphores.

Important Parts

Critical sections help keep threads in the same process working together smoothly. They are easier to use and quicker than mutexes.

Using Critical Sections

Initialize: Initialize a critical section object.

CRITICAL_SECTION cs;

InitializeCriticalSection(&cs);

Enter: Enter the critical section before accessing shared resources.

EnterCriticalSection(&cs);

// Access shared resources

Leave: Leave the critical section when done.

LeaveCriticalSection(&cs);

Delete: Delete the critical section when no longer needed.

DeleteCriticalSection(&cs);

Mutexes

Mutexes are used to keep things in order when different parts of a program are working at the same time. They make sure that only one thread can use the mutex at a time.

Using Mutexes

Create: Create or open a named mutex.

HANDLE hMutex = CreateMutex(NULL, FALSE, "MyMutex");

Acquire: Wait for the mutex to be available.

WaitForSingleObject(hMutex, INFINITE);

Release: Release the mutex when done.

ReleaseMutex(hMutex);

Close: Close the mutex handle.

CloseHandle(hMutex);

Semaphores

Semaphores control how many people can use a limited number of resources. They are used to manage how many threads can use a resource at the same time.

Using Semaphores

Create: Create a semaphore with an initial count.

HANDLE hSemaphore = CreateSemaphore(NULL, 1, 1, "MySemaphore");

Wait: Decrement the semaphore count and wait if the count is zero.

WaitForSingleObject(hSemaphore, INFINITE);

Release: Increment the semaphore count.

ReleaseSemaphore(hSemaphore, 1, NULL);

Close: Close the semaphore handle.

CloseHandle(hSemaphore);

Thread Communication

Threads often need to talk to each other or share information. This can be done using shared memory, sending messages, or using synchronization tools.

Using Common Memory

Threads in the same process can directly use shared memory by using global or static variables. We need to keep things in sync to avoid messing up the data.

// Shared resource

int sharedData;

void ThreadFunction(LPVOID lpParam) {

EnterCriticalSection(&cs);

sharedData++;  // Modify shared resource

LeaveCriticalSection(&cs);

}

Message Passing

Threads can use message queues or ways to communicate between processes to send messages to each other.

Example: PostMessage Function

PostMessage(hwnd, WM_USER + 1, (WPARAM)wParam, (LPARAM)lParam);

hwnd: A reference to the window that is getting the message.

wParam: Information related to a specific message.

lParam: Extra information related to the message.

Managing Thread Lifecycles

Making Threads on the Go

Threads can be started whenever they are needed, which helps applications use resources better.

HANDLE hThread = CreateThread(NULL, 0, ThreadFunction, NULL, 0, NULL);

Stopping Threads

Threads should be ended properly to prevent wasting resources. Only use TerminateThread as a last option.

TerminateThread(hThread, 0);  // Not recommended; use proper synchronization

Thread pools

Thread pools are groups of worker threads that can be used again for different jobs, which helps make things run better and use resources more efficiently.

Using the Thread Pool API

HANDLE hPool = CreateThreadpool(NULL);

SetThreadpoolThreadMaximum(hPool, 4);

SetThreadpoolThreadMinimum(hPool, 2);

CreateThreadpool: Makes a group of threads ready to use.

SetThreadpoolThreadMaximum: This sets the highest number of threads allowed.

SetThreadpoolThreadMinimum: Sets the least number of threads needed.

Handling Thread Errors

Looking for Mistakes

Always look for mistakes in thread operations by using the GetLastError function.

DWORD error = GetLastError();

Debugging Threads

Use debugging tools to watch how threads run and find problems.

Visual Studio Debugger: Lets you check and manage threads.

Fixing API issues: Use tools like DebugActiveProcess and DebugSetProcessKillOnExit.

Advanced Multithreading Concepts

Thread Safety

Make sure that shared resources are safe and can be used properly by different threads at the same time.

Atomic Operations: Use atomic operations to safely update data when multiple threads are working at the same time.

Lock-Free Data Structures: Use data structures that allow safe operations without needing to lock them when multiple threads are working.

Load balancing

Spread the work evenly across threads to get the best performance.

Task scheduling: Use methods to manage tasks to ensure workloads are balanced.

Work Stealing: Use work-stealing methods to evenly distribute tasks.

Real time thread

Real-time threads are designed to meet certain timing needs for programs that need to respond in a consistent way.

SetThreadPriority: Change the importance of threads to meet immediate needs.

Real-Time Scheduling: Use special rules to prioritize tasks that need to be completed quickly.

Conclusion

In this chapter, we looked at the basic and more advanced ideas of multithreading and concurrency in Windows programming. We discussed how to make and control threads, how to keep them in sync, how they can talk to each other, and how to manage their lives. By learning and using these ideas, you can create fast and responsive apps that make good use of multi-core processors.

# Chapter 7

## Network Programming

Network programming means making programs that can talk to each other through a network. It includes various methods to send and get information between computers or devices. In Windows, most network programming uses the Windows Sockets API (Winsock) to connect and communicate through TCP/IP and other methods.

Main Ideas

Socket: A point used to send or receive data over a network.

Protocol: A group of rules for sharing data, like TCP (Transmission Control Protocol) and UDP (User Datagram Protocol).

Client-Server Model: A way to set up a network where a client asks for help or information, and a server gives it to them.

Advantages of Network Programming

Communication: Allows programs to share information and talk to each other across different systems.

Distributed Systems: Help build applications that work across many computers.

Scalability: Lets apps grow by sharing tasks across different servers.

The Winsock API

The Windows Sockets API (Winsock) is a tool that helps programmers create network applications in Windows. It simplifies the network rules and provides tools to handle network connections and data transfer.

Starting Winsock

Before you use Winsock functions, start the library with WSAStartup.

#include <winsock2.h>

#include <ws2tcpip.h>

WSADATA wsaData;

int result = WSAStartup(MAKEWORD(2, 2), &wsaData);

if (result != 0) {

printf("WSAStartup failed: %d\n", result);

return 1;

}

WSAStartup: Starts the Winsock library.

MAKEWORD: Specifies which version of Winsock to use (2\. 2 in this example).

Cleaning up Winsock

After finishing network tasks, use WSACleanup to tidy up.

WSACleanup();

Creating a Socket

The Socket Function

Make a socket using the socket function, and choose the type of network, what kind of socket it is, and the protocol to use.

SOCKET sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);

if (sock == INVALID_SOCKET) {

printf("Socket creation failed: %d\n", WSAGetLastError());

WSACleanup();

return 1;

}

AF_INET: A type of address for IPv4.

SOCK_STREAM: This is a type of socket used for TCP connections.

IPPROTO_TCP: The protocol used for the connection.

Connecting a Socket

Connect the socket to a local address and port with the bind command.

struct sockaddr_in service;

service.sin_family = AF_INET;

service.sin_addr.s_addr = htonl(INADDR_ANY);

service.sin_port = htons(27015);

int result = bind(sock, (SOCKADDR*)&service, sizeof(service));

if (result == SOCKET_ERROR) {

printf("Bind failed: %d\n", WSAGetLastError());

closesocket(sock);

WSACleanup();

return 1;

}

INADDR_ANY: Connects to all available network connections.

htons: Changes the port number to the format used for network communication.

Listening and Accepting Connections

The Listen Function

Set up the socket to allow incoming connections by using the listen function.

int result = listen(sock, SOMAXCONN);

if (result == SOCKET_ERROR) {

printf("Listen failed: %d\n", WSAGetLastError());

closesocket(sock);

WSACleanup();

return 1;

}

SOMAXCONN: Specifies the maximum number of pending connections.

The accept Function

Accept incoming connections with accept.

SOCKET clientSocket = accept(sock, NULL, NULL);

if (clientSocket == INVALID_SOCKET) {

printf("Accept failed: %d\n", WSAGetLastError());

closesocket(sock);

WSACleanup();

return 1;

}

clientSocket: Handle to the newly connected socket.

Connecting to a Server

The Connect Function

For client apps, use "connect" to link up with a server.

struct sockaddr_in server;

server.sin_family = AF_INET;

server.sin_port = htons(27015);

inet_pton(AF_INET, "127.0.0.1", &server.sin_addr);

int result = connect(sock, (SOCKADDR*)&server, sizeof(server));

if (result == SOCKET_ERROR) {

printf("Connect failed: %d\n", WSAGetLastError());

closesocket(sock);

WSACleanup();

return 1;

}

Sending and Receiving Data

The send function

Send information to a connected socket using the send method.

const char* data = "Hello, Server!";

int result = send(sock, data, strlen(data), 0);

if (result == SOCKET_ERROR) {

printf("Send failed: %d\n", WSAGetLastError());

}

The recv Function

Receive data from a socket using recv.

char buffer[512];

int result = recv(sock, buffer, sizeof(buffer), 0);

if (result > 0) {

printf("Received data: %.*s\n", result, buffer);

} else if (result == 0) {

printf("Connection closed\n");

} else {

printf("Receive failed: %d\n", WSAGetLastError());

}

Closing Sockets

The closesocket function

Close the socket when you finish using it for network communication.

closesocket(sock);

Always close sockets to free up resources and prevent possible leaks.

Handling Multiple Connections

Using select for managing multiple connections

Select helps you check many sockets to see if they can read data, send data, or if there are any special issues.

fd_set readfds;

FD_ZERO(&readfds);

FD_SET(sock, &readfds);

int result = select(0, &readfds, NULL, NULL, NULL);

if (result == SOCKET_ERROR) {

printf("Select failed: %d\n", WSAGetLastError());

}

FD_ZERO: Clears the list of file descriptors.

FD_SET: Puts sockets into the group.

Choose: Keeps an eye on the sockets.

Asynchronous I/O with WSAAsyncSelect

For GUI applications, use WSAAsyncSelect to work on network events asynchronously.

WSAAsyncSelect(sock, hwnd, WM_SOCKET, FD_READ | FD_WRITE | FD_CLOSE);

hwnd: A window ID that gets messages.

WM_SOCKET: A tag that shows when something happens with a socket.

Error Handling and Debugging

Error codes

Use WSAGetLastError to get the last error code after a Winsock function doesn’t work.

DWORD error = WSAGetLastError();

Fixing Problems with Network Connections

Wireshark: Use it to look at and fix network data.

Logging: Set up a way to record network activities and problems.

Advanced Network Programming

Non-blocking Sockets

Change the sockets to non-blocking mode so they don’t stop other processes from running.

u_long mode = 1;

ioctlsocket(sock, FIONBIO, &mode);

Using Other Communication Methods Besides TCP/IP

Look into other methods like:

UDP (User Datagram Protocol): Used for sending messages without needing a connection.

HTTP/HTTPS: For websites and online apps.

FTP: For moving files.

Secure communication

Add security features like:

SSL/TLS: For secure messaging.

Authentication: To make sure only the right people can access resources.

Conclusion

In this chapter, we talked about the basics of network programming in Windows using the Winsock API. We looked into how to make connections, wait for them, send and receive information, and manage many connections at the same time. By learning these ideas, you can create strong networked applications that can communicate well using different network methods.

# Chapter 8

## Advanced Windows Programming

Advanced Windows programming uses more advanced features of the Windows API to build complicated and fast applications. This chapter talks about more complex subjects like how different parts of a program can communicate with each other, how to manage memory, advanced methods for keeping things in order, and using special Windows features to make applications better.

Main Ideas

Inter-Process Communication (IPC): Methods for sharing information between different processes.

Memory Management: Using and freeing up memory effectively.

Advanced Synchronization: Keeping threads safe and controlling access when multiple threads are used at the same time.

Windows Features: Using special Windows tools for better performance.

Inter-Process Communication (IPC)

IPC helps different programs talk to each other and share information. Windows has several ways for programs to talk to each other, like named pipes, shared memory, and message queues.

Named pipes

Named pipes are a way for programs to talk to each other, either over a network or on the same computer. They allow communication in one direction or both ways.

Creating a Named Pipe

Use CreateNamedPipe to create a named pipe.

HANDLE hPipe = CreateNamedPipe(

TEXT("\\\\.\\pipe\\MyPipe"),   // Pipe name

PIPE_ACCESS_DUPLEX,            // Read/Write access

PIPE_TYPE_MESSAGE | PIPE_READMODE_MESSAGE | PIPE_WAIT, // Pipe mode

1,                             // Number of instances

1024 * 16,                      // Output buffer size

1024 * 16,                      // Input buffer size

0,                             // Client time-out

NULL                           // Default security attributes

);

Connecting to a Named Pipe

Use ConnectNamedPipe on the server side and CreateFile on the client side.

BOOL connected = ConnectNamedPipe(hPipe, NULL);

On the client side:

HANDLE hPipe = CreateFile(

TEXT("\\\\.\\pipe\\MyPipe"),   // Pipe name

GENERIC_READ | GENERIC_WRITE,  // Desired access

0,                             // Share mode

NULL,                          // Default security attributes

OPEN_EXISTING,                  // Open existing pipe

0,                             // No flags

NULL                           // No template file

);

Shared memory

Shared memory lets different programs use the same part of memory.

Creating a File Mapping Object

Use CreateFileMapping to create a file mapping object.

HANDLE hMapFile = CreateFileMapping(

INVALID_HANDLE_VALUE,            // Use system paging file

NULL,                           // Default security attributes

PAGE_READWRITE,                  // Read/Write access

0,                              // Maximum object size (high-order bits)

1024 * 1024,                     // Maximum object size (low-order bits)

TEXT("SharedMemoryName")        // Name of the mapping object

);

Mapping a view of file

Show the file in the area of memory the process can use.

LPVOID pBuf = MapViewOfFile(

hMapFile,        // Handle to file mapping object

FILE_MAP_ALL_ACCESS, // Desired access

0,               // File offset high

0,               // File offset low

0                // Number of bytes to map

);

Message Queues

Message queues let applications talk to each other without needing to respond right away.

Making a Message Queue

Use CreateQueue or similar functions based on the message queue system you are using.

Sending and Getting Messages

Use SendMessage and PostMessage to send messages between windows or threads.

PostMessage(hwnd, WM_USER + 1, (WPARAM)wParam, (LPARAM)lParam);

hwnd: A reference for the window that is getting the message.

wParam: Extra information related to the message.

lParam: Extra information related to the message.

Memory Management

Good memory management helps things run well and makes the best use of resources. It means giving, using, and removing memory in a smart way.

Dynamic Memory Allocation

Use Windows-specific tools for better control of memory.

Allocating Memory

Heap Functions: Use HeapAlloc to get memory and HeapFree to release it when you’re done.

HANDLE hHeap = GetProcessHeap();

LPVOID pMemory = HeapAlloc(hHeap, HEAP_ZERO_MEMORY, 1024);

Virtual Memory Functions: Use VirtualAlloc and VirtualFree for larger allocations.

LPVOID pMemory = VirtualAlloc(

NULL,                 // Allocate memory in the address space of the calling process

1024 * 1024,          // Number of bytes to allocate

MEM_COMMIT,           // Allocate memory

PAGE_READWRITE        // Memory protection

);

Memory-Mapped Files

Memory-mapped files connect the data from a file directly with a program's memory. This lets the program read and write to the file as if it were using memory, making it faster and easier to work with.

Using Memory-Mapped Files

Making a File Mapping Object: Use CreateFileMapping.

To see the file, use MapViewOfFile.

Advanced Synchronization Techniques

Advanced synchronization methods help make sure that several threads or processes can use shared resources safely and effectively.

Event Objects

Event objects tell threads to go ahead or to hold on.

Creating and Using Events

HANDLE hEvent = CreateEvent(

NULL,       // Default security attributes

FALSE,      // Manual reset (FALSE for auto-reset)

FALSE,      // Initial state (FALSE for non-signaled)

TEXT("EventName") // Event name

);

WaitForSingleObject(hEvent, INFINITE);  // Wait for event to be signaled

SetEvent(hEvent);                        // Signal the event

Semaphores

Semaphores manage access to a limited number of resources.

Creating and Using Semaphores

HANDLE hSemaphore = CreateSemaphore(

NULL,      // Default security attributes

1,         // Initial count

10,        // Maximum count

TEXT("SemaphoreName") // Semaphore name

);

WaitForSingleObject(hSemaphore, INFINITE);  // Wait for semaphore

ReleaseSemaphore(hSemaphore, 1, NULL);      // Release semaphore

Mutexes

Mutexes allow only one thread or process to use a resource at a time.

Creating and Using Mutexes

HANDLE hMutex = CreateMutex(

NULL,      // Default security attributes

FALSE,     // Initial owner (FALSE for no initial owner)

TEXT("MutexName") // Mutex name

);

WaitForSingleObject(hMutex, INFINITE);  // Wait for mutex

ReleaseMutex(hMutex);                   // Release mutex

Leveraging Windows-Specific Features

Windows has extra tools to make applications better, like COM, special Windows API features, and ways to check how well they are running.

COM

COM is a Microsoft tool that helps create and use software parts that can be reused.

Using COM

Starting COM: Use CoInitialize or CoInitializeEx.

HRESULT hr = CoInitialize(NULL);

Creating COM Objects: Use CoCreateInstance

to create an instance of a COM object.

ICustomInterface* pInterface = NULL;

hr = CoCreateInstance(CLSID_CustomObject, NULL, CLSCTX_INPROC_SERVER, IID_ICustomInterface, (void**)&pInterface);

Uninitializing COM: Use CoUninitialize when done.

CoUninitialize();

Performance Monitoring

Windows offers tools to keep track of how well applications are running.

Using Performance Monitors

Making and Using Performance Counters: Use Performance Counter APIs to keep track of system and application data.

PDH_HQUERY hQuery;

PDH_HCOUNTER hCounter;

PdhOpenQuery(NULL, 0, &hQuery);

PdhAddCounter(hQuery, TEXT("\\Processor(_Total)\\% Processor Time"), 0, &hCounter);

PdhCollectQueryData(hQuery);

Windows API Extensions

Windows 10 UWP: For creating new apps using the Universal Windows Platform (UWP).

Windows API Functions: Use extra functions from the Windows API for special tasks.

Conclusion

In this chapter, we looked at more complex ideas in Windows programming. We talked about how programs can talk to each other (IPC), how to manage memory, advanced ways to keep things in sync, and using special Windows features. Learning these complex subjects will help you create advanced apps that work better, faster, and have more features.

# Chapter 9

## Debugging and Testing

Debugging and testing are important steps in making software. Debugging means finding and fixing mistakes in computer code, and testing checks if the software works as it should and meets what it's supposed to do. In Windows programming, there are many tools and methods that help developers check and test their applications properly.

Main Ideas

Debugging: Finding and fixing mistakes in computer code.

Testing: Checking software to make sure it works like it should.

Debugging Tools: Tools used to find and fix mistakes in programs.

Testing Methods: Ways to check if software works correctly and performs well.

Debugging Techniques

Using the Visual Studio Debugger

Visual Studio has a strong built-in tool that helps developers find and fix problems in their code.

Setting Breakpoints

Breakpoints let you stop the program at a certain line of code so you can check what's happening in the application.

To add breakpoints, click in the space next to a line of code or press F9.

Walking Through Code

When you reach a breakpoint, you can go through the code step by step to see what it does.

Step Into (F11): Use this to go through the code one line at a time to find problems.

Step Over (F10): Run the current line and go to the next one.

Step Out (Shift+F11): Leave the current function and go back to where it was called from.

Examining at Variables

Use the Locals and Watch windows to look at variables and what their values are.

Locals Window: Displays all local variables and what they are set to.

Watch Window: Add certain variables or expressions to keep an eye on their values.

Using the immediate Window

The Immediate Window lets you run commands and check expressions while you are fixing problems in your code.

? variableName  // Displays the value of variableName

Using Debugging APIs

Windows has tools called debugging APIs that help developers find and fix problems in their programs.

Debugging Tools

OutputDebugString: Sends a message to the debugger.

OutputDebugString(TEXT("Debug message"));

DebugBreak: Forces a breakpoint in the code.

DebugBreak();

Testing Techniques

Unit Testing

Unit testing means checking single parts or functions of a program on their own to make sure they function properly.

Using Microsoft Unit Test Tools

Visual Studio allows you to do unit testing using the Microsoft Unit Testing Framework.

Making Test Projects: Add a new test project to your solution.

Creating Test Methods: Use tags like [TestMethod] to set up test cases.

[TestMethod]

public void TestMethod1() {

Assert.AreEqual(expectedValue, actualValue);

}

Integration Testing

Integration testing checks if the different parts of the application work well together.

Testing Interfaces: Make sure how different parts and outside systems work together.

Creating Real-Life Examples: Use test cases that copy real user situations.

System Testing

System testing checks the whole software system to make sure everything works together.

End-to-End Testing: Make sure the app works well from the beginning to the end.

Testing Against Requirements: Check that the software meets all the listed needs.

Performance Testing

Performance testing checks how well the application works in different situations.

Load Testing: Find out how well the application works when it has a lot of users or tasks at once.

Stress Testing: Check how the application works in very tough situations.

Using Performance Testing Tools

Visual Studio Load Test: Pretend many users are using the program at the same time and check how well it works.

Use tools like JMeter or LoadRunner for more complex situations.

User Acceptance Testing (UAT)

UAT makes sure that the software works well for the people who will use it.

Getting Users Involved: Let real users try the app in everyday situations.

Getting Feedback: Ask for opinions and fix any problems or worries.

Debugging Multithreaded Applications

Challenges in Multithreaded Debugging

It can be hard to fix problems in multithreaded applications because they run at the same time and can have issues working together.

Identifying Deadlocks

Deadlocks happen when two or more threads are stuck, waiting forever for each other to free up resources.

Checking Thread States: Use tools to find deadlocks.

Debugging Tools: Use Visual Studio's tool to see how threads are working.

Synchronization Issues

Synchronization problems can cause race conditions, where multiple threads try to use shared resources at the same time in the wrong way.

Checking Locks: Make sure that locks and synchronization tools are used properly.

Finding Race Conditions: Use tools and methods to spot and fix race conditions.

Debugging with Logging

Logging means keeping track of information while a program is running. This helps to find problems and see how the program works.

Setting Up Logging

Using the Windows Event Log: Record messages to the Windows Event Log with the EventLog class.

EventLog.WriteEntry("Application", "Log message", EventLogEntryType.Information);

File-Based Logging: Write logs to files for persistent storage.

using (StreamWriter writer = new StreamWriter("log.txt", true)) {

writer.WriteLine("Log message");

}

Analyzing Logs

Checking Log Files: Look at the log files for error messages and trends.

Using Log Analysis Tools: Use tools to look at and display log data.

Automated Testing

Benefits of Automated Testing

Automated testing makes testing faster and makes sure the tests are done the same way every time.

Getting Automated Tests Ready

Making Automated Test Sets: Build automated test sets using tools like NUnit or MSTest.

Continuous Integration: Add automatic tests to the building process using tools like Jenkins or Azure DevOps.

Implementing Automated Test Cases

Creating Test Scripts: Make scripts to automate testing tasks.

Running Tests: Automatically check for issues while developing or launching.

Debugging and Testing Best Practices

Debugging Best Practices

Reproduce Problems Regularly: Make sure you can recreate the problems every time so you can fix them properly.

Find Problems: Break down the issues by focusing on the specific code or part that is causing the problem.

Write down what you find: Keep clear notes of problems and their answers for later use.

Testing Best Practices

Test Early and Often: Begin testing at the start of the project and keep testing regularly.

Use real test data: Make sure the test data looks like real-life situations.

Try to automate tasks whenever you can. This will help you save time and make fewer mistakes.

Conclusion

In this chapter, we talked about ways to fix problems and test software that are important for making dependable and good-quality Windows apps. We looked into using Visual Studio's debugger, creating small tests and combined tests, fixing issues with multiple threads, and using logging and automated testing. Following good methods for finding and fixing problems, as well as testing, will help you create strong apps that work well and satisfy users.

# Chapter 10

## Deployment and Distribution

Deployment and distribution are important parts of making software. They involve getting the software to users and handling its setup and updates. Good deployment strategies make sure that applications are set up correctly and easily on users' computers, while distribution strategies decide how the software gets to the people who need it. This chapter looks at different ways to set up and share Windows applications effectively.

Main Ideas

Deployment: The process of putting software on users' computers and setting it up.

Distribution: The way software is provided to users.

Installation Packages: Groups that have the app and everything needed to install it.

Update Mechanisms: Ways to give updates and fixes to software.

Deployment Strategies

Installation Packages: How to Set Things Up

Installation packages are complete collections that have everything needed to set up an app.

Different Types of Installation Packages

MSI (Microsoft Installer): A standard for making installation packages on Windows.

xml

<Package Id="MyApp" Manufacturer="MyCompany" UpgradeCode="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX">

<Product Id="*" Name="MyApp" Language="1033" Version="1.0.0.0" UpgradeCode="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX">

<Package InstallerVersion="500" Compressed="yes" />

</Product>

</Package>

EXE Installers: Files that start the installation process.

Making MSI Packages

Use tools like WiX to make MSI packages.

<Product Id="*" Name="MyApp" Language="1033" Version="1.0.0.0" Manufacturer="MyCompany" UpgradeCode="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX">

<Package InstallerVersion="500" Compressed="yes" />

<Media Id="1" Cabinet="product.cab" DiskId="1" />

<Feature Id="ProductFeature" Title="MyApp" Level="1">

<ComponentGroupRef Id="ProductComponents" />

</Feature>

</Product>

Making EXE Installers

You can use tools like Inno Setup or NSIS (Nullsoft Scriptable Install System) to make EXE installer files.

OutFile "MyAppInstaller.exe"

InstallDir "$PROGRAMFILES\MyApp"

Section

SetOutPath "$INSTDIR"

File "MyApp.exe"

SectionEnd

ClickOnce Deployment

ClickOnce is a Microsoft tool that makes it easy to install Windows applications without needing much input from users.

Benefits of ClickOnce

Easy Installation: Users can install apps with just one click.

Automatic Updates: Apps can be updated by themselves.

Setting Up ClickOnce Deployment

Publishing: Use Visual Studio's ClickOnce publish tool to publish the application.

Deployment: Users download the app from a website link or a network folder.

Windows Store Deployment

Starting with Windows 8, apps can be shared through the Microsoft Store.

Packaging for the Store

App Packages: Use Visual Studio to make an AppX package.

<Package

xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"

xmlns:mp="http://schemas.microsoft.com/appx/manifest/phone/windows10"

xmlns:windows="http://schemas.microsoft.com/appx/manifest/windows10"

xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10">

<Identity Name="MyApp" Publisher="CN=MyCompany" Version="1.0.0.0" />

</Package>

Submission: Send the package to the Microsoft Store using the Partner Center.

Distribution Strategies

Direct Distribution

Direct distribution means providing the software so people can download it or get a physical copy.

Ways of Direct Selling

Website Download: Put the installation file on a website so users can download it.

<a href="http://example.com/MyAppInstaller.exe">Download MyApp</a>

Physical Media: Share software using CDs, DVDs, or USB drives.

Distribution via Software Repositories

Software repositories are places where you can find, share, and update software easily.

Examples of Storage Places

Package Managers: Tools like Chocolatey or Windows Package Manager (winget) help to install and manage software.

winget install MyApp

Enterprise Repositories: Use internal storage spaces to share software within a company.

Automated Software Deployment

Automated deployment tools make it easier to install and update software on different computers.

Tools for Automatic Setup

Microsoft Endpoint Manager: A tool for managing installations in big businesses.

SCCM (System Center Configuration Manager): For distributing software on a large scale.

Managing Updates and Patches

Update Mechanisms

Keeping updates in check makes sure users get new features and fixes for problems.

Different Kinds of Updates

Patch Updates: Small changes that fix specific problems.

Feature Updates: Big changes that add new functions.

Putting in Place Update Processes

Automatic Updates: Use Windows Update or other services to get updates automatically.

<PackageFamilyName>MyApp_1.0.0.0_x64__8wekyb3d8bbwe</PackageFamilyName>

<Dependencies>

<PackageDependency Name="Microsoft.NET.Core.Runtime.2.1" MinVersion="2.1.0.0" />

</Dependencies>

User-Started Updates: Let users choose to check for and install updates themselves.

Handling Versioning

Using clear version names helps keep track of updates and ensures everything works well together.

Semantic Versioning: Use version numbers like Major. MinorPatch

xml

<Version>1.0.0</Version>

Version Control: Keep track of changes and handle different updates using tools like Git.

Ensuring Successful Deployment

Pre-Deployment Testing

Testing before launching helps make sure that the setup and the way the app works are right.

Different Kinds of Testing Before Deployment

Installation Testing: Check that the installation works correctly on different systems.

Compatibility Testing: Make sure it works well with different operating systems and setups.

Monitoring Post-Deployment

After launching the app, keep an eye on it to make sure it works properly and fix any problems that come up.

Tools for Watching or Checking

Application Performance Monitoring (APM): Tools such as New Relic or AppDynamics help you keep an eye on how well your application is working.

Error Reporting: Set up ways to find and study problems that happen while the program is running.

User Support

Helping users gives them answers and fixes problems after the system is set up.

Help Desks: Create a help desk or support team to help users.

Documentation: Create detailed guides and frequently asked questions (FAQs) for users.

Best Practices for Deployment and Distribution

Deployment Best Practices

Use automation tools to make processes easier and cut down on mistakes.

Check Carefully: Make sure to test the installation process and how the application works very well.

Give simple steps: Provide easy-to-follow steps for setting up and adjusting.

Distribution Best Practices

Pick the best ways to deliver your message so it reaches the people you want to reach.

Check and Update: Keep an eye on the distribution process and share updates when necessary.

Talk to users: Ask for their opinions and quickly help with any problems they have.

Conclusion

In this chapter, we looked at the methods and tips for putting Windows applications into use and sharing them. We talked about different ways to make installation packages, install software, manage updates, and ensure everything runs smoothly during the setup. By doing these things, you can successfully provide your software to users, keep it in good shape, and fix any problems that come up.