
```cpp
Vector read(istream& is) 
{
    Vector v;
    for (double d; is>>d; ) // read floating-point values into d
        v.push_back(d); // add d to v
    return v;
}
```

```cpp
Vector v1 = {1, 2, 3, 4, 5};
Vector v2 = {1.23, 3.45, 6.7, 8};
```

// v1 has 5 elements
// v2 has 4 elements

```cpp
Vector::Vector(std::initializer_list<double> lst) // Il initialize with a list
    :elem{new double[lst.size()]}, sz{static_cast<int>(lst.size())}
{
    copy(lst.begin(),lst.end(),elem); // Il copy from lst into elem (§13.5)
}
```

```cpp
class Container {
public:
    virtual double& operator[](int) = 0; // Il pure virtual function
    virtual int size() const = 0; // Il const member function (§5.2.1)
    virtual ~Container() {} // destructor (§5.2.2)
};
```

```cpp
Container c;
Container* p = new Vector_container(10);
```

// Il error: there can be no objects of an abstract class
// OK: Container is an interface for Vector_container

```cpp
void use(Container& c)
{
    const int sz = c.size();

    for (int i=0; i!=sz; ++i)
        cout << c[i] << '\n';
}
```

```cpp
class Vector_container : public Container { // Vector_container implements Container
public:
    Vector_container(int s) : v(s) { // Vector of s elements
    Vector_container() {}

    double& operator[](int i) override { return v[i]; }
    int size() override { return v.size(); }
private:
    Vector v;
};
```

```cpp
void g()
{
    Vector_container vc(10); // Vector of ten elements
    // ... fill vc ...
    use(vc);
}
```

```cpp
class List_container : public Container { // Il List_container implements Container
public:
    List_container() { // Il empty List
    List_container(initializer_list<double> il) : ld(il) {}
    ~List_container() {}

    double& operator[](int i) override;
    int size() const override { return ld.size(); }

private:
    std::list<double> ld; // II (standard-library) list of doubles (\SS 12.3)
};

double& List_container::operator[](int i)
{
    for (auto& x : ld) {
        if (i==0)
            return x;
        --i;
    }
    throw out_of_range{"List container"};
}
```

```cpp
void h()
{
    List_container lc = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    use(lc);
}
```

```cpp
void use(Container& c)
{
    const int sz = c.size();

    for (int i=0; i!=sz; ++i)
        cout << c[i] << '\n';
}
```

```cpp
class Shape {
public:
    virtual Point center() const =0; // Il pure virtual
    virtual void move(Point to) = 0;

    virtual void draw() const = 0; // Il draw on current "Canvas"
    virtual void rotate(int angle) = 0;

    virtual ~Shape() {} // Il destructor
    // ...
};
```

```cpp
void rotate_all(vector<Shape*>& v, int angle) // rotate v's elements by angle degrees
{
    for (auto p : v)
        p->rotate(angle);
}
```

```cpp
class Circle : public Shape {
public:
    Circle(Point p, int rad) :x{p}, r{rad} {} // constructor

    Point center() const override { return x; }
    void move(Point to) override { x = to; }
    void draw() const override;
    void rotate(int) override {} // nice simple algorithm
private:
    Point x; // center
    int r; // radius
};
```

```cpp
class Smiley : public Circle { // use the circle as the base for a face
public:
    Smiley(Point p, int rad) : Circle{p,rad}, mouth{nullptr} {}
    ~Smiley()
    {
        delete mouth;
        for (auto p : eyes)
            delete p;
    }

    void move(Point to) override;

    void draw() const override;
    void rotate(int) override;

    void add_eye(Shape* s)
    {
        eyes.push_back(s);
    }

    void set_mouth(Shape* s);
    virtual void wink(int i); // wink eye number i

    // ...

private:
    vector<Shape*> eyes; // usually two eyes
    Shape* mouth;

};
```

```cpp
enum class Kind { circle, triangle, smiley };

Shape* read_shape(istream& is) // read shape descriptions from input stream
{
    // Il ... read shape header from is and find its Kind k ...

    switch (k) {
        case Kind::circle:
            // Il ... read circle data {Point,int} into p and r ...
            return new Circle(p,r);
        case Kind::triangle:
            // Il ... read triangle data {Point,Point,Point} into p1, p2, and p3 ...
            return new Triangle(p1,p2,p3);
        case Kind::smiley:
            // Il ... read smiley data {Point,int} into p and r ...
            return new Smiley(p,r);
    }
}
```
