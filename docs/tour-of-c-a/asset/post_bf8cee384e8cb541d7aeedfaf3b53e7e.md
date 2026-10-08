
knows only the interface defined by Container. Consequently, use(Container&) needn't be recompiled if the implementation of List_container changes or a brand-class derived from Container is used.

The flip side of this flexibility is that objects must be manipulated through pointers or references (§6.2, §15.2.1).

## 5.4 Virtual Functions

Consider again the use of Container:

Click here to view code image

```
void use(Container& c) {
    const int sz = c.size();
    for (int i=0; i<sz; ++i)
        cout << c[i] << "\n";
}
```

How is the call of c[i] in use() resolved to the right operator[]? When a hi calls use(), List_container's operator[] must be called. When a gi calls use(), Vector_container's operator() must be called. To achieve this achievement, a Container object must contain information to allow it to select the right function to call at runtime. The compiler converts the name of a virtual function into an index into a table of pointers to functions. That table is usually called the virtual function table or simply the vtable. Each class with virtual functions has its vtable identifying its virtual functions. Can be represented graphically like this:

| Vector_container: | vtable: |
| --- | --- |
| v | Vector_container::operator[]() |
| | Vector_container::size() |
| | Vector_container::Vector_container() |

| List_container: | vtable: |
| --- | --- |
| Id | List_container::operator[]() |
| | List_container::size() |
| | List_container::List_container() |

The functions in the vtable allow the object to be used correctly even when the size of the object and the layout of its data are unknown to the caller. The implementation of the caller needs only to know the location of the pointer to the vtable in a Container and the index used for each virtual function. This virtual call mechanism can be made as efficient as the "normal function call" mechanism (within 25% and far cheaper for repeated calls to the same object). Its space overhead is one pointer in each object of a class with virtual functions plus one vtbl for each such class.

## 5.5 Class Hierarchies

The Container example is a very simple example of a class hierarchy. A class hierarchy is a set of classes ordered in a lattice created by derivation (e.g., public). We use class hierarchies to represent concepts that have hierarchical relationships, such as "A fire engine is a kind of truck that is a kind of a vehicle" and "Smiley face is a kind of a circle that is a kind of a shape." Huge hierarchies, with hundreds of classes, that are deep and wide are common. As a semi-realistic classic example, let's consider shapes on a screen:

![](img/0bd2e25eba2737c3c5daca16fad1b65b_78_0.png)

The arrows represent inheritance relationships. For example, class Circle is derived from class Shape. A class hierarchy is conventionally drawing down from the most basic class, the root, towards the (later defined) derived classes. To represent simple diagram in code, we must first specify a class that defines the general properties of all shapes:

Click here to view code image

```
class Shape {
public:
    virtual Point center() const = 0;      // pure virtual
    virtual void move(Point to) = 0;

    virtual void draw() const = 0;          // draw on current "Canvas"
    virtual void rotate(int angle) = 0;

    virtual ~Shape()                     // destructor // ...
};
```

Naturally, this interface is an abstract class: as far as representation is concerned, nothing (except the location of the pointer to the vtbl) is common for every Shape. Given this definition, we can write general functions manipulating vectors of points to shapes:

Click here to view code image

```
void rotate_all(vector<Shape>& v, int angle) // rotate v's elements by angle degrees
{
    for (auto p : v)
        p->rotate(angle);
}
```

To define a particular shape, we must say that it is a Shape and specify its particular properties (including its virtual functions):

Click here to view code image

```
class Circle : public Shape {
public:
    Circle(Point p, int rad) : x{p}, r{rad} {}

    Point center() const override { return x; }
    void move(Point to) const override { x = to; }
    void draw() const override;
    void rotate(int angle) override;
private:
    Point x;       // center
    int r;          // radius
};
// constructor
// nice simple algorithm

So far, the Shape and Circle provide examples showing nothing new compared to the Container and Vector_container example, but we can build further:

Click here to view code image

```
class Smiley : public Circle // // use the circle as the base for the face
public:
    Smiley(Point p, int rad) : Circle(p,rad), mouth(nullptr) {}
    ~Smiley() {
        delete mouth;
        for (auto p : eyes)
            delete p;
    }

    void move(Point to) override;
    void draw() const override;
    void rotate(int angle) override;

    void add_eye(Shape*) s {
        eyes.push_back(s);
    }

    void set_mouth(Shape*) s; // // wink eye number i
    virtual void wink(int i);
// ...
private:
    vector<Shape*> eyes; // // usually two eyes
    Shape* mouth;
};
```

The push_back() member of vector copies its argument into the vector (here, eyes) as the last element, increasing vector's size by one.

We can now define Smiley::draw() using calls to Smiley's base and member draw(j):

```
void Smiley::draw() const
{
  Circle::draw();
  for (auto p : eyes)
    p->draw();
  mouth->draw();
}
```

The way that Smiley keeps its eyes in a standard-library vector and deletes them in its destructor. Shape's uses of virtual and Smiley's destructor overrides it. A virtual destructor is essential for an abstract class an an object of a derived class is usually manipulated through the interface provided by its abstract base class. In particular, it may be deleted through a pointer to a base class. That destructor, the function call mechanism ensures that the proper destructor is called. That destructor implicitly invokes the destructors of its base and members.

## 5.5.1 Benefits from Hierarchies

A class hierarchy offers two kinds of benefits:

- Interface inheritance: An object of a derived class can be used wherever an object of a base class is required. That is, base class provides interfaces.
- Implementation inheritance: Base classes provide implementations, using pointers or references. For example, consider a function that reads shapes from input stream:

```cpp
enum Kind { circle, triangle, smiley };

Shape* read_shape(istream& is) // It read shape from input stream
{
  Kind k; // finds its Kind
  switch (k) {
    case Kind::circle: // read circle data (Point,r)
      return new Circle(p,r);
    case Kind::triangle: // read triangle data (Point,p2,p3)
      return new Triangle(p1,p2,p3);
    case Kind::smiley: // read smiley data (Point,r)
      Smiley* ps = new Smiley(p,r);
      ps->add_eye(e1);
      ps->add_eye(e2);
      ps->set_mouth(m);
      return ps;
  }
}
```

A program may use that:

```cpp
void user()
{
  vector<Shape> v;

  while (cin)
    v.push_back(read_shape(cin));

  draw_all(v);
  rotate_all(v,45);

  for (auto p : v)
    delete p;
}
```

Obviously, the example is simplified – especially with respect to error handling – but it vividly illustrates that user() has absolutely no kind of shapes it manipulates. The user() code can be compiled and used later for new Shapes added to the program. Note that there are no pointers to the outside user(), so user()'s virtual destructor is responsible for deallocating this. Because destructor is virtual, delete operator correctly invokes the Shape's virtual destructor for the most derived class. This is crucial because a derived class may have acquired all kinds of resources (such as file handles, locks, and output streams) that need to be released. In this case, a Smiley deletes its eyes and mouth objects. Once it has done that, it calls Circle's destructor. Objects are constructed "bottom up" (base first) and destructed "top down" (derived) by constructors.

## 5.5.2 Hierarchy Navigation

The read_shape() returns a Shape* that we can treat all Shapes. However, how can we we want to use a member that is only provided by a particular derived class, such as Smiley's wink(); We can ask "is this Shape a kind of Smiley?" using the dynamic_cast operator:

```
Shape* ps = (read_shape(cin));

if (Smiley* p = dynamic_cast<Smiley*>(ps)) { // If ps does point to a Smiley
  // ... a Smiley; use it ...
}\else {
  // ... not a Smiley, try something else ...
}
```
