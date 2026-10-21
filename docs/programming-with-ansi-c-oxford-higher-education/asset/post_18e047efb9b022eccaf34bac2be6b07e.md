
```cpp
friend CollectionEmp;
};

class CollectionEmp
{
private:
    employee ColEmp[10];
    int Index;
public:
    bool AddToCol(employee Emp)
    {
        if(Index < 9)
        {
            ColEmp[Index] = Emp;
            Index++;
            return true;
        }
        else
            return false;
    }

    void ListDeptWise()
    {
        string TempDeptName;
        cout << "Enter the department of the university:";
        cin >> TempDeptName;
        cout << "\n";

        for(int i = 0; i < 10; ++i)
        {
            if(ColEmp[i].DeptName == TempDeptName)
            {
                ColEmp[i].DisplayDetails();
            }
        }
    }

    CollectionEmp()
    {
        Index = 0;
    }

    CollectionEmp(employee TempEmp[], int Size = 10)
    {
        Index = 0;
        for(int i = 0; i < Size; ++i)
        {
            AddToCol(TempEmp[i]);
        }
    }
};

void main()
{
employee UniEmployee[10] =
{
    employee(1, "Lara", "Exam", "Professor"),
    employee(2, "Ponting", "Marksheet", "Clerk"),
    employee(3, "Laxman", "Accounts", "Head Clerk"),
    employee(4, "Flintoff", "Exam", "Clerk"),
    employee(5, "Murlidharan", "Accounts", "CAO"),
    employee(6, "Sarfaraz", "Exam", "Informator"),
    employee(7, "Dean Jones", "Exam", "Invigilator"),
    employee(8, "Madugalle", "Exam", "Examiner"),
    employee(9, "Ganguly", "Marksheet", "Repeater"),
    employee(10, "Nafees", "Accounts", "Clerk")
};
CollectionEmp UniCol(UniEmployee);
UniCol.ListDeptWise();
}
```

## How the Program Works

Look at both the constructors of the CollectionEmp class. The constructors of Employee objects (which are contained by the CollectionEmp class) are not called.

```cpp
CollectionEmp()
{
    Index = 0;
}

CollectionEmp(employee TempEmp[], int Size = 10)
{
    Index = 0;
    for(int i = 0; i < Size; ++i)
    {
        AddToCol(TempEmp[i]);
    }
}
```

Let us understand what this program tries to achieve. As this program has already been analysed earlier, let us look at only the additional part. The composite object constructor does not require calling the constructors of the objects it contains.

Earlier we have seen such an example of item object as a part of customer object while discussing copy constructors in Chapter 5. Even then, we have not specified any constructor call in the definition of the customer object. Unlike the constructor of a derived class where the base class constructor must be called, there is no need to call that constructor in this case. However, there may be a need to call the constructors of contained objects in the constructor of the container class. Program 9.9 is an example that represents the case where such constructor calls are needed.

### Calling constructors of contained objects in the composite object

Suppose there is a graphical figure (say, that of a face) that has a triangle, a square, and a pair of circles (to represent the nose, mouth, and pair of eyes). Every instance of the graphical figure determines the position of each of its components, that is, if the first instance of the face is located at (2, 2) on the screen, the components, that is, the pair of circles, the triangle, and the square, will be drawn with respect to (2, 2).

If the next face is drawn at (20, 20), the circles, square, and the triangle will be drawn with respect to position (20, 20). When the face is constructed, all component figures need to be constructed with respect to the position of the face. The constructor of the graphical figure Face should be called with the required arguments, one of which must be Position, which in turn is used to call the constructors of the embedded (component) objects to find their respective positions. It is a simplified face, which can be positioned where one wants it in two-dimensional space. Depending on the position of the face, the elements (two circles for eyes, one triangle for nose, and one square for mouth) are to be drawn. The issues of orientation of the face (the direction the face is facing) and scaling (making the face bigger and smaller) are ignored here for simplicity.

Program 9.9 is for drawing a face, without really drawing a face on the screen, but printing a message alone. If the face is drawn in the program, then the code becomes compiler dependent (as C++ does not have standard graphics library) and more complicated. Therefore, it is not shown here. It is written just for the purpose of representing the concept of composite objects. The only important part to learn is the call to the constructors while initializing user-defined objects that are a part of the composite object, that is, calling the constructors of circle, triangle, and square while calling the constructor for the face. The positions of the component objects depend on the position of the composite object. The constructors of the component objects should be called using MIL as shown in the program. The values given in the program for X and Y coordinates of all the points is intuitively chosen. Drawing the figure might not draw an exact face but might be something similar to it. One may need to play with X and Y values of all the components to get the face look like an actual face.

### PROGRAM 9.9 Composite object where calling constructors of contained objects is necessary

```cpp
//CompositeObj2.cpp
class Point
{
    int X;
    int Y;
public:
    Point(int TempX = 0, int TempY = 0)
    {
        X = TempX;
        Y = TempY;
    }

    int GetX() const
    {
        return X;
    }
    int GetY() const
    {
        return Y;
    }
};

class Square
{
    Point LeftBottom;
    int Length;
public:
    Square(Point TempLeftBottom, int TempLength)
    {
        LeftBottom = TempLeftBottom;
        Length = TempLength;
    }
};

class Triangle
{
    Point Avertex, Bvertex, Cvertex;
public:
    Triangle(Point TempAvertex, Point TempBvertex, Point TempCvertex)
    {
        Avertex = TempAvertex;
        Bvertex = TempBvertex;
        Cvertex = TempCvertex;
    }
};

class Circle
{
    Point Centre;
    int Radius;
public:
    Circle(Point TempCentre, int TempRadius)
    {
        Centre = TempCentre;
        Radius = TempRadius;
    }
};

class Face
{
    Circle LeftEye;
    Circle RightEye;
    Triangle Nose;
    Square Mouth;
    Point Position;
public:
    Face(Point TempPosition) : LeftEye(Point((TempPosition.GetX() + 20),
                                             TempPosition.GetY() + 10), 4),
                               RightEye(Point((TempPosition.GetX() + 50),
                                              TempPosition.GetY() + 10), 4),
                               Nose(Point((TempPosition.GetX() + 35),
                                          TempPosition.GetY() + 20),
                                    (Point((TempPosition.GetX() + 30),
                                           TempPosition.GetY() + 25)),
                                    (Point((TempPosition.GetX() + 40),
                                           TempPosition.GetY() + 25))),
                               Mouth(Point(TempPosition.GetX() + 25,
                                           TempPosition.GetY() + 30), 20)
    {
        Position = TempPosition;
    }
};

void main()
{
    Face DummyFace(Point(20, 30));
    Face OtherFace(Point(50, 70));
}
```

## How the Program Works

Five classes have been defined in this program. The Point class is designed as a platform for deriving all other figures from it. The Point objects are passed to the constructors of Square, Circle, and Triangle. The Point object passed to Square determines the left bottom vertex of the square. The length is also passed as a second argument. Given these two values, a square can easily be drawn. In the case of the triangle, all three vertices are passed. In the case of the circle, a point representing the centre and the radius is passed. The component figures that are under discussion, that is, Square, Circle, and Triangle, are thus composite objects themselves, containing the Point objects within them. There is no need to call the constructor of Point while calling the constructor of any of these objects. Why do we need to call the constructors of Square, Circle, and Triangle in the constructor of their composite object Face? This is because their construction cannot take place in an absolute way. Their construction has one important parameter, the Position, which depends on the construction of the composite object (the position at which the composite object is constructed). So, the constructor of component objects should be called within the body of the composite object.

The program has two objects of type Face. Both are drawn at different places in the two-dimensional space. Since both contain different coordinates, all the objects that are a part of Face need to be drawn at different places. This is achieved by calling the constructor of the component objects in the MIL of the constructor of Face.

## Inherited Members vs Contained Members

At times, a beginner in C++ is confused between the inherited members and the contained members. Though they look same, they are very different. The following are the differences:

- 1. From the design point of view, inherited members have a relationship that is similar to a subset relationship. If Scooter is inherited from Vehicle, then Scooter objects also belong to Vehicle class (scooters are vehicles; hence, they are a subset of vehicles). All instances of Scooter are instances of Vehicle. In Program 9.9, Face contains the object circle, but it does not have the subset relationship. It is rather a part of relationship. Nose (a triangle) is a part of the face. Left and right eyes (circles) are again parts of the face. However, all instances of Triangle and circle are not instances of Face as well.

- 2. Inherited members must execute their constructors outside the constructor body of the derived class using MIL. If the base class has a constructor, the derived class must also have one itself. Both these restrictions do not apply to contained members. We have seen two different cases, one of the employee collection object in Program 9.8 and the other of the component objects Square, Circle, and Triangle in Program 9.9, where the constructors of the embedded objects are not called.

- 3. One needs to be careful while assigning values to the constructors of the contained objects based on the values passed to the constructor of the container class. Here, one needs to execute the constructors of the contained objects in the constructor of the container class using MIL. (Program 9.9 is an example of such a need. Circles, triangle, and square representing the eyes, nose, and mouth, respectively, need to be drawn depending on the position of the face.)

- 4. Both types of members (inherited and contained) are treated by C++ in a similar way (embedded in the target class); so, they seem similar while programming.

- 5. Understanding the difference between the part of and subset relationship helps in one more way. It is called choosing the right link (or inheritance chain) when one is in need of some specific attribute. Suppose an object representing the arm of a sofa is being considered at
