For example, we'll define a C++ class Point includes both a point's location and a member function to set the location.

```
class Point {
private:
    int x;
    int y;
public:
    void setxy(int, newX, int newY);
};
```

```
inline Point::setxy(int newX, int newY) {
    x = newX;
    y = newY;
}
```

Here the member function is coded inline. As stated above, we can also both declare and define the member function within the class itself:

```
class Point {
private:
    int x;
    int y;
public:
    void setxy(int newX, int newY) {
    x = newX;
    y = newY;
};
```

Member functions that are defined in the body of the class are treated as inline was requested. Note that the inline keyword is actually just a polite request to the compiler. The compiler may choose to ignore the request and compile the function as a normal function. Any short function is a candidate to be an inline function.

So inline functions operate like macros in the sense that they can be used to eliminate the overhead of function calls. However, they are different from macros in that:

+   * type checking is performed with inline functions just as it is for any function having a prototype

Focus on Object-Oriented Programming with C++