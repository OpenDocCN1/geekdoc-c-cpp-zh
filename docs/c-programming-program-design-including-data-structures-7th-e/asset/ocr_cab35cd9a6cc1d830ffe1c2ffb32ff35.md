# EXAMPLE 13-4

In this example, we use the `class` rectangleType to illustrate how a `friend` function works. In the following definition we do not document the functions. The complete definition of this class is available at the Web site accompanying this book.

```
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

private:
    double length;
    double width;
};
```

In the definition of the `class` rectangleType, rectangleFriend is declared as a friend function. Suppose that the definition of the function rectangleFriend is:

```
void rectangleFriend(rectangleType recFriendObject)
{
    cout << "recFriendObject area: " << recFriendObject.area()
         << endl;

    recFriendObject.length = recFriendObject.length + 5;
    recFriendObject.width = recFriendObject.width + 5;

    cout << "After increasing length and width by 5 units "
         << "each, \n         recFriendObject area: "
         << recFriendObject.area() << endl;
}
```

The function rectangleFriend contains a (value) formal parameter recFriendObject of type rectangleType. (Note that because rectangleType is a value parameter, it will copy the value of its actual parameter.) The first statement outputs the area of the object recFriendObject. The next two statements increase the length and width of recFriendObject by 5 units. The next statement outputs the area of the object recFriendObject using the new length and width. Note that the recFriendObject accesses its private member variables length and width and that these values