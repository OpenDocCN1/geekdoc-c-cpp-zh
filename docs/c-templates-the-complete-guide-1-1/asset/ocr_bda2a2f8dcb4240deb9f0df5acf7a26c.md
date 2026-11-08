```
);

// concrete geometric object class Circle

// - derived from GeoObj

class Circle : public GeoObj {

public:

    virtual void draw() const override;

    virtual Coord center_of_gravity() const override;

    ...

};

// concrete geometric object class Line

// - derived from GeoObj

class Line : public GeoObj {

public:

    virtual void draw() const override;

    virtual Coord center_of_gravity() const override;

    ...

};
```

After creating concrete objects, client code can manipulate these objects through references or pointers to the common base class by using the virtual function dispatch mechanism. Calling a virtual member function through a pointer or reference to a base class subject results in an invocation of the appropriate member of the specific “most-derived” (concrete) object being referred to.

For example, the concrete code can be sketched as follows:

[Click here to view code image](#)

![](bbox=[0.081, 0.479, 0.919, 0.572])

poly/dynamic1.cpp

```
#include <iostream>

#include <vector>

// draw any GeoObj

void myDraw (GeoObj const& obj)
{
    obj.draw();                  // call draw() according to
}

// compute distances to center of gravity between two

Coord distance (GeoObj const& x1, GeoObj const& x2)
{
    Coord c = x1.center_of_gravity() - x2.center_of_gravity();
    return c.abs();              // return coordinates as above
}

// draw heterogeneous collection of GeoObjs

void drawElements (std::vector<GeoObj*> const& elems)
{
    for (std::vector<GeoObj*>::iterator i=elems.begin(); i!=elems.end(); ++i) {
        (*i)->draw();            // call draw() according to
    }
}
```