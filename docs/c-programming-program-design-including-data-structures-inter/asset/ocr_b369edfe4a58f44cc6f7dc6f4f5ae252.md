of type `classIllusFriend`—which is either a local variable of `two` or a formal parameter of `two`—can access its `private` members within the definition of the function `two`. (Example 13-3 illustrates this concept.) Moreover, because a `friend` function is not a member of a class, its declaration can be placed within the `private`, `protected`, or `public` part of the class. However, they are typically placed before any member function declaration.

# **DEFINITION OF A friend FUNCTION**

When writing the definition of a `friend` function, the name of the class and the scope resolution operator do not precede the name of the `friend` function in the function heading. Also, recall that the word `friend` does not appear in the heading of the `friend` function's definition. Thus, the definition of the function `two` in the previous class `classIllusFriend` is:

```
```cpp
void two(/*parameters*/)
{
    .
    .
    .
}
```
```

Of course, we will place the definition of the `friend` function in the implementation file.

The next section illustrates the difference between a member function and a nonmember function (`friend` function) when we overload some of the operators for a specific class. The following example shows how a `friend` function accesses the `private` members of a class.

# **EXAMPLE 13-3**

In this example, we use the `class` `rectangleType` to illustrate how a `friend` function works. In the following definition we do not document the functions. The complete definition of this class is available at the Web site accompanying this book.

```
```cpp
class rectangleType
{
    friend void rectangleFriend(rectangleType recObject);
public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;

    rectangleType();
    rectangleType(double l, double w);
```
```