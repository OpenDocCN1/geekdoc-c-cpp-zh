
Obviously, **Point** is a class with a constructor that takes a pair of integers and interprets them as an $(x, y)$ coordinate pair. We could have written

```cpp
Simple_window win {Point{100,100},600,400,"Canvas"};
```

However, we want to use the point (100,100) several times so it is more convenient to give it a symbolic name. The 600 is the width and 400 is the height of the window, and **Canvas** is the label we want put on the frame of the window.

To actually get the window drawn on the screen, we have to give control to the GUI system. We do this by calling **win.wait_for_button()** and the result is:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_455_0.png)

In the background of our window, we see a laptop screen (somewhat cleaned up for the occasion). For people who are curious about irrelevant details, we can tell you that I took the photo standing near the Picasso library in Antibes looking across the bay to Nice. The black console window partially hidden behind is the one running our program. Having a console window is somewhat ugly and unnecessary, but it has the advantage of giving us an effective way of killing our window if a partially debugged program gets into an infinite loop and refuses to go away. If you look carefully, you'll notice that we have the Microsoft C++ compiler running, but you could just as well have used some other compiler (such as Borland or GNU).

For the rest of the presentation we will eliminate the distractions around our window and just show that window by itself:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_456_0.png)

The actual size of the window (in inches) depends on the resolution of your screen. Some screens have bigger pixels than other screens.

### 12.7.3 Axis

An almost blank window isn’t very interesting, so we’d better add some information. What would we like to display? Just to remind you that graphics is not all fun and games, we will start with something serious and somewhat complicated: an axis. A graph without axes is usually a disgrace. You just don’t know what the data represents without axes. Maybe you explained it all in some accompanying text, but it is far safer to add axes; people often don’t read the explanation and often a nice graphical representation gets separated from its original context. So, a graph needs axes:

```cpp
Axis xa {Axis::x, Point(20,300), 280, 10, "x axis"};   // make an Axis
// an Axis is a kind of Shape
// Axis::x means horizontal
// starting at (20,300)
// 280 pixels long
// 10 “notches”
// label the axis “x axis”

win.attach(xa);                 // attach xa to the window, win
win.set_label("Canvas #2");     // relabel the window
win.wait_for_button();          // display!
```

The sequence of actions is: make the axis object, add it to the window, and finally display it:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_457_0.png)

We can see that an Axis::x is a horizontal line. We see the required number of “notches” (10) and the label “x axis.” Usually, the label will explain what the axis and the notches represent. Naturally, we chose to place the x axis somewhere near the bottom of the window. In real life, we’d represent the height and width by symbolic constants so that we could refer to “just above the bottom” as something like y_max-bottom_margin rather than by a “magic constant,” such as 300 (§4.3.1, §15.6.2).

To help identify our output we relabeled the screen to Canvas #2 using Window’s member function set_label().

Now, let’s add a y axis:

```cpp
Axis ya (Axis::y, Point{20,300}, 280, 10, "y axis");
ya.set_color(Color::cyan);           // choose a color
ya.label.set_color(Color::dark_red); // choose a color for the text
win.attach(ya);
win.set_label("Canvas #3");
win.wait_for_button();               // display!
```

Just to show off some facilities, we colored our $y$ axis cyan and our label dark red.

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_458_0.png)

We don't actually think that it is a good idea to use different colors for $x$ and $y$ axes. We just wanted to show you how you can set the color of a shape and of individual elements of a shape. Using lots of color is not necessarily a good idea. In particular, novices tend to use color with more enthusiasm than taste.

### 12.7.4 Graphing a function

What next? We now have a window with axes, so it seems a good idea to graph a function. We make a shape representing a sine function and attach it:

```cpp
Function sine {sin,0,100,Point(20,150),1000,50,50};    // sine curve
// plot sin() in the range [0:100] with (0,0) at (20,150)
// using 1000 points; scale x values *50, scale y values *50

win.attach(sine);
win.set_label("Canvas #4");
win.wait_for_button();
```

Here, the **Function** named **sine** will draw a sine curve using the standard library function **sin()** to generate values. We explain details about how to graph functions in §15.3. For now, just note that to graph a function we have to say where it starts (a **Point**) and for what set of input values we want to see it (a range), and we need to give some information about how to squeeze that information into our window (scaling):

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_459_0.png)

Note how the curve simply stops when it hits the edge of the window. Points drawn outside our window rectangle are simply ignored by the GUI system and never seen.

### 12.7.5 Polygons

A graphed function is an example of data presentation. We’ll see much more of that in Chapter 15. However, we can also draw different kinds of objects in a window: geometric shapes. We use geometric shapes for graphical illustrations, to indicate user interaction elements (such as buttons), and generally to make our presentations more interesting. A **Polygon** is characterized by a sequence of points, which the **Polygon** class connects by lines. The first line connects the first point to the second, the second line connects the second point to the third, and the last line connects the last point to the first:

```cpp
sine.set_color(Color::blue);    // we changed our mind about sine's color

Polygon poly;                      // a polygon; a Polygon is a kind of Shape
poly.add(Point(300,200));          // three points make a triangle
poly.add(Point(350,100));
poly.add(Point(400,200));

poly.set_color(Color::red);
poly.set_style(Line_style::dash);
win.attach(poly);
win.set_label("Canvas #5");
win.wait_for_button();
```

This time we change the color of the sine curve (*sine*) just to show how. Then, we add a triangle, just as in our first example from §12.3, as an example of a polygon. Again, we set a color, and finally, we set a style. The lines of a **Polygon** have a “style.” By default that is solid, but we can also make those lines dashed, dotted, etc. as needed (see §13.5). We get

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_460_0.png)

### 12.7.6 Rectangles

A screen is a rectangle, a window is a rectangle, and a piece of paper is a rectangle. In fact, an awful lot of the shapes in our modern world are rectangles (or at least rectangles with rounded corners). There is a reason for this: a rectangle is the simplest shape to deal with. For example, it’s easy to describe (top left corner plus width plus height, or top left corner plus bottom right corner, or whatever), it’s easy to tell whether a point is inside a rectangle or outside it, and it’s easy to get hardware to draw a rectangle of pixels fast.

So, most higher-level graphics libraries deal better with rectangles than with other closed shapes. Consequently, we provide **Rectangle** as a class separate from the **Polygon** class. A **Rectangle** is characterized by its top left corner plus a width and height:

```cpp
Rectangle r {Point{200,200}, 100, 50};    // top left corner, width, height
win.attach(r);
win.set_label("Canvas #6");
win.wait_for_button();
```

From that, we get

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_461_0.png)

Please note that making a polyline with four points in the right places is not enough to make a **Rectangle**. It is easy to make a **Closed_polyline** that looks like a **Rectangle** on the screen (you can even make an **Open_polyline** that looks just like a **Rectangle**); for example:

```cpp
Closed_polyline poly_rect;
poly_rect.add(Point{100,50});
poly_rect.add(Point{200,50});
poly_rect.add(Point{200,100});
poly_rect.add(Point{100,100});
win.attach(poly_rect);
```
