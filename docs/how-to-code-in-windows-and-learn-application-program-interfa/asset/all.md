![](Images/cover00050.jpeg)

Introduction

# Your First Window

Welcome to Create Your Own Window, a book that uses the C++ programming language alongside the Windows API. With this book, you will learn the syntax required to build your very first window. Step by step, you can move through the stages of creating a fully functional windows that you can see on your PC screen.

# The Window Example

By the end of this book you will be capable of writing code that builds a window and understanding it. The window you create will look the same or similar to this:

![](Images/image00048.jpeg)

The first stage that this book introduces you to is to make sure you have the programming experience required to understand the syntax needed for a window. To understand everything that is shown and explained in this book, you will need to understand the basics of C++ and some of Object-Oriented Programming. This includes understanding concepts such as:

*   Variables.
*   Classes.
*   Inheritance.
*   Functions.
*   Passing values by reference and pointers.
*   Loops.
*   Statements.

Now, let’s begin by looking at the code of a simple window called The Message Box.

## Conventions & Practices

There is no doubt about it, the Windows API is a difficult to learn, but very rewarding. I mean, you get to build your own Windows. You get to become Bill Gates – without the millions of dollars obviously.

Throughout the pages of this book you will discover three boxes that have special information that focuses on programming techniques. The following illustrates the boxes that are spread out amongst the numerous pages.

Programming Knowledge

These boxes are filled with necessary information, which can help to enhance your knowledge of the C++ language.

Programming Technical Talk

These boxes are for the “geek” inside us, which desires to learn and absorb the information of in-depth C++ concepts.

Programming Warnings

These boxes point out dangerous areas that a programmer should be aware of before attempting to code something, via a certain programming concept.

# Chapter 1: The MessageBox Window

## Your First Window: The Message Box

Do you remember the first program you created? If you read book 1 of C++ Programming Simplified, written by my good self, then your first program would probably have been The Hello Programmer application. Well, I hope you did and to begin your journey with Windows programming, we are going to the Hello Programmer application and converting it to work with the Windows API.

Of course, creating a Windows version of the Hello Programmer application is much more than just the simple program you see here.

#include <iostream>

using namespace std;

int main()

{

    cout << "Hello Programmer!" << endl;

    return 0;

}

Looks pretty easy doesn’t it? Well, remember those days when programming in C++ was easy, although not as rewarding as what you’re about to jump into – not literally. Don’t worry, I am not going to leave you without a flair gun stood in a sinking boat. Each stage we go through I’ll be there to hold your hand – again not literally  - and talk you through every part slowly. So, let’s us begin with the first step of building the MessageBox program.

### Step 1: the <Windows.h> File

Before we create our Windows MessageBox, the initial line of code required is a pre-processor directive that includes the Windows.h header file. This is probably easy for any intermediate or advanced C++ programmer. However, I have written the line below.

#include <Windows.h>

By including the Windows header file, it allows the program to utilize everything required to construct a program, which operates in Windows.

Warning: Windows Header File

Depending on the compiler you are using to build your window shall depend on how its like the Windows header file to be included.

Most compiler will accept #include <Windows>.

However, in some case, like Code::Blocks, you will need to include a .h after the Windows. As such:

#include <Windows.h>

### Step 2: Open With The WinMain function

Stated earlier, when creating a Windows application the main function, used for Windows console programs, is replaced with the WinMain function. Like the main function, WinMain is the beginning of any Windows application created. Therefore, when coding a programs using the Windows API, the initial line inside the WinMain function is the beginning of the program.

The WinMain function also has several parameters that are used in a Windows program. The syntax below reveals the prototype for the WinMain function.

WINAPI int WinMain(HINSTANCE hInstance,

                   HINSTANCE hPrevInstance,

                   LPSTR cmdLine, int cmdShow);

Warning: The WinMain Is Not main

Developing a console window using main and building a window by opening with WinMain is totally different. One of the only similarity’s it has is like main, WinMain is where the program begins.

Now, you might already be gapping at those parameters wondering what HINSTANCE and LPSTR mean. Put in a complex way, HINSTANCE is a handle to an instance. This means, to someone attempting Windows programming for the first time, that HINSTANCE is a type defined using typdef, which looks for the address in memory it is being utilized for. Therefore, it iss like any data type, which can define a variable. Later on we will look at the different types the Windows API has and uses in its programming. As for the example above, HINSTANCE creates a variable called hInstance and another called hPrevInstance. The second variable is basically ignored and not used in todays Windows programming, unless you wish to create a program for an older version of Windows, like Windows 95.

Next we have LPSTR, which is another type created for the Windows API. It stands for Long Pointer to String. In short terms, it is a pointer type that looks for a string variable. This means that when this type is used it requires to point to a string variable. Once we move onto creating the message box object, this will come into full practise.

The last parameter is a classic int variable, which means it looks for a whole number. Again, we will see how this works with the message box object we shall create next.

Once the WinMain function is complete, it opens up with brackets and we can start to create our message box. To create a message box we shall use the message box function known as MessageBox(). Like the WinMain function, the MessageBox object uses parameters to determine what information the message box will have in the program.

To create the Hello Programmer message box follow the syntax:

MessageBox(0,“Hello Programmer, nice to see you again!”,“Welcome Back!”, MB_OK);

On the MSDN website, it displays the syntax for the MessageBox object as the following.

int WINAPI MessageBox(

  _In_opt_  HWND hWnd,

  _In_opt_  LPCTSTR lpText,

  _In_opt_  LPCTSTR lpCaption,

  _In_      UINT uType

);

Let’s go through this before we end the program.

#### HWND hWnd

The MessageBox function opens with a HWND (handle to window/window handle) object. A HWND object is another typedef that equals to an int variable. This type looks for a whole number. This is why in our small example the value of the HWND is set to 0, therefore telling the compiler there is no HWND for the MessageBox to use.

#### LPCTSTR lpText

Next, a LPSTR type is required. The first LPSTR allocates the message inside the Message Box. This is important, as if you get these mixed up you’ll have the wrong piece of string in the wrong place. As you can see, the first variable in the example is called lpText, signifying it is used for the message in the dialog box.

#### LPCTSTR lpCaption

The second LPSTR is to fill the caption of the dialog box. The caption is the header file of the dialog box.

As you can see from the image above, the caption in the message dialog box reads“Message Box”and the message itself reads“Hello Programmer!.

#### UINT uType

The last part of the MessageBox object parameters is an unsigned integer type. Although, you do not write a number in the parameter, but instead a typedef name that is equal to a value. In this case, the name is MB_OK. What this does is allows for the message box to have an OK button attached to it.

Knowledge: The unsigned Means Not Below 0

Remember unsigned states that values cannot go below the rate of 0.

Knowledge: The OK Window

Whether it is buttons, scroll bars or text boxes, they are all known as windows. This means that the OK button in the example is also a window

Once the MessageBox function is wrote out, we can end the program with a return value of 0 and use a closing bracket.

![](Images/image00049.jpeg)

This is the end product of the MessageBox program. I know it doesn’t look much, but hey, you have just made your first ever window. That is correct. Even a small block on the screen like this is a window.

# Chapter 2: Creating A Window

## Programming The Main Window

In the previous example you created your very own window application. Even though it was only a message dialog box, it used the basic fundamentals every windows application is required to have.

Now, we are going to create a full screen window. It is a simple blank window with a white background.  A basic window averages around 70-80 lines of code.

Well, what is the To begin with, you need to initialize the window and then create the window behind setting a loop.

### Step 1: Window Class

After coding the Windows.h header file and opening the WinMain function, the initial step to creating a window is to allocate it a class called a Windows class.

#### WNDCLASSEX

The following syntax is required to create a windows class.

WNDCLASSEX <class name>;

WNDCLASSEX parentWindow;

Once the window class is declared, then you can start to define it by filling in the specifications of its parameters.

Below is a list of the parameters that need attending to before moving onto the next stage.

| Parameter | Description |
| cbClsExtra | Determines the amount of reserved bytes required for the Windows Class. Normally, this is set to NULL. |
| cbSize | Sets the byte size of the Windows Class. |
| cbWndExtra | Determines the amount of reserved bytes required for the Window. Normally, this is set to NULL. |
| hbrBackground | Set the type of brush for drawing and colouring the window. It can alter the colour of the window. |
| hCursor | Set the cursor type used in the window. If set to NULL, then the default cursor will be used. |
| hIcon | Sets the original icon used for the window. This is the icon seen in the taskbar. If set to NULL, then the default icon will be used. |
| hIconSm | Set the small sized icon (seen in the Windows tray). If set to NULL, then the default icon will be used. |
| hInstance | Set the handle name of the instance that the Window uses. |
| lpszClassName | Set the name of the Windows class name between double quotes. |
| lpfnWndProc | Set the name found in the WinProc function. |
| lpszMenuName | Set the name of the menu that the window has. If the window has no menu then set to NULL. |
| style | Set the style (shape) of the window. |

Once all of these are filled out as shown below, the next step is to make sure the window is registered in memory.

       prWnd.cbClsExtra = 0;

       prWnd.cbSize = sizeof( WNDCLASSEX);

       prWnd.cbWndExtra = 0;

       prWnd.hbrBackground = ( HBRUSH)( COLOR_WINDOW+1);

       prWnd.hCursor = LoadCursor(hInst , IDC_ARROW );

       prWnd.hIcon = NULL;

       prWnd.hIconSm = NULL;

       prWnd.hInstance = hInst;

       prWnd.lpfnWndProc = ( WNDPROC)WndProc;

       prWnd.lpszClassName = "DirectX Project";

       prWnd.lpszMenuName = NULL;

       prWnd.style = CS_HREDRAW | CS_VREDRAW ;

### Step 2: Register the Windows Class

This part is simple, and requires only one line of code. First you write RegisterClassEx then in brackets () you reference the windows class you have just made. In this case it would look like the following.

#### RegisterClassEx

RegisterClassEx(&parentWindow);

There. Simple.

### Step 3: Create The Window

Now that you have the window registered in memory for the computer to use, you have to create its foundations. Don’t get this confused with creating the windows class, as now you are forming the visual aspect of the window instead of telling the compiler what the window boarder and how the window should act.

To begin to create a window you first have to use the handle variable (normally hWnd) and incorporate the CreateWindow function into the handle. The reason for this is due to the hWnd acting like a hook for holding the window up on the desktop when it is ran on the computer. Without a handle, the window would not have anything to grapple onto when trying to load.

Once the hWnd is written an assignment operator is used and then you place the CreateWindow function in along with its lists of parameters.  I will take you through the parameters now.

| Parameter | Description |
| LPSTR | The first LPSTR looks for the name of the class you set in the windows class. |
| LPSTR | The second LPSTR looks for the name of the window caption. |
| DWORD | This sets how the window will be displayed on the screen. |
| int | The following is the X position of where the window will be once it is open on the desktop. |
| int | The following is the Y position of where the window will be once it is open on the desktop. |
| int | The following is the width of the window. |
| int | The following is the height of the window. |
| HWND | This is to set whether the window has a parent window in it hierarchy. If the window is the main window then this is set to NULL. |
| HMENU | This is to set whether the window has a handle to a menu. If the window his no menu then this is set to NULL. |
| HINSTANCE | This looks for the handle to the instance of the window. |
| LPVOID | This is pointer to value used by the window to determine where it requires to use to create a certain type of structure. For a basic window this is set to NULL. |

#### CreateWindow(...)

There is all the parameters and this is how they may look for your window.

hWnd = CreateWindow("My First Window" ,

                                      "My Main Window",

                                      WS_OVERLAPPEDWINDOW | WS_EX_TOPMOST | WS_VISIBLE,

                                      400, 400,

                                      800, 600,

                                      NULL, NULL,

                                      hInstance, NULL);

### Step 4: Show & Update The Window

Next, it is now time to tell the compiler how it will display the window. This is not how it will look but to tell it what handle to use to show and then update the window whenever a new event is created.

Technical Talk: What is a Windows event?

A Window event is anything that happens in the window. Whether that is a mouse click, a menu being open or the window resizing, they are all events and the compiler requires to be told when one happens so it update the window through the UpdateWindow function.

#### ShowWindow(…)

First we need to show the window before we can tell the compiler it needs updating. To do this the ShowWindow function is iniitated along with a set of parameters to tell the compiler what handle to use and the concept of how the handle is to be used.

ShowWindow(hWnd, SW_SHOW);

We know that that hWnd is a handle to the window. But the SW_SHOW is an object type that tells the show window that after grabbing the handle it then has to utilise it to show the window.

Looking at SW_SHOW we can easily tell that the SW stands for Show Window. What it really does is initialise the window and tells it to show it to the width, length and position dictated by the windows class.

### Step 5: Translate & Update

#### MSG

The final aspect that is required in the WinMain function is to create a MSG variable, which will be used to interrupt integer values for the window to interpret. To begin with a MSG variable needs to be created. The type definition of MSG is a simple int variable.

The syntax to create a MSG variable is rather like any other type of variable, although, instead of a built-in type being written MSG replaces it.

MSG message;

#### ZeroMemory(…)

Next the ZeroMemoryfunction is used to determine that its parameters are allocated a NULL value before being used. The reason for this is due to that you don’t want a variable’s data to be unnecessary wiped.

The syntax for the ZeroMemory function is as follows.

ZeroMemory(message, &message);

As you can see, it uses the message variable and references it to see if it has any data stored in it.

#### while Loop

The next stage is to create a loop that always stays true until the window is shut down, thus, it returns the value of 0.

The loop is of the while loop method, or you can write it as a do while loop. These are two easiest loops to write for this stage in programming the window.

while (true) {

   // windows functions

}

do

{

   // windows functions

} while (true);

If you wanted to write this as a for loop than the following syntax will work.

bool wndEvent = true;

dor (wndEvent = true; wndEvent = false; ;)

{

   // windows functions

}

Do you see how much more there is to write with the for loop when coding this piece for a window? It may not seem like a lot more, but it is still an awkward method.

Now that the loop is done (Ill be using a while loop), we can now move onto the two window functions required for translating and dispatching them.

#### TranslateMessage(…)

First we your window will require to take the message and translate it to something it can understand. Thus, we use a function called TranslateMessage. This function takes only one parameter and it is the message variable. So, it will look like this:

TranslateMessage(&message);

#### DispatchMessage(…)

Following its translation, the message is then sent by reference to the DispatchMessage function, which sends it to the computer to achieve its task.

Looking at the Dispatch function, we can see that it similar to the TranslateMessage.

DispatchMessage(&message);

Look at the while loop in its fullest then, this is how it looks with the two Windows functions.

while (true) {

   TranslateMessage(&message);

   DispatchMessage(&message);

}

### Step 6: The Event Loop

#### CallBack Function

The last part of the window is to create the callback function, which will hold the event loops. Even though it is called an Event Loop, what we are going to create is a switch statement that decides on an action to approach depending on the value given.

To start the callback function we create the function heading. The syntax for the callbackfunction may look strange at first but each keyword used I’ll explain in this section.

Let us look at the function first.

LRESULT CALLBACK WndProc(HWND hWnd, UINT msg, WPARAM wParam, LPARAM lParam)

{

   // statements

}

Of course, the switch statement resides inside the callback function. First, before we get into the function, we will look at each keyword in the function heading.

| Keyword | Description |
| LRESULT | The LRESULT is the beginning of the callback function. |
| CALLBACK | The CALLBACK is a typdef that is like a return statement and tells the compiler that the results from the functions needs to affect the whole window. |
| WndProc | The WndProc is the title of the opening of the function. |
| HWND | We have already seen HWND. The HWND keyword is a handle to a window. |
| UINT | We have already seen UINT as an unsigned integer. This will hold values for the messages passed into the switch statement. |
| WPARAM | WPARM is the Wide Parameter. Depending on the message the window needs will depend on whether if WPARAM or LPARAM is used. |
| LPARAM | The LPARAM is the Long Parameter. Depending on the message the window needs will depend on whether if WPARAM or LPARAM is used. |

#### switch Statement

Delving into the function, we first encounter a switch statement with the value of whatever the variable of msg holds. First, we will look at the switch statement.

switch (msg)             

{

   case 1: WM_Destroy

   PostQuitWindow(0);

}

The switch statement takes the msg variable and depending on the value it receives chooses from the cases it have to choose from.

In the case of this switch statement example, there is only one option to choose from..

But for now, we are going to look at WM_DESTROY. This type is a call to the window shutting down. The PostQuitWindow parameter value is 0, which makes the program shut down when the case is initialised.

This is all there is to creating a simple window. The full coding of the window program is posted on the next page.

### Step 7: Adopting the Basic Window with OOP

#### Building A BasicWindow Class

Now we have seen how a basic window is created, it is time to start manipulating it using OOP. First we are going to create a class to store all the data required for the window.

First, let us start off with the basics.

class BasicWindow {

public:

API int WinMain(HINSTANCE, HINSTANCE, LPSTR, int);

LRESULT CALLBACK WndProc(HWND, UINT, WPARAM, LPARAM);

protected:

HWND hWnd;

HINSTANCE hInstance;

};

For a start having HWND hWnd in the class will wipe out the need for a global HWND variable. This gives the appearance of clearer code straight away.

Next, we have the two functions of the WinMain and also of the WndProc. Again, this makes your code cleaner as you are declaring the functions in the class.

To use these objects and data methods, you have to add to your code the name of the class along with the dot operator before the data methods.

# Chapter 3: Putting The Window Together

## The Final Product

This is the final part of the book. Here we are going to put everything we have learnt together, which will build the window from the first few pages.

Here is the code for the window in full.

// HEADER FILES INCLUDED

#include <Windows.h>

// WINDOWS CLASS

class InWindows {

public:

        bool LoadWindow( HINSTANCE hInst);

private:

        HWND hWnd;

        HINSTANCE hInst;

};

LRESULT CALLBACK WndProc(HWND hWnd , UINT uMsg , WPARAM wParam , LPARAM lParam )

{

        // MESSAGE CENTER FOR WINDOW

        switch( uMsg)

       {

        case WM_DESTROY:

              PostQuitMessage(0);

               break;

       }

        return DefWindowProc(hWnd , uMsg , wParam , lParam );

}

bool InWindows ::LoadWindow(HINSTANCE hInst)

{

        InWindows CreateWin;

        WNDCLASSEX prWnd;

       prWnd.cbClsExtra = 0;

       prWnd.cbSize = sizeof( WNDCLASSEX);

       prWnd.cbWndExtra = 0;

       prWnd.hbrBackground = ( HBRUSH)( COLOR_WINDOW+1);

       prWnd.hCursor = LoadCursor(hInst , IDC_ARROW );

       prWnd.hIcon = NULL;

       prWnd.hIconSm = NULL;

       prWnd.hInstance = hInst;

       prWnd.lpfnWndProc = ( WNDPROC)WndProc;

       prWnd.lpszClassName = "DirectX Project";

       prWnd.lpszMenuName = NULL;

       prWnd.style = CS_HREDRAW | CS_VREDRAW ;

        RegisterClassEx(&prWnd);

       CreateWin.hWnd = CreateWindow("DirectX Project" ,

                                      "My Main Window",

                                      WS_OVERLAPPEDWINDOW | WS_EX_TOPMOST | WS_VISIBLE,

                                      400, 400,

                                      800, 600,

                                      NULL, NULL,

                                      hInst, NULL);

        if(!CreateWin.hWnd)

       {

               MessageBox(hWnd, "Window Creation Failed" , "Failed To Create Window", MB_OK);

               return false;

       }

       ShowWindow(hWnd, SW_SHOW);

       UpdateWindow(hWnd);

        return true;

}

// START OF WINMAIN

int WINAPI WinMain(HINSTANCE hInst , HINSTANCE hPrevInst , LPSTR lpCmdLine , int iCmdShow)

{

        InWindows theWindow; // WINDOW CLASS OBJECT

        if(!theWindow.LoadWindow( hInst ))

       {

               // IF PARENT WINDOW FAILS TO LOAD

               MessageBox(NULL , "Error Initializing Parent Window" , "Initialize Parent Window Failed", MB_OK);

               return false; // QUIT PROGRAM

       }

        MSG message;

        ZeroMemory(&message, sizeof (message));

        while( true )

       {

               if( PeekMessage(&message, NULL , 0,0,PM_REMOVE ))

              {

                     TranslateMessage(&message);

                     DispatchMessage(&message);

              }

       }

}

### Last Words

I would like to thank you for purchasing or borrowing this kindle book from the kindle store. I truly hope it has been extremely helpful in learning how to develop and program a Window. If you have any questions about the book then please e-mail me at [ltrobespierre@outlook.com](mailto:ltrobespierre@outlook.com).

Also, I would be eternally grateful if after reading this book you write a review on Amazon about how much you enjoyed or – heavens forbid – disliked this book.

If you discover any errors in this book, please e-mail at the above address with the problem, including the chapter number and section. Thank you.

Thank you again. I was a pleasure to write this book and I hope you had just as much desire from reading and learning the basics of the Windows API.

Once again,

Thank you!