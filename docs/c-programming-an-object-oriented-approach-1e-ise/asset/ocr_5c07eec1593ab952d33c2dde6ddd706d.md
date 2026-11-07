# Program 7.4  Using the class Rectangle (Continued)

```
74  cout << "Area: " << rect1.getArea() << endl;
75  cout << "Perimeter: " << rect1.getPerimeter() << endl << endl;
76  // Operations on second rectangle
77  cout << "Rectangle 2: ";
78  rect2.print();
79  cout << "Area: " << rect2.getArea() << endl;
80  cout << "Perimeter: " << rect2.getPerimeter() << endl << endl;
81  // Operations on third rectangle
82  cout << "Rectangle 3: ";
83  rect3.print();
84  cout << "Area: " << rect3.getArea() << endl;
85  cout << "Perimeter: " << rect3.getPerimeter() << endl << endl;
86  return 0;
87  }
```

```
Run
Rectangle 1: A rectangle of 3 by 4.2
Area: 12.6
Perimeter: 14.4

Rectangle 2: A rectangle of 5.1 by 10.2
Area: 52.02
Perimeter: 30.6

Rectangle 3: A rectangle of 5.1 by 10.2
Area: 52.02
Perimeter: 30.6
```

# 7.5 STATIC MEMBERS

As we mentioned, a class type can have two types of members: *instance members* and *static members*. We discussed instance members in the previous section; we discuss static members in this section. As with instance members, we can have *static data members* and *static member functions*. We discuss them separately.

# 7.5.1 Static Data Members

A *static data member* is a data member that belongs to all instances; it also belongs to the class itself. As an example of a *static data member*, assume that we want to keep track of the number of current instances in our program. We can create a *static* data member, called *count*, which is initialized to 0. We can change the definition of all constructors to increment this *static* member every time an instance is created. We can change the definition of the destructor to decrement it when an object is destroyed (goes out of scope). A *static data member* has other applications that we will see later in this chapter and in other chapters.