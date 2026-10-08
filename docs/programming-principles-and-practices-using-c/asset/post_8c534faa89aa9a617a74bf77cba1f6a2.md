
- Graphics are a fertile source of design examples. It is actually hard to design and implement a good graphics and GUI library. Graphics are a very rich source of concrete and practical examples of design decisions and design techniques. Some of the most useful techniques for designing classes, designing functions, separating software into layers (of abstraction), and constructing libraries can be illustrated with a relatively small amount of graphics and GUI code.

- Graphics provide a good introduction to what is commonly called object-oriented programming and the language features that support it. Despite rumors to the contrary, object-oriented programming wasn’t invented to be able to do graphics (see Chapter 22), but it was soon applied to that, and graphics provide some of the most accessible examples of object-oriented designs.

- Some of the key graphics concepts are nontrivial. So they are worth teaching, rather than leaving it to your own initiative (and patience) to seek out information. If we did not show how graphics and GUI were done, you might consider them “magic,” thus violating one of the fundamental aims of this book.

## 12.2 A display model

The iostream library is oriented toward reading and writing streams of characters as they might appear in a list of numeric values or a book. The only direct supports for the notion of graphical position are the newline and tab characters. You can embed notions of color and two-dimensional positions, etc. in a one-dimensional stream of characters. That’s what layout (typesetting, “markup”) languages such as Troff, TeX, Word, HTML, and XML (and their associated graphical packages) do. For example:

```html
<h2>
Organization
</h2>
This list is organized in three parts:
<ul>
<li><b>Proposals</b>, numbered EPddd, ...
<li><b>Issues</b>, numbered Edddd, ...
<li><b>Suggestions</b>, numbered ESddd, ...
</ul>
<p>We try to . . .
</p>
```

This is a piece of HTML, specifying a header (<h2> . . . </h2>), a list (<ul> . . . </ul>) with list items (<li> . . . </li>), and a paragraph (<p>). We left out most of the actual text because it is irrelevant here. The point is that you can express layout notions in plain text, but the connection between the characters written and what appears on the screen is indirect, governed by a program that interprets those “markup” commands. Such techniques are fundamentally simple and immensely useful (just about everything you read has been produced using them), but they also have their limitations.

In this chapter and the next four, we present an alternative: a notion of graphics and of graphical user interfaces that is directly aimed at a computer screen. The fundamental concepts are inherently graphical (and two-dimensional, adapted to the rectangular area of a computer screen), such as coordinates, lines, rectangles, and circles. The aim from a programming point of view is a direct correspondence between the objects in memory and the images on the screen.

The basic model is as follows: We compose objects with basic objects provided by a graphics system, such as lines. We “attach” these graphics objects to a window object, representing our physical screen. A program that we can think of as the display itself, as “a display engine,” as “our graphics library,” as “the GUI library,” or even (humorously) as “the small gnome writing on the back of the screen,” then takes the objects we have attached to our window and draws them on the screen:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_446_0.png)

The “display engine” draws lines on the screen, places strings of text on the screen, colors areas of the screen, etc. For simplicity, we’ll use the phrase “our GUI library” or even “the system” for the display engine even though our GUI library does much more than just drawing the objects. In the same way that our code lets the GUI library do most of the work for us, the GUI library delegates much of its work to the operating system.

## 12.3 A first example

Our job is to define classes from which we can make objects that we want to see on the screen. For example, we might want to draw a graph as a series of connected lines. Here is a small program presenting a very simple version of that:

```cpp
#include "Simple_window.h"   // get access to our window library
#include "Graph.h"               // get access to our graphics library facilities

int main()
{
   using namespace Graph_lib;   // our graphics facilities are in Graph_lib
   Point tl {100,100};          // to become top left corner of window
   Simple_window win {tl,600,400,"Canvas"};   // make a simple window
   Polygon poly;                // make a shape (a polygon)
   poly.add(Point{300,200});    // add a point
   poly.add(Point{350,100});    // add another point
   poly.add(Point{400,200});    // add a third point
   poly.set_color(Color::red);  // adjust properties of poly
   win.attach (poly);           // connect poly to the window
   win.wait_for_button();       // give control to the display engine
}
```

When we run this program, the screen looks something like this:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_447_0.png)

Let’s go through the program line by line to see what was done. First we include the headers for our graphics interface libraries:

```cpp
#include "Simple_window.h" // get access to our window library
#include "Graph.h" // get access to our graphics library facilities
```

Then, in **main()**, we start by telling the compiler that our graphics facilities are to be found in **Graph_lib**:

```cpp
using namespace Graph_lib; // our graphics facilities are in Graph_lib
```

Then, we define a point that we will use as the top left corner of our window:

```cpp
Point tl {100,100}; // to become top left corner of window
```

Next, we create a window on the screen:

```cpp
Simple_window win {tl,600,400,"Canvas"}; // make a simple window
```

We use a class representing a window in our **Graph_lib** interface library called **Simple_window**. The name of this particular **Simple_window** is **win**; that is, **win** is a variable of class **Simple_window**. The initializer list for **win** starts with the point to be used as the top left corner, **tl**, followed by **600** and **400**. Those are the width and height, respectively, of a window, as displayed on the screen, measured in pixels. We’ll explain in more detail later, but the main point here is that we specify a rectangle by giving its width and height. The string **Canvas** is used to label the window. If you look, you can see the word **Canvas** in the top left corner of the window’s frame.

Next, we put an object in the window:

```cpp
Polygon poly; // make a shape (a polygon)

poly.add(Point{300,200}); // add a point
poly.add(Point{350,100}); // add another point
poly.add(Point{400,200}); // add a third point
```

We define a polygon, **poly**, and then add points to it. In our graphics library, a **Polygon** starts empty and we can add as many points to it as we like. Since we added three points, we get a triangle. A point is simply a pair of values giving the x and y (horizontal and vertical) coordinates within a window.

Just to show off, we then color the lines of our polygon red:

```cpp
poly.set_color(Color::red); // adjust properties of poly
```

Finally, we attach **poly** to our window, **win**:

```cpp
win.attach(poly);        // connect poly to the window
```

If the program wasn't so fast, you would notice that so far nothing had happened to the screen: nothing at all. We created a window (an object of class **Simple\_window**, to be precise), created a polygon (called **poly**), painted that polygon red (**Color::red**), and attached it to the window (called **win**), but we have not yet asked for that window to be displayed on the screen. That's done by the final line of the program:

```cpp
win.wait_for_button();   // give control to the display engine
```

To get a GUI system to display objects on the screen, you have to give control to “the system.” Our **wait\_for\_button()** does that, and it also waits for you to “press” (“click”) the “Next” button of our **Simple\_window** before proceeding. This gives you a chance to look at the window before the program finishes and the window disappears. When you press the button, the program terminates, closing the window.

In isolation, our window looks like this:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_449_0.png)

You'll notice that we “cheated” a bit. Where did that button labeled “Next” come from? We built it into our **Simple\_window** class. In Chapter 16, we'll move from **Simple\_window** to “plain” **Window**, which has no potentially spurious facilities
