
This produces

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_496_0.png)

Note that we can see the lines that make up the rectangles even though we have filled (all but one of them). If we don't like those outlines, we can remove them:

```cpp
rect00.set_color(Color::invisible);
rect11.set_color(Color::invisible);
rect12.set_color(Color::invisible);
rect21.set_color(Color::invisible);
rect22.set_color(Color::invisible);
```

We get

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_496_1.png)

Note that with both fill color and line color set to invisible, **rect22** can no longer be seen.

Because it has to deal with both line color and fill color, **Rectangle**’s **draw_lines()** is a bit messy:

```cpp
void Rectangle::draw_lines() const
{
    if (fill_color().visibility()) {   // fill
        fl_color(fill_color().as_int());
        fl_rectf(point(0).x, point(0).y, w, h);
    }

    if (color().visibility()) {      // lines on top of fill
        fl_color(color().as_int());
        fl_rect(point(0).x, point(0).y, w, h);
    }
}
```

As you can see, FLTK provides functions for drawing rectangle fill (**fl_rectf()**) and rectangle outlines (**fl_rect()**). By default, we draw both (with the lines/outline on top).

## 13.10 Managing unnamed objects

So far, we have named all our graphical objects. When we want lots of objects, this becomes infeasible. As an example, let us draw a simple color chart of the 256 colors in FLTK’s palette; that is, let’s make 256 colored squares and draw them in a 16-by-16 matrix that shows how colors with similar color values relate. First, here is the result:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_497_0.png)

Naming those 256 squares would not only be tedious, it would be silly. The obvious “name” of the top left square is its location in the matrix (0,0), and any other square is similarly identified (“named”) by a coordinate pair (i,j). What we need for this example is the equivalent of a matrix of objects. We thought of using a vector<Rectangle>, but that turned out to be not quite flexible enough. For example, it can be useful to have a collection of unnamed objects (elements) that are not all of the same type. We discuss that flexibility issue in §14.3. Here, we’ll just present our solution: a vector type that can hold named and unnamed objects:

```cpp
template<class T> class Vector_ref {
public:
    // ...
    void push_back(T&); // add a named object
    void push_back(T*); // add an unnamed object

    T& operator[](int i); // subscripting: read and write access
    const T& operator[](int i) const;

    int size() const;
};
```

The way you use it is very much like a standard library vector:

```cpp
Vector_ref<Rectangle> rect;

Rectangle x {Point(100,200),Point(200,300)};
rect.push_back(x); // add named

rect.push_back(new Rectangle(Point(50,60),Point(80,90))); // add unnamed

for (int i=0; i<rect.size(); ++i) rect[i].move(10,10); // use rect
```

We explain the new operator in Chapter 17, and the implementation of Vector_ref is presented in Appendix E. For now, it is sufficient to know that we can use it to hold unnamed objects. Operator new is followed by the name of a type (here, Rectangle) optionally followed by an initializer list (here, {Point(50,60),Point(80,90)}). Experienced programmers will be relieved to hear that we did not introduce a memory leak in this example.
Given Rectangle and Vector_ref, we can play with colors. For example, we can draw a simple color chart of the 256 colors shown above:

```cpp
Vector_ref<Rectangle> vr;

for (int i = 0; i<16; ++i)
    for (int j = 0; j<16; ++j) {
        vr.push_back(new Rectangle(Point(i*20,j*20),20,20));
        vr[vr.size()-1].set_fill_color(Color(i*16+j));
        win20.attach(vr[vr.size()-1]);
    }
```

We make a **Vector_ref** of 256 **Rectangles**, organized graphically in the **Window** as a 16-by-16 matrix. We give the **Rectangle**s the colors 0, 1, 2, 3, 4, and so on. After each **Rectangle** is created, we attach it to the window, so that it will be displayed:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_499_0.png)

## 13.11 Text

Obviously, we want to be able to add text to our displays. For example, we might want to label our “odd” **Closed_polyline** from §13.8:

```cpp
Text t {Point(200,200),"A closed polyline that isn't a polygon"};
t.set_color(Color::blue);
```

We get

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_500_0.png)

Basically, a **Text** object defines a line of text starting at a **Point**. The **Point** will be the bottom left corner of the text. The reason for restricting the string to be a single line is to ensure portability across systems. Don't try to put in a newline character; it may or may not be represented as a newline in your window. String streams (§11.4) are useful for composing **string** for display in **Text** objects (examples in §12.7.7 and §12.7.8). **Text** is defined like this:

```cpp
struct Text : Shape {
    // the point is the bottom left of the first letter
    Text(Point x, const string& s)
        : lab(s)
        { add(x); }

    void draw_lines() const;

    void set_label(const string& s) { lab = s; }
    string label() const { return lab; }

    void set_font(Font f) { fnt = f; }
    Font font() const { return fnt; }

    void set_font_size(int s) { fnt_sz = s; }
    int font_size() const { return fnt_sz; }

private:
    string lab; // label
    Font fnt { fl_font() };
    int fnt_sz { (fl_size()<14)?14:fl_size() };
};
```

If you want the font character size to be less than 14 or larger than the FLTK default, you have to explicitly set it. This is an example of a test protecting a user from possible variations in the behavior of an underlying library. In this case, an update of FLTK changed its default in a way that broke existing programs by making the characters tiny, and we decided to prevent that problem.

We provide the initializers as member initializers, rather than as part of the constructors' initializer lists, because the initializers do not depend on constructor arguments.

Text has its own draw_lines() because only the Text class knows how its string is stored:

```cpp
void Text::draw_lines() const
{
    fl_draw(lab.c_str(),point(0).x,point(0).y);
}
```

The color of the characters is determined exactly like the lines in shapes composed of lines (such as Open_polyline and Circle), so you can choose a color using set_color() and see what color is currently used by color(). The character size and font are handled analogously. There is a small number of predefined fonts:

```cpp
class Font { // character font
public:
    enum Font_type {
        helvetica=FL_HELVETICA,
        helvetica_bold=FL_HELVETICA_BOLD,
        helvetica_italic=FL_HELVETICA_ITALIC,
        helvetica_bold_italic=FL_HELVETICA_BOLD_ITALIC,
        courier=FL_COURIER,
        courier_bold=FL_COURIER_BOLD,
        courier_italic=FL_COURIER_ITALIC,
        courier_bold_italic=FL_COURIER_BOLD_ITALIC,
        times=FL_TIMES,
        times_bold=FL_TIMES_BOLD,
        times_italic=FL_TIMES_ITALIC,
        times_bold_italic=FL_TIMES_BOLD_ITALIC,
        symbol=FL_SYMBOL,
        screen=FL_SCREEN,
        screen_bold=FL_SCREEN_BOLD,
        zapf_dingbats=FL_ZAPF_DINGBAT
    };

    Font(Font_type ff) :f(ff) {}
    Font(int ff) :f(ff) {}

    int as_int() const { return f; }
private:
    int f;
};
```

The style of class definition used to define **Font** is the same as we used to define **Color** (§13.4) and **Line\_style** (§13.5).

## 13.12 **Circle**

Just to show that the world isn't completely rectangular, we provide class **Circle** and class **Ellipse**. A **Circle** is defined by a center and a radius:

```cpp
struct Circle : Shape {
    Circle(Point p, int rr);    // center and radius

    void draw_lines() const;

    Point center() const ;
    int radius() const { return r; }
    void set_radius(int rr)
    {
        set_point(0,Point{center().x-rr,center().y-rr}); // maintain
                                                          // the center

        r = rr;
    }
private:
    int r;
};
```

We can use **Circle** like this:

```cpp
Circle c1 {Point{100,200},50};
Circle c2 {Point{150,200},100};
Circle c3 {Point{200,200},150};
```
