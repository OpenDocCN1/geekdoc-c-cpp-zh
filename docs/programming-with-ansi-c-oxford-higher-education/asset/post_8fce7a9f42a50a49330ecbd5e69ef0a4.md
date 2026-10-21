
> A typedef can help assess whether the object is of a specific single class. However, for assessing whether an object is a member of a hierarchy of class objects, we need dynamic_cast.

This would solve the problem for the time being. However, if later on HtmlNews inherits into TaggedHtmlNews and UntaggedHtmlNews, one needs to add two more lines at that place. Every time a class is added to the hierarchy, a line needs to be added here. This approach is both error-prone and laborious.

Where is the problem? The problem is that the typedef operator checks for the current news type alone. If it checks all news derived from the current news type, the problem is solved.

Thus, if it is possible to assure that the news item one is looking for belongs to some class derived from PlainTextNews, then it is safe to provide printing. To check this, a check is needed for every possible type of class that is derived from the PlainTextNews class. One needs to check for every such class and add information to modify the code. A solution is needed where it is possible to write a general statement that can work for any descendant of PlainTextNews class, which typedef cannot do. If typedef cannot solve this problem, then how can it be solved? This is explained in the following sections.

## 11.2 DYNAMIC CASTING USING dynamic_cast

In ANSI C++, there are four additional casting operators available, namely, dynamic_cast, static_cast, const_cast, and reinterpret_cast. The first operator, dynamic_cast, provides a solution to the problem mentioned in Section 11.1.9. Let us learn about dynamic_cast. Though it is a casting operator, it is very special. The following are its salient features:

- 1. This casting operator is used only for polymorphic object casting. In other words, it can cast only from one polymorphic object to another polymorphic object.
- 2. It is also known as safe cast. It succeeds only when it is properly casted, which means that dynamic_cast succeeds only when the pointer (or reference) being cast is an object of the target type or its derived type.
- 3. The syntax of dynamic_cast is different from normal C-type casting. It is written as dynamic_cast<ToObjectPtrOrRef> (FromObjectPtrOrRef)
- It casts from FromObject to ToObject pointer or reference. Instead of a FromObject pointer or reference, it is also possible to write an expression that yields a FromObject pointer or reference. From this rule, it is clear that for dynamic_cast to succeed, the FromObject must be of the same type as the ToObject, or derived from it. One needs to be very careful with the syntax. The first set of braces are angled, that is, < > and the second set of braces are normal round, that is, ( ).
- 4. If a Base class and a Derived class are available, then casting from the Derived to the Base pointer always succeeds. However, the casting from the Base to the Derived pointer can succeed only if the Base pointer is actually pointing to an object of the Derived type. This is known as downcasting and we will learn more about it in Section 11.9.
- 5. Conversion (casting) takes place only with the help of pointers or references. It cannot be done with objects.
- 6. While working with pointers, if the dynamic_cast fails, it would return null. So, it is important to check for the return value of dynamic_cast similar to a function to see whether the cast is successful. In case of references, the reference cannot be null; so, dynamic_cast will throw bad_cast when it fails.

```
dynamic_cast<ToObjectPtrOrRef> (FromObjectPtrOrRef)
```

### 11.2.1 Using dynamic_cast

Polymorphic objects such as circle and Shape that we have seen earlier in Program 11.2 can be dynamically casted using dynamic_cast to shape pointer. Let us look at Program 11.4 to understand this better.

```
PROGRAM 11.4 Dynamic casting on polymorphic objects

//PolymorphicDynamic_cast.cpp
#include <iostream>
using namespace std;

class Shape
{
int LineStyle;
int FillColour;
public:
virtual void draw()
{
cout << "Shape is drawn \n";
}
};

class Circle : public Shape
{
int Radius;
int CentrePointX;
int CentrePointY;
public:
void draw()
{
cout << "Circle is drawn \n";
}
};

int main()
{
Shape SomeShape, *PtrShape;
Circle Ring, *PtrCircle;

// Part I

// Testing four possible cases of conversion

// A base pointer pointing to base is casted to base
PtrShape = dynamic_cast<Shape *> (&SomeShape);
if(PtrShape)
cout << "Shape pointer to Shape pointer casted\n";
else
cout << "Shape pointer to Shape pointer not casted\n";

/* A derived pointer pointing to derived is casted to derived */
PtrCircle = dynamic_cast<Circle *> (&Ring);
if(PtrCircle)
cout << "Circle pointer to Circle pointer casted\n";
else
cout << "Circle pointer to Circle pointer not casted\n";

/* A base pointer pointing to base is casted to derived */
PtrCircle = dynamic_cast<Circle *> (&SomeShape);
if(PtrCircle)
cout << "Circle pointer to Circle pointer casted\n";
else
cout << "Circle pointer to Circle pointer not casted\n";
```

```
cout << "Shape pointer to Circle pointer casted\n";
else
cout << "Shape pointer to Circle pointer not casted\n";
/* A derived pointer pointing to derived is casted to base */
PtrShape = dynamic_cast<Shape *> (&Ring);
if(PtrShape)
cout << "Circle pointer to Shape pointer casted\n";
else
cout << "Circle pointer to Shape pointer not casted\n";
/* Part II */
/* Casting from base class pointer to derived */
/* A base pointer pointing to a derived class object
is casted to a derived class object successfully */
cout << "Trying to cast a base class pointer\n";
cout << "pointing to a derived class object\n";
cout << "to a derived class pointer\n";
PtrShape = &Ring;
PtrCircle = dynamic_cast<Circle *> (PtrShape);
if(PtrCircle)
cout << "Successful\n";
else
cout << "Unsuccessful\n";
/* A base pointer pointing to a base class object
failed to cast to a derived class object */
cout << "Trying to cast a base class pointer\n";
cout << "pointing to a base class object\n";
cout << "to a pointer to a derived class object\n";
PtrShape = &SomeShape;
PtrCircle = dynamic_cast<Circle *> (PtrShape);
if(PtrCircle)
cout << "Successful\n";
else
cout << "Unsuccessful\n";
/* A derived pointer pointing to a derived object
is casted to a base class pointer successfully */
cout << "Trying to cast a derived class pointer\n";
cout << "pointing to a derived class object\n";
cout << "to a base class pointer\n";
PtrCircle = &Ring;
PtrShape = dynamic_cast<Shape *> (PtrCircle);
if(PtrShape)
cout << "Successful\n";
else
cout << "Unsuccessful\n";
/* The only option left is a derived class pointer
pointing to a base class object, which is not possible */
```

Output
Shape pointer to Shape pointer casted
Circle pointer to Circle pointer casted

```
Shape pointer to Circle pointer not casted
Circle pointer to Shape pointer casted
Trying to cast a base class pointer
pointing to a derived class object
to a derived class pointer
Successful
Trying to cast a base class pointer
pointing to a base class object
to a pointer to a derived class object
Unsuccessful
Trying to cast a derived class pointer
pointing to a derived class object
to a base class pointer
Successful
```

## How the Program Works

Note that the derived class to derived class and the base class to base class conversions are obviously acceptable. Look at the following casting operations. Both of them are successful.

```
PtrShape = dynamic_cast<Shape *> (&SomeShape);
PtrCircle = dynamic_cast<Circle *> (&Ring);
```

It can also be seen that the derived class pointer to base class pointer conversion is also acceptable.

```
PtrShape = dynamic_cast<Shape *> (&Ring);
```

Base class pointer to derived class pointer is possible only if base class pointer is actually pointing to a derived class object. So, the following conversion is not successful. Conversion from a Shape pointer to a Circle pointer will fail when the pointer is pointing to a base class object.

```
PtrCircle = dynamic_cast<Circle *> (&SomeShape);
```

However, we will succeed in the following attempt, as the pointer that we are trying to convert is indeed pointing to a derived class.

```
PtrShape = &Ring;
PtrCircle = dynamic_cast<Circle *> (PtrShape);
```

The following is another example where a derived class pointer is casted into a base class pointer successfully. The derived class pointer that is pointing to a derived class object is casted to a base class pointer. This pointer can now access only the base class subobject embedded within the derived class object.

```
PtrCircle = & Ring;
PtrShape = dynamic_cast<Shape *> (PtrCircle);
```

### 11.2.2 Using dynamic_cast to Replace typeid

In some cases, the code using dynamic_cast can be replaced by one using typeid. It is better and is advisable to do so in such cases. The code using typeid checks for the first slot in the virtual table (where the RTTI information is kept). It has the same performance overhead as
