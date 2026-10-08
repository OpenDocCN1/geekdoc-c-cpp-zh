```
public:
  void draw();  // override Shape::draw
  // ... 
};
Circle c(p,20);  // OK: Circle is not abstract
```

The most common way of making a class abstract is to define at least one pure virtual function. A pure virtual function is a virtual function that requires overriding:

```
class Shape {
 public:
  virtual void draw() = 0;  // =0 means “pure”
  // ... 
};
```

See §14.3.5.

The rarer, but equally effective, way of making a class abstract is to declare all its constructors protected (§14.2.1).

# ### A.12.4.3 Generated operations

When you define a class, it will by default have several operations defined for its objects:

+   • Default constructor
• Copy operations (copy assignment and copy initialization)
• Move operations (move assignment and move initialization)
• Destructor

Each is (again by default) defined to apply recursively to each of its base classes and members. Construction is done “bottom-up,” that is, bases before members. Destruction is done “top-down,” that is, members before bases. Members and bases are constructed in order of appearance and destroyed in the opposite order. That way, constructor and destructor code always relies on well-defined base and member objects. For example:

```
struct D : B1, B2 {
  M1 m1;
  M2 m2;
};
```