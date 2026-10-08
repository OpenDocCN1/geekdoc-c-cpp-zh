
In this case, we ask the system to call one of our functions (a “callback function”) when the mouse button is clicked “on our button.” To do that we must:

- Define a button
- Get it displayed
- Define a function for the GUI to call
- Tell the GUI about that button and that function
- Wait for the GUI to call our function

Let’s do that. A button is part of a **Window**, so (in **Simple_window.h**) we define our class **Simple_window** to contain a member **next_button**:

```cpp
struct Simple_window : Graph_lib::Window {
    Simple_window(Point xy, int w, int h, const string& title);

    void wait_for_button(); // simple event loop
private:
    Button next_button; // the "Next" button
    bool button_pushed; // implementation detail

    static void cb_next(Address, Address); // callback for next_button
    void next(); // action to be done when next_button is pressed
};
```

Obviously, **Simple_window** is derived from **Graph_lib::Window**. All our windows must be derived directly or indirectly from **Graph_lib::Window** because it is the class that (through FLTK) connects our notion of a window with the system’s window implementation. For details of **Window**’s implementation, see §E.3.

Our button is initialized in **Simple_window**’s constructor:

```cpp
Simple_window::Simple_window(Point xy, int w, int h, const string& title)
    : Window(xy,w,h,title),
    next_button(Point{x_max()-70,0}, 70, 20, "Next", cb_next),
    button_pushed(false)
{
    attach(next_button);
}
```

Unsurprisingly, **Simple_window** passes its location (**xy**), size (**w,h**), and title (**title**) on to **Graph_lib**’s **Window** to deal with. Next, the constructor initializes **next_button** with a location (**Point{x_max()-70,0}**; that’s roughly the top right corner), a size (**(70,20)**), a label ("Next"), and a “callback” function (**cb_next**). The first four parameters exactly parallel what we do for a **Window**: we place a rectangular shape on the screen and label it.

Finally, we **attach()** our **next_button** to our **Simple_window**; that is, we tell the window that it must display the button in its position and make sure that the GUI system knows about it.

The **button_pushed** member is a pretty obscure implementation detail; we use it to keep track of whether the button has been pushed since last we executed **next()**. In fact, just about everything here is implementation details, and therefore declared *private*. Ignoring the implementation details, we see:

```cpp
struct Simple_window : Graph_lib::Window {
    Simple_window(Point xy, int w, int h, const string& title);

    void wait_for_button();   // simple event loop

    // ...
};
```

That is, a user can make a window and wait for its button to be pushed.

### 16.3.1 A callback function

The function **cb_next()** is the new and interesting bit here. This is the function that we want the GUI system to call when it detects a click on our button. Since we give the function to the GUI for the GUI to “call back to us,” it’s commonly called a *callback* function. We indicate **cb_next()**’s intended use with the prefix **cb_** for “callback.” That’s just to help us – no language or library requires naming convention. Obviously, we chose the name **cb_next** because it is to be the callback for our “Next” button. The definition of **cb_next** is an ugly piece of “boilerplate.”

Before showing that code, let’s consider what is going on here:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_588_0.png)

Our program runs on top of several “layers” of code. It uses our graphics library that we implement using the FLTK library, which is implemented using operating system facilities. In a system, there may be even more layers and sub-layers. Somehow, a click detected by the mouse’s device driver has to cause our function `cb_next()` to be called. We pass the address of `cb_next()` and the address of our `Simple_window` down through the layers of software; some code “down there” then calls `cb_next()` when the “Next” button is pressed.

The GUI system (and the operating system) can be used by programs written in a variety of languages, so it cannot impose some nice C++ style on all users. In particular, it does not know about our `Simple_window` class or our `Button` class. In fact, it doesn’t know about classes or member functions at all. The type required for a callback function is chosen so that it is usable from the lowest level of programming, including C and assembler. A callback function returns no value and takes two addresses as its arguments. We can declare a C++ member function that obeys those rules like this:

```cpp
static void cb_next(Address, Address); // callback for next_button
```

The keyword `static` is there to make sure that `cb_next()` can be called as an ordinary function, that is, not as a C++ member function invoked for a specific object. Having the system call a proper C++ member function would have been much nicer. However, the callback interface has to be usable from many languages, so this is what we get: a `static` member function. The `Address` arguments specify that `cb_next()` takes arguments that are addresses of “something in memory.” C++ references are unknown to most languages, so we can’t use those. The compiler isn’t told what the types of those “somethings” are. We are close to the hardware here and don’t get the usual help from the language. “The system” will invoke a callback function with the first argument being the address of the GUI entity (`Widget`) for which the callback was triggered. We won’t use that first argument, so we don’t bother to name it. The second argument is the address of the window containing that `Widget`; for `cb_next()`, that will be our `Simple_window`. We can state that information like this:

```cpp
void Simple_window::cb_next(Address, Address pw)
// call Simple_window::next() for the window located at pw
{
    reference_to<Simple_window>(pw).next();
}
```

The `reference_to<Simple_window>(pw)` tells the compiler that the address in `pw` is to be considered the address of a `Simple_window`; that is, we can use `reference_to<Simple_window>(pw)` as a reference to a `Simple_window`. In Chapters 17 and 18, we will return to the issue of addressing memory. In §E.1, we present the (by then, trivial) definition of **reference to**. For now, we are just glad that we finally obtained a reference to our **Simple_window** so that we can access our data and functions exactly as we like and are used to. Finally, we get out of this system-dependent code as quickly as possible by calling our member function **next()**.

We could have written all the code we wanted to execute in **cb_next()**, but we — like most good GUI programmers — prefer to keep messy low-level stuff separate from our nice user code, so we handle a callback with two functions:

- **cb_next()** simply maps the system conventions for a callback into a call to an ordinary member function (**next()**).
- **next()** does what we want done (without having to know about the messy conventions of callbacks).

The fundamental reason for using two functions here is the general principle that “a function should perform a single logical action”: **cb_next()** gets us out of the low-level system-dependent part of the system and **next()** performs our desired action. Whenever we want a callback (from “the system”) to one of our windows, we define such a pair of functions; for example, see §16.5–7. Before going further, let’s repeat what is going on here:

- We define our **Simple_window**.
- **Simple_window**’s constructor registers its **next_button** with the GUI system.
- When we click the image of **next_button** on the screen, the GUI calls **cb_next()**.
- **cb_next()** converts the low-level system information into a call of our member function **next()** for our window.
- **next()** performs whatever action we want done in response to the button click.

That’s a rather elaborate way of getting a function called. But remember that we are dealing with the basic mechanism for communicating an action of a mouse (or other hardware device) to a program. In particular:

- There are typically many programs running.
- The program is written long after the operating system.
- The program is written long after the GUI library.
- The program can be written in a language that is different from that used in the operating system.
