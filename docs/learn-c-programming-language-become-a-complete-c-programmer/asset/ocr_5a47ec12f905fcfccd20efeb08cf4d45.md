unlikely case where two base classes provided operations with exactly the same name, but with different semantics: add an interface layer. Consider the classical (but mostly hypothetical/theoretical) example of a class of a draw() member function in a video game involving cowboys:

```
class Window {
public:
void draw(); // displayimage
// ...
};
```

```
class Cowboy {
public:
void draw(); // pull gun from holster
// ...
};
```

```
class Cowboy_window : public Cowboy, public Window {
// ...
};
```

How do we override Cowboy::draw() and Window::draw()? These two functions have radically different meanings (semantics) but are identical in name and type; we need to override them by two separate functions. There is no direct language solution to this (exotic) problem, but adding intermediate classes will do:

```
struct WWindow : Window {
using Window::Window;
virtual void win_draw() = 0;
void draw() override final { win_draw(); }
};
```

```
// inheritconstructors
// force derived class to override // displayimage
```

```
struct CCowboy : Cowboy{
using Cowboy::Cowboy;
virtual void cow_draw() = 0;
void draw() override final { cow_draw(); }
};
```

```
// inheritconstructors
// force derived class to override // pull gun from holster
```

```
class Cowboy_window : public CCowboy, public WWindow { public:
void cow_draw() override;
void win_draw() override;
// ...
};
```

Or graphically: