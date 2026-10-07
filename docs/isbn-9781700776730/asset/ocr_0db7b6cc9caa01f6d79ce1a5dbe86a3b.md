It would be illegal to declare move() to be a constant member function. For any constant member function, the hidden pointer is treated as a pointer to a constant object and thus attempted updates to the object's data are flagged as errors. The following code will not compile due to the const keyword added to the move() member function:

```
class Point {
  private:
    int x, y;
  public:
    Point(int a, int b) { x = a; y = b; }
    int xPos() const { return x; }
    int yPos() const { return y; }
    void move(int dx, int dy) const { x += dx; y += dy; }
};
```

A constant member function defined outside the class body must specify the const keyword in both its declaration and definition:

```
class Point {
  private:
    int x, y;
  public:
    Point(int a, int b) { x = a; y = b; }
    int xPos() const;
    int yPos() const;
    void move(int dx, int dy) const { x += dx; y += dy; }
};

int Point::xPos() const { return x; }
int Point::yPos() const { return y; }
```

You must also be careful when calling other functions inside a constant member function. These other functions cannot be allowed to modify any of the data members. The compiler ensures that when inside a constant member function, each data member is typed as though it were a constant! Thus, the only legal way to pass the members to another function is either by value, or by using pointers to constants, or by using references to constants.

We introduce a new member function modify(), which calls a random function to assign the coordinates random values: