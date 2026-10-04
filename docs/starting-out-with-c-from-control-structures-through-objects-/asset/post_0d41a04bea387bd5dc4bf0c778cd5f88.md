
## Appendix O: Solutions to Odd Numbered Review Questions

9. By using the getline function.

10. Two arguments: The starting address of the section of memory where the data will be stored, and the number of bytes to read.

11. The seekg function moves a file's write position, and the seekp function moves a file's read position.

12. Call the file object's clear member function.

13. Use the seekg function to move the read position back to the beginning of the file.

14. NULL or 0

- 21. getline
- 23. put
- 25. text, ASCII text
- 27. structures
- 29. read
- 31. sequential
- 33. seekg
- 35. tellg
- 37. ios::beg
- 39. ios::cur

```cpp
41. fstream places("places.dat", ios::in | ios::out);
```

```cpp
43. pets.open("pets.dat", ios::in)
fstream open("pets.dat", ios::in);
```

- 49. True
- 51. True
- 53. True
- 55. False
- 57. True
- 59. True
- 61. True
- 63. False

65. File should be opened as

```cpp
fstream file("info.dat", ios::in | ios::out);
or
fstream file:
file.open("info.dat", ios::in | ios::out);
```

67. File access logs must be specified with fstream objects.

69. The file class flag should be ios::in. Also, the get member function cannot be used to read a string.

71. The file class flag should be ios::out. Also, the last line should read
dataFile.write(reinterpret_cast<char *>(&dt), sizeof(dt));

## Chapter 13

- 1. A class describes a data type. An instance of a class is an object of the data type that exists in memory.
- 3. private
- 5. A class is analogous to the blueprint.
- 7. Yes it is. This protects the variables from being directly manipulated by code outside the class, and prevents them from receiving invalid data.
- 9. When the function is for internal processing, but not useful to the program outside the class. In some cases a class may contain member functions that initialize member variables or destroy their contents. These functions should not be accessible by an external part of the program because they be called at the wrong time.
- 11. A default constructor is a constructor that is called without any arguments. It is not to have more than one default constructor.
- 13. executes when the object is created.
- 15. A class's responsibilities are the things the class is responsible for knowing and the actions that the class is responsible for doing.
- 17. procedural programming, object-oriented programming
- 19. object-oriented
- 21. class
- 23. access specifier
- 25. public
- 27. ->
- 29. canine.cpp
- 31. constructor
- 33. constructors
- 35. default
- 37. ~
- 39. default
- 41. constructor, destructor

```cpp
43. class Circle
{
    private:
        double radius;
    public:
        void setRadius(double r)
        { radius = r; }
        double getRadius()
        { return radius; }
        double getArea()
        { return 3.14159 * radius * radius; }
}
```

```cpp
45. class Circle
{
    private:
        double radius;
    public:
        Circle()
        { radius = 0.0; }
        Circle(double r)
        { radius = r; }
        void setRadius(double r)
        { radius = r; }
        double getRadius()
        { return radius; }
        double getArea()
        { return 3.14159 * radius * radius; }
}
```

- 47. Circle[5] = { 12, 7, 9, 14, 8 };

| Animal | Medication | Nurse |
| :--- | :--- | :--- |
| Doctor | Invoice | Customer |
| Patient | Client |

- 51. False
- 53. False
- 55. False
- 57. True
- 59. False
- 61. True
- 49.
- 63. True
- 65. True
- 67. False
- 69. True
- 71. False There should not be a colon after the word Circle. Colons should appear after the words private and public. A semicolon should appear after the closing brace.
- 75. The semicolon should not appear after the word DumbBell. The function header for setWeight should appear as:

```cpp
void DumbBell::setWeight(int w)
```

The line reads:
DumbBell(200);
should read:

```cpp
bar.setWeight(200);
```

bar.weight cannot be accessed outside of the class because no access specifier appeared before the class, making the private to the class by default. This means the statement will not work.

## Chapter 14

- 1. Each class object has its own copy of the class's instance member variables. All objects of the class share the class's static member variables.
- 3. Outside the class declaration.
- 5. Because every member function of the first class would have access to the class's private member variables.
- 7. When an object is initialized with another object's data.
- 9. When an object has a pointer as a member, and it points to a chunk of dynamically allocated memory. When this object is copied to another object via member assignment, the receiver's pointer will point to the same chunk of memory.
- 11. It is a copy constructor that is automatically created for a class, and performs assignment.
- 13. The object on the right side of the = operator in the statement that called the overloaded function operator.
- 15. A dummy parameter is used in the function header of a postfix operator.
- 17. A Boolean value.
- 19. Place the keyword :: before the variable declaration (inside the class). Then, place a definition of the variable outside the class.
- 21. 3, 3, 1, 0, Thing::putThing(2);

## Appendix O: Solutions to Odd Numbered Review Questions

- 23. To inform the compiler of the class's existence before it reaches the class's definition.
- 25. Because the parameter variable is created in memory when the function executes, and is initialized with the argument object. This causes the constructor to be called.
- 27. outside
- 29. before
- 31. forward declaration
- 33. copy constructor
- 35. overloaded
- 37. aggregation
- 39. Bird Bird::operator=(const Bird &right)
- 41. bool Yen::operator=(const Yen &right)
- 43. Collection Collection::operator[](const Collection &sub)
- 45. True
- 47. False
- 49. True
- 51. True
- 53. True
- 55. False
- 57. True
- 59. The copy constructor's parameter should be a reference variable.
- 61. The overloaded + function header should read

```cpp
void operator+(const Point &right)
```

- 63. The float conversion function header should read

```cpp
operator float()
```

## Chapter 15

- 1. When one object is a specialized version of another object, there is an "is a" relationship between them. This indicates that one class is "a" specialized version of the other class.
- 3. Base class access specification specifies how members of the base class are inherited by the derived class. Member access specification specifies how members may be accessed by code outside the class.
- 5. No.
- 7. When a derived class has a function with the same name as a base class function, and the base class function is not virtual, it is said that the function is redefined in the derived class. If the base class's function is however, it is said that the function is overridden.
- 9. An abstract base class is not instantiated, but serves as a base class for other classes. The abstract base class represents the generic, abstract form of all the classes that are derived from it. It is abstract when it has one or more virtual functions.

## Appendix O: Solutions to Odd Numbered Review Questions

- 11. Dog
- 13. public
- 15. private
- 17. inaccessible, protected, protected
- 19. members
- 21. last
- 23. The base class version.
- 25. static
- 27. polymorphism
- 29. abstract base class
- 31. chain
- 33. override or redefine
- 35. class SoundSystem : public CDplayer, public Tuner, public CasettePlayer
- 37. class B
{
    private:
        int m;
    protected:
        int n;
    public:
        void setM(int);
        int getM();
        void setN(int);
        int getN();
        virtual int calc()
        { return m * n; }
}
class D : public B
{
protected:
        float q;
        float r;
    public:
        void setQ(float);
        float getQ();
        void setR(float);
        float getR();
        virtual float calc()
        { return q * r; }
};

- 39. True
- 41. True
- 43. False
- 45. False
- 47. True
