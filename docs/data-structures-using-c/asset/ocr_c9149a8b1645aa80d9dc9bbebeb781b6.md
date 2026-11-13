Here, 0 is a reference to the object, which is used to initialize another object. A constructor is called once for global objects and for static objects. For local objects, the constructor is called each time the object declaration is encountered. With the help of constructors, one of the requirements of ADT implementation, namely initialization at definition time, is fulfilled. We still need a mechanism that automatically destroys an object when it gets invalid (for example, because of leaving its scope). Therefore, destructors are defined.

# ## A.9.2 Destructors

Consider a class `List` for a linked list. The elements of the list are dynamically appended and removed. The constructor helps in creating an initial empty list. However, when we leave the scope of the definition of a list object, we must ensure that the allocated memory is released. We, therefore, define a special method called `destructor`, which is called once for each object at its destruction time.

Destruction of an object takes place when the object leaves its scope of definition or is explicitly destroyed. The latter happens when we dynamically allocate an object and release it when it is no longer needed. Destructors are declared similar to constructors. Thus, they also use the class name, but are prefixed by a tilde (~).

```
```cpp
class Point
{
    int _x, _y;
public:
    Point()
    {
        _x = _y = 0;
    }
    Point(const int x, const int y)
    {
        _x = xval;
        _y = yval;
    }
    Point(const Point & from)
    {
        _x = from._x;
        _y = from._y;
    }
// destructor definition
    ~Point() { /* Nothing to do!*/ }
    void setX(const int val);
    void setY(const int val);
    int getX() { return _x; }
    int getY() { return _y; }
}; // end of class declaration
void main(void)
{
    point appoint; // constructor point :: point()
```
```