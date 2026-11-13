# 1.2.1 Class

Class is one of the most important features of C++. A class is a collection of variables of different data types and functions. The variables in a class are called member variables, and the functions in a class are called member functions or methods. A class is created with the keyword class. Class is similar to structure the only difference being that all the members of a class are by default private, whereas all the members of structure are public by default. Syntactically, class is similar to structure.

```
class Class-name
{
private:
    members
    access-specifier1
    members
    access-specifier2
    members
    - - - - - -
    - - - - - -
};
```

The body of the class may contain members that are either data or a function declaration. The class - name is the name of the class, the access - specifier can be one of the three keywords public, private or protected, which will be discussed later. By convention the class name should begin with an uppercase letter.

```
class Shape
{
    int l,b;
    public:
    void area()
    {
        cout<<"area of rectangle is:"<<<*l*b;
    }
};
```

In the above program Shape is class. The variables l,b are private and the function area() is public. Every class must terminate with a semicolon.

# 1.2.2 OBJECTS

Class defines a new data type that combines both the code and the data, and this new type can be used to create an object of that class. So, an object is an instance of a class. A class has a logical appearance, whereas an object has physical existence.

The declaration of an object is similar to the declaration of variables.

```
float x,y;                 //declaration of variables
Shape s1,s2                //declaration of objects with type Shape.
```

For the above class, Shape s1, s2 are the objects. s1 will hold the variables l,b values and function area(). Similarly, s2 will also have the copy of members of the Shape class.