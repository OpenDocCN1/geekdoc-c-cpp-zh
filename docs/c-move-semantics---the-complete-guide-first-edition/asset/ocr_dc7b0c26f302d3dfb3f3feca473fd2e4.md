```
```cpp
GeoObj(std::string n)
  : name(std::move(n)) {
}
public:
  virtual void draw() const = 0;    // pure virtual function (introducing the API)
  ...
  virtual ~GeoObj() = default;      // would disable move semantics for name
protected:
  // enable copy and move semantics (callable only for derived classes):
  GeoObj(const GeoObj&) = default;
  GeoObj(GeoObj&&) = default;
  // disable assignment operator (due to the problem of slicing):
  GeoObj& operator=(GeoObj&) = delete;
  GeoObj& operator=(const GeoObj&) = delete;
};
```
```

See *poly/geoobj.hpp* for the complete header file.

# 4.4.2  Implementing a Polymorphic Derived Class

A polymorphic derived class might look as follows (see *poly/polygon.hpp* for the complete header file):¹

```
```cpp
class Polygon : public GeoObj {
  protected:
    std::vector<Coord> points;
  public:
    Polygon(std::string s, std::initializer_list<Coord> = {});  // constructor
    virtual void draw() const override;    // implementation of draw()
};
```
```

Usually, in a polymorphic derived classes there is no need to declare any special member function. Especially, there is no need to declare a virtual destructor again (unless you have to implement it). Declaring a destructor again (whether or not it is virtual) would disable automatic support of move semantics for the members of the derived class (here, for the vector points):

```
```cpp
class Polygon : public GeoObj {
  protected:
    std::vector<Coord> points;
  public:
    Polygon(std::string s, std::initializer_list<Coord> = {});  // constructor
    ...
    virtual ~Polygon() = default;  // OOPS: don’t do that because it disables move semantics
};
```
```

¹ `virtual` is not necessary if member functions are declared with `override`. However, I prefer to have it again for better alignment and the rule that either all or no member functions should be virtual.