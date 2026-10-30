
Another important benefit arises when we consider adding new functionality to the program. Suppose we want to implement layouts of exponential expressions. As you will see, we can do this without touching any of our old files (except the main program file, if we wish to use exponential expressions, of course). The key benefit of this strategy is: we can be sure that when we add exponential expressions, there isn’t even a remote chance of damaging the old working code. Programmers (deservedly) tend to be paranoid about their code, and this kind of reassurance is useful. Notice that if the old code was written by one programmer, and the new one by another, then it is very convenient if one programmer’s code is not touched by another. This way there is clarity about who was responsible for what.

## 24.1.3 Adding exponential expressions

We will add a class Pow that will represent exponential expressions. This will be a subclass of Formula2 since it has 2 operands.

```
class Pow : public Formula2{
public:
    Pow(Formula* lhs1, Formula* rhs1){ lhs = lhs1; rhs = rhs1; }
    string op(){return "^";}
    void draw(float clx, float cly){
        lhs->draw(clx, cly);
        rhs->draw(clx+lhs->getWidth(),
                  cly - (lhs->getHeight() - lhs->getDescent())
                  - rhs->getDescent()
                  );
    }
    void setSize(){
        lhs->setSize(); rhs->setSize();
        width = lhs->getWidth() + rhs->getWidth();
        height = lhs->getHeight() + rhs->getHeight();
        descent = lhs->getDescent();
    }
};
```

The basic idea is to layout the exponent above and to the right of the base. The detailed expressions which decide how to position what are obtained in the manner of Section ??, and are left for you to figure out. Using this class is simple, to represent X + Y^Z we simply write Sum(new Literal("X"), new Pow(new Literal("Y"), new Literal("Z"))).

The key point to appreciate is that this new code can be developed independently, in a new file, without even having the rest of the code, only the class header files would be needed.. If we had used the coding approach of Section 22.1, we would need to have and modify the old code.

## 24.2 The simplecpp graphics system

We will discuss the role played by inheritance in the design of the simplecpp graphics system. Although this system is quite small by standards of real graphics systems, we will not discuss the entire system here, but only some relevant portions of it.

Briefly stated, the core specification of the system is: allow the user to create and manipulate graphical objects on the screen. This statement is very vague, of course. What does it mean to manipulate objects? As you know, in simplecpp, manipulate simply means move, rotate, scale. There are also other questions: what kind of primitives is the user to be given? Will the user need to specify how each object appears in each frame (like the picture frames in a movie) or will the user only state the incremental changes, e.g. move object x, which means the other objects remain unchanged? As you know, we have opted for the latter. And then of course there is the question of what kinds of objects we can have. As you know, simplecpp supports the following kinds of graphical objects: circles, lines, rectangles, polygons, turtles and text.

So in the rest of this section, we consider the problem of creating and manipulating the objects given above, in the manner described above. We will not discuss issues such as the pens associated with each object, or graphical input, as in the getClick command.

Clearly, such a system must have the following capabilities:

- 1. It must be able to keep track of the objects created by the user so far.
- 2. It should be able to display the objects on the screen.
- 3. It should be able to manipulate the objects as requested, e.g. move an object.

Let us take item 2 first. simplecpp is built on top of the X Windows system, which provides functions that can draw lines, arcs, polygons, circles (filled and non-filled) on the screen, at the required place. So we call these functions. Item 3 is also relatively easy. With each object we associated some configuration data, which says how large it is to be drawn, in what orientation, and where. Note that this data is distinct from the shape data. Item 1 is also not difficult in principle: we merely keep a list or a set of some kind in which we place each object. To complete this very high level description we need to answer one more question: when should the objects be displayed? The simplest answer to this is: whenever the user changes the state of any object, clear the entire display and display all objects again. Inheritance is useful for facilitating many of the actions described here.

It should be clear that we have the category of all graphical objects, and then subcategories corresponding to different types of objects, e.g. circles. So clearly, these correspond to subclasses of the class representing the category ALL of all objects. Our categories indeed form a hierarchy, and so do the associated classes, as shown in Figure 24.1. The class associated with the category of all objects is called Sprite, in honour of the Scratch programming environment (scratch.mit.edu), where the name is used for a similar concept.

The hierarchy facilitates storing of information as follows. In the Sprite class we keep all attributes that are common to all graphics objects. At first glance, you might think that precious little might be common to all the very different looking objects: circles, lines, polygons and so on. But as mentioned earlier, when a graphics object is to be displayed on the screen, it will have a position, orientation, scale in addition to its shape. It will also have

attributes such as colour. All objects will have these attributes. So these attributes become data members in the Sprite class.

The classes Circle, Line, Polygon etc. will contain the shape related attributes (in addition to all the attributes inherited from Sprite). For example, Circle contains a data member called radius which holds the radius of the circle being drawn. The Polygon class contains an array which holds the coordinates of the vertices of the polygon. As discussed earlier these coordinates are given in a specially created coordinate frame; while drawing they will be drawn relative to the position of the polygon (as recorded in the Sprite part of its object). Figure 24.2 shows possible ways contents of the Circle and Sprite classes. The actual implementations different, and you can see them in the code supplied.

In addition, we must also consider function members. Suppose we wish to move an object. This requires two actions: (a) recording that the object has indeed been moved, and updating its position accordingly, (b) redrawing the object on the screen. Clearly, action (a) can be performed independent of the shape of the object, whereas (b) requires the shape information. Thus in our implementation, action (b) is implemented by a paint method in each shape class. The move member function is defined in the Sprite class. It performs action (a) using the attributes available in the Sprite class. It then signals that all objects need to be redrawn.

The redrawing works as follows. Essentially simplecpp maintains a vector that holds pointers to all objects active at the current instant. Suppose the vector is named ActiveSprites, then its declaration would be

```
vector<Sprite*> ActiveSprites;
```

Because the elements of ActiveSprites have type Sprite*, they can hold pointers to any graphical object. When the objects are to be drawn, we simply iterate over the queue and execute the paint method of the object.

```
for(int i=0; i < ActiveSprites.size(); i++){
    ActiveSprites[i]->paint();
}
```

![](img/c7233aedab7e4c7cad32a7615b6a4783_412_0.png)

Figure 24.1: Heirarchy of graphics object categories

```
class Sprite{
protected:
    double x,y;            // position on the canvas
    double orientation;    // angle in radians made with the x axis
    double scale;          // scaling factor
    Color fill_color;      // Color is a data type in the X windows Xlib package.
    bool fill;             // whether to fill or not
    ...
public:
    Sprite();
    Sprite(double x, double y);
    ...
    void forward(double dist);
    ...
    virtual void paint()=0;
    ...
}

class Circle : public Sprite{
private:
    double radius;
public:
    Circle();
    Circle(double x, double y, double radius=10);
    void init(double x, double y, double radius=10);
    virtual void paint()
};
```

Figure 24.2: Possible definitions of Sprite and Circle
