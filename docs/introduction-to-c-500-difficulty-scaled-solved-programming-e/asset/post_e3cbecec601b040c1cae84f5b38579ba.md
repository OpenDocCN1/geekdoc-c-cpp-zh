
```cpp
class Network : virtual public School
{
private:
    int courses;
public:
    Network(int num) : courses(num) {}
    virtual void show() const;
};
```

```cpp
void Network::show() const {
    cout << "Net-Courses: " << courses << '\n';
};
```

```cpp
class Student : public Programming, public Network {
private:
    string name;
    int code;
public:
    Student(const string& sch_n, const string& stud_n, int num, int prg_c, int prg_n) : School(sch_n), Programming(prg_c), Network(prg_n), name(std_n), code(num) {
    virtual void show() const;
    }
};
```

```cpp
void Student::show() {
    cout << "Stud:" << name << << << "Code:" << code << '\n';
    Programming::show();
    Network::show();
    School::show();
}
```

Comments: According to the exercise, the base class School should be virtual so that a single object of it is created. The default constructor is added to the School, which the Programming and Network constructors need to call. Since p is a reference to the School and the show() of the Student must be called, we understand that we should define the show() as virtual. To display all the information, we define respective show() in each class, which we call in its body.

C.21.5 Define the Shape class with private members the coordinates of x and y and the virtual function area() to calculate the area. Define the Shape2D class with public access from the Shape with a private member name of the shape. Define the Rect class with public access from the Shape2D with private members length and height of the rectangle. Define the Shape3D class with public access from the Shape with a private member colour of the shape and the pure virtual function vol() to calculate the volume. Define the Sphere class with public access from the Shape3D with private member the radius of the sphere. The Rect and Sphere classes should not be abstract. Add appropriate functions in the classes that so the following program.

```cpp
int main() {
    Sphere(1, 2, "Blue", 3); /* The x member of the Shape sub-object should become 1, the y member should become 2, the colour of the Shape3D sub-object should become Blue and the radius of the sph should become 3. */
    Rect r4(5, "Rect", 6); /* The x member of the Shape sub-object should become 4, the y member should become 5, the name of the Shape2D sub-object should become Rect, the length of r should become 6 and its height 7. */
    Shape *p[2] = {sph, r}; 
    p[0]->show(); /* The program should display the values of the center x as well as the area and volume of the sphere. */
    p[1]->show(); /* The program should display the values of the center x as well as the area of the rectangle. */
    return 0;
}
```

Answer:

```cpp
#include <iostream>
#include <string>
using std::cout;
using std::string;

class Shape {
private:
    float cntr_x;
    float cntr_y;
public:
    Shape(float x, float y) : cntr_x(x), cntr_y(y) {}
    virtual ~Shape() {}
    virtual void show() const { cout << "Cx:" << cntr_x << " "Cy:" << cntr_y << '\n'; }
    virtual void area() const = 0;
};

class Shape2D : public Shape {
private:
    string name;
public:
    Shape2D(float x, float y, const string& n) : Shape(x, y), name(n) {}
};

class Rect : public Shape2D {
private:
    float len;
    float hght;
public:
    Rect(float x, float y, const string& n, float l, float h) : Shape2D(x, y, n), len(l), hght(h) {}
    virtual void area() const { cout << "Area(R):" << len * hght << '\n'; }
    void show() const {
        area();
        Shape::show();
    }
};

class Shape3D : public Shape {
private:
    string col;
public:
    Shape3D(float x, float y, const string& n) : Shape(x, y), col(n) {}
    virtual void vol() const = 0;
};

class Sphere : public Shape3D {
private:
    float rad;
public:
    Sphere(float x, float y, const string& n, float r) : Shape3D(x, y, n), rad(r) {}
    virtual void area() const { cout << "Area:" << 3.14 * rad * rad << '\n'; }
    virtual void vol() const { cout << "Vol:" << (4/3.0)*rad * rad * rad << '\n'; }
    void show() const {
        area();
        vol();
        Shape::show();
    }
};
```

Comments: Since the exercise tells us that the Rect and Sphere classes are not abstract, we understand that they should implement the virtual functions declared in their base classes. Since p is an array of pointers to Shape and information contained in the derived classes should be displayed, we understand that the show() we will define in Shape should be virtual.

# UNSOLVED EXERCISES

U.21.1 Define the A and B classes and the C class which is derived with public access from A and B. Then, define the D class with public access from B. Finally, define the E class with public access from C and D. Suppose that an E object is created (e.g. e). Define the classes in such a way that e contains only sub-object of the B class. In what order do you think the sub-objects of the classes will be created and destroyed? Write a program that implements the inheritance scheme. Each class should contain a constructor and a destructor that display messages so that you can verify your answer about the order in which the objects are created and destroyed. The program should display:
B() A() C() D() E()
E() D() C() A() B()

U.21.2 Define the abstract class named Product which contains the code and the price of the product as protected members. Define the Book class derived with public access from the Product with the private member the publishing firm (of type string). Also, define the Car class derived from public access from the Product with private member horsepower. Add appropriate functions in the classes so that the following program works.

```cpp
int main() {
    Car b(1
// ...
```

U.21.3 Write a program that implements a simplified vehicle application.. Define the Vehicle class with private member name of the owner. Also that the owner owns a car and a motorcycle. Define the Car and Moto classes with public access from the Vehicle with private members, the plate number (of type string) and the insurance cost of each vehicle. Define the Insurance derived from access access the Car and Moto classes with private member the name of the insurance company. When an Insurance object is created a single sub-object of the Vehicle class should be created. Define the f() function that takes a vector of Insurance elements and displays the name of the owner who pays the largest amount, as well as the details of his and the name of the insurance company. Assume that there is only one owner with the highest total cost. Add appropriate functions in the classes so that the following program works.

```cpp
int main() {
    vector<Insurance> v;
    Insurance ins1("Alpha","1.2",10,"3.4",20,"Ins 1");
    Insurance ins2("Beta","5.6",30); /* In this example, for
    name of the owner should become Alpha, the plate number of the
    1.2, the insurance cost 10, the plate number of the motorcycle 3.4,
    the insurance cost 20, and the name of the insurance company Ins 1.
    For each Insurance object a single Vehicle sub-object should be created.
    Create more Insurance objects and store them in v. Then, call f().
    For example, if v contains only these two elements, the program should
    display Beta 5.6 7.8 Ins 2, because the total insurance cost is 30+40=70, which is greater than 10+20 = 30 of the first owner.*/
    return 0;
}
```

# Exceptions

In this chapter we'll discuss about exceptions. Exceptions are an integral part of the C++ language. We are using exceptions to catch and identify problems that may occur during the execution of the program (runtime errors). They are used extensively in the standard library to signal errors. It is important to know how the mechanism of the exceptions works, so that you can integrate them in your programs.

# EXCEPTIONS

As you guess, when a program is running, errors may occur, which, if not handled properly, can lead to a program crash. The traditional error handling technique is to have scattered code that makes each part of the program responsible to handle its own errors. For example, when we use a function we need to check if it was executed successfully. If it fails, the program should have added code to catch the error and handle it. If it returns a value, the typical way to check for an error is:

```cpp
k = f();
if (k == ERROR_VALUE_1)
{
  ...
}
else if (k == ERROR_VALUE_2)
{
  ...
}
else if (k == ERROR_VALUE_N)
{
  ...
}
else // No error happened.
{
  ...
}
```
