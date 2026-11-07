# Abstract Classes and Pure Virtual Functions

The preceding sections discussed virtual functions. Other than enforcing run-time binding of functions, virtual functions also have another use, which is discussed in this section. Chapter 11 discussed the second principle of OOD—in­heritance. Through inheritance we can derive new classes without designing them from scratch. The derived classes, in addition to inheriting the existing members of the base class, can add their own members and also redefine or override public and protected member functions of the base class. The base class can contain functions that would want each derived class to implement. There are many scenarios when it is desirable for a class to serve as a base class for a number of derived classes; however, the derived classes may contain certain functions that may not have meaningful definitions in the base class.

Let us consider the class shape given in Chapter 11. As noted in that chapter, from the class shape, you can derive other classes, such as rectangle, circle, ellipse, and so on. Some of the things common to every shape are its center, using the center to move a shape to a different location, and drawing the shape. We can include these in the class shape. For example, you could have the definition of the class shape similar to the following:

```
class shape
{
public:
    virtual void draw();
        //Function to draw the shape.

    virtual void move(double x, double y);
        //Function to move the shape at the position (x, y).

    .
    .
    .
};
```

Because the definitions of the functions draw and move are specific to a particular shape, each derived class can provide an appropriate definition of these functions. Note that we have made the functions draw and move virtual to enforce run-time binding of these functions.

This definition of the class shape requires you to write the definitions of the functions draw and move. However, at this point, there is no shape to draw or move. Therefore, these function bodies have no code. One way to handle this is to make the body of these functions empty. This solution would work, but it has a drawback. Once we write the definitions of the functions of the class shape, then we could create an object of this class and invoke the empty draw and move functions. Because there is no shape to work with, we would like to prevent the user from creating objects of the class shape. It follows that we would like to do the following two things—not include the definitions of the functions draw and move and to prevent the user from creating objects of the class shape.