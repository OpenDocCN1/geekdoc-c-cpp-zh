
built in, and show how we can write our own code to control interaction with a window.

For the next three chapters, we’ll simply use that “Next” button to move from one “display” to the next when we want to display information in stages (“frame by frame”).

You are so used to the operating system putting a frame around each window that you might not have noticed it specifically. However, the pictures in this and the following chapters were produced on a Microsoft Windows system, so you get the usual three buttons on the top right “for free.” This can be useful: if your program gets in a real mess (as it surely will sometimes during debugging), you can kill it by hitting the X button. When you run your program on another system, a different frame will be added to fit that system’s conventions. Our only contribution to the frame is the label (here, Canvas).

## 12.4 Using a GUI library

In this book, we will not use the operating system’s graphical and GUI (graphical user interface) facilities directly. Doing so would limit our programs to run on a single operating system and would also force us to deal directly with a lot of messy details. As with text I/O, we’ll use a library to smooth over operating system differences, I/O device variations, etc. and to simplify our code. Unfortunately, C++ does not provide a standard GUI library the way it provides the standard stream I/O library, so we use one of the many available C++ and GUI libraries. So as not to tie you directly into one of those GUI libraries, and to save you from hitting the full complexity of a GUI library all at once, we use a set of simple interface classes that can be implemented in a couple of hundred lines of code for just about any GUI library.

The GUI toolkit that we are using (indirectly for now) is called FLTK (Fast Light Tool Kit, pronounced “full tick”) from www.fltk.org. Our code is portable wherever FLTK is used (Windows, Unix, Mac, Linux, etc.). Our interface classes can also be re-implemented using other toolkits, so code using them is potentially even more portable.

The programming model presented by our interface classes is far simpler than what common toolkits offer. For example, our complete graphics and GUI interface library is about 600 lines of C++ code, whereas the extremely terse FLTK documentation is about 1,000 pages. You can download from www.fltk.org, but we don’t recommend you do that just yet. You can do without that level of detail for a while. The general ideas presented in Chapters 12–16 can be used with any popular GUI toolkit. We will of course explain how our interface classes map to FLTK so that you will (eventually) see how you can use that (and similar toolkits) directly, if necessary.

We can illustrate the parts of our "graphics world" like this:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_451_0.png)

Our interface classes provide a simple and user-extensible basic notion of two-dimensional shapes with limited support for the use of color. To drive that, we present a simple notion of GUI based on "callback" functions triggered by the use of user-defined buttons, etc. on the screen (Chapter 16).

## 12.5 Coordinates

A computer screen is a rectangular area composed of pixels. A pixel is a tiny spot that can be given some color. The most common way of modeling a screen in a program is as a rectangle of pixels. Each pixel is identified by an $x$ (horizontal) coordinate and a $y$ (vertical) coordinate. The $x$ coordinates start with 0, indicating the leftmost pixel, and increase (toward the right) to the rightmost pixel. The $y$ coordinates start with 0, indicating the topmost pixel, and increase (toward the bottom) to the lowest pixel:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_451_1.png)

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_452_0.png)

Please note that y coordinates “grow downward.” Mathematicians, in particular, find this odd, but screens (and windows) come in many sizes, and the top left point is about all that they have in common.

The number of pixels available depends on the screen: 1024-by-768, 1280-by-1024, 1400-by-1050, and 1600-by-1200 are common screen sizes.

In the context of interacting with a computer using a screen, a window is a rectangular region of the screen devoted to some specific purpose and controlled by a program. A window is addressed exactly like a screen. Basically, we see a window as a small screen. For example, when we said

```
Simple_window win {11,600,400,"Canvas"};
```

we requested a rectangular area 600 pixels wide and 400 pixels high that we can address as 0-599 (left to right) and 0-399 (top to bottom). The area of a window that you can draw on is commonly referred to as a canvas. The 600-by-400 area refers to “the inside” of the window, that is, the area inside the system-provided frame; it does not include the space the system uses for the title bar; quit button, etc.

## 12.6 Shapes

Our basic toolbox for drawing on the screen consists of about a dozen classes:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_452_1.png)

An arrow indicates that the class pointing can be used where the class pointed to is required. For example, a **Polygon** can be used where a **Shape** is required; that is, a **Polygon** is a kind of **Shape**.

We will start out presenting and using

- **Simple_window, Window**
- **Shape, Text, Polygon, Line, Lines, Rectangle, Function**, etc.
- **Color, Line_style, Point**
- **Axis**

Later (Chapter 16), we’ll add GUI (user interaction) classes:

- **Button, In_box, Menu, etc.**

We could easily add many more classes (for some definition of “easy”), such as

- **Spline, Grid, Block_chart, Pie_chart, etc.**

However, defining or describing a complete GUI framework with all its facilities is beyond the scope of this book.

## 12.7 Using Shape primitives

In this section, we will walk you through some of the primitive facilities of our graphics library: Simple_window, Window, Shape, Text, Polygon, Line, Lines, Rectangle, Color, Line_style, Point, Axis. The aim is to give you a broad view of what you can do with those facilities, but not yet a detailed understanding of any of those classes. In the next chapters, we explore the design of each.

We will now walk through a simple program, explaining the code line by line and showing the effect of each on the screen. When you run the program you’ll see how the image changes as we add shapes to the window and modify existing shapes. Basically, we are “animating” the progress through the code by looking at the program as it is executed.

### 12.7.1 Graphics headers and main

First, we include the header files defining our interface to the graphics and GUI facilities:

```c++
#include "Window.h"    // a plain window
#include "Graph.h"
```

or

```c++
#include "Simple_window.h"    // if we want that "Next" button
#include "Graph.h"
```

As you probably guessed, Window.h contains the facilities related to windows and Graph.h the facilities related to drawing shapes (including text) into windows. These facilities are defined in the Graph_lib namespace. To simplify notation we use a namespace directive to make the names from Graph_lib directly available in our program:

```c++
using namespace Graph_lib;
```

As usual, `main()` contains the code we want to execute (directly or indirectly) and deals with exceptions:

```c++
int main ()
try
{
    // ... here is our code ...
}
catch(exception& e) {
    // some error reporting
    return 1;
}
catch(...) {
    // some more error reporting
    return 2;
}
```

For this `main()` to compile, we need to have `exception` defined. We get that if we include `std_lib_facilities.h` as usual, or we could start to deal directly with standard headers and include `<stdexcept>`.

### 12.7.2 An almost blank window

We will not discuss error handling here (see Chapter 5, in particular, §5.6.3) but go straight to the graphics within `main()`:

```c++
Point tl {100,100}; // top left corner of our window

Simple_window win {tl,600,400,"Canvas"};
// screen coordinate tl for top left corner
// window size(600*400)
// title: Canvas
win.wait_for_button(); // display!
```

This creates a `Simple_window`, that is, a window with a “Next” button, and displays it on the screen. Obviously, we need to have #included the header `Simple_window.h` rather than `Window.h` to get `Simple_window`. Here we are specific about where on the screen the window should go: its top left corner goes at `Point(100,100)`. That’s near, but not too near, the top left corner of the screen.
