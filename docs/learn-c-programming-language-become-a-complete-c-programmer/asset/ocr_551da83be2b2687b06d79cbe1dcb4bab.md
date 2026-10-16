This design is cleaner and more easily maintainable than the traditional one – and no less efficient. However, it still fails to solve the version control problem:

```
class Ival_box { /* ... */ }; // common
class Ival_slider
: public Ival_box, protected BBwidget { /* ... */ }; // for BB
class Ival_slider
: public Ival_box, protected CWwidget { /* ... */ }; // for CW
// ...
```

There is no way of having the Ival_slider for BBwidgets coexist with the Ival_slider for CWwidgets, even if the two user-interface systems could themselves coexist. The obvious solution is to define several different Ival_slider classes with separate names:

```
class Ival_box { /* ... */ };
class BB_ival_slider
: public Ival_box, protected BBwidget { /* ... */ };
class CW_ival_slider
: public Ival_box, protected CWwidget { /* ... */ };
// ...
```

or graphically:

```
BBwidget Ival_box CWwidg et
BB_ival_slider CW_ival_slider
```

To further insulate our application-oriented Ival_box classes from implementation details, we can derive an abstract Ival_slider class from Ival_box and then derive the system-specific Ival_sliders from that:

```
class Ival_box { /* ... */ };
class Ival_slider
: public Ival_box { /* ... */ };
class BB_ival_slider
: public Ival_slider, protected BBwidget { /* ... */ };
class CW_ival_slider
: public Ival_slider, protected CWwidget { /* ... */ };
// ...
```

or graphically:

```
Ival_box
BBwidget Ival_slider CWwidg et
BB_ival_slider CW_ival_slider
```

# Section 21.2.3 Alternative Implementations 621

Usually, we can do better yet by utilizing more specific classes in the implementation hierarchy. For example, if the “Big Bucks Inc.” system has a slider class, we can derive our Ival_slider directly from the BBslider:

```
class BB_ival_slider
: public Ival_slider, protected BBslider { /* ... */ };
```