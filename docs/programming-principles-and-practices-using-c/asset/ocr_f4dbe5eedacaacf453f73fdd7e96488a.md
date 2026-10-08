case, we ask the system to call one of our functions (a “callback function”) when the mouse button is clicked “on our button.” To do that we must

+   • Define a button
• Get it displayed
• Define a function for the GUI to call
• Tell the GUI about that button and that function
• Wait for the GUI to call our function

Let’s do that. A button is part of a **Window**, so (in **Simple_window.h**) we define our class **Simple_window** to contain a member **next_button**: 

```
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

```
Simple_window::Simple_window(Point xy, int w, int h, const string& title)
    : Window(xy,w,h,title),
    next_button(Point{(x_max()-70,0)}, 70, 20, "Next", cb_next),
    button_pushed(false)
{
    attach(next_button);
}
```

Unsurprisingly, **Simple_window** passes its location (**xy**), size (**w,h**), and title (**title**) on to **Graph_lib**’s **Window** to deal with. Next, the constructor initializes **next_button** with a location (**Point{x_max()-70,0}**; that’s roughly the top right corner), a size (**(70,20)**), a label ("Next"), and a “callback” function (**cb_next**). The first four