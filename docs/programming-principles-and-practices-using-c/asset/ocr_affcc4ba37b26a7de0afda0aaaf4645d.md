The definitions of **Widget** and of the widgets we use here (**Button**, **Menu**, etc.) are found in **GUI.h**.

# ### 16.4.2 Buttons

A **Button** is the simplest **Widget** we deal with. All it does is to invoke a callback when we click on it:

```
```
class Button : public Widget {
    public:
        Button(Point xy, int ww, int hh, const string& s, Callback cb)
            :Widget{xy,ww,hh,s,cb} {}

        void attach(Window& win);
};
```
```

That’s all. The **attach()** function contains all the (relatively) messy FLTK code. We have banished the explanation to Appendix E (not to be read until after Chapters 17 and 18). For now, please just note that defining a simple **Widget** isn’t particularly difficult.

We do not deal with the somewhat complicated and messy issue of how buttons (and other **Widgets**) look on the screen. The problem is that there is a near infinity of choices and that some styles are mandated by certain systems. Also, from a programming technique point of view, nothing really new is needed for expressing the looks of buttons. If you get desperate, we note that placing a **Shape** on top of a button doesn’t affect the button’s ability to function – and you know how to make a shape look like anything at all.

# ### 16.4.3 In_box and Out_box

We provide two **Widgets** for getting text in and out of our program:

```
```
struct In_box : Widget {
    In_box(Point xy, int w, int h, const string& s)
        :Widget{xy,w,h,s,0} {}
    int get_int();
    string get_string();

    void attach(Window& win);
};
```
```