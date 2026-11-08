
![](img/43c5f409f9b17790a628c4b4df854b61_378_0.png)

**Figure 13.14:** Describing Operations, Requests, and Methods

Similar to a C structure, a class is an abstract data type. It is a representation of objects and the sets of operations that may be applied on the objects. A class consists of data members and methods. The main purpose of a class is to hold the data or information. This is achieved along with the attributes, which are also called data members. The member functions determine the behavior from the class.

The general definition of a class is shown in Listing 13.1:

**Listing 13.1: Showing the Definition of a Class**

```cpp
public class Employee
{
}
```

In the preceding code snippet, we have defined a public class Employee, which is empty. This implies that the class does not contain any data member or method associated with it.

Using the preceding class definition, we can create the *Employee* object, *objectEmployee*, as follows:

```cpp
Employee objectEmployee = new Employee();
```

Following is the complete blueprint of a class:

```cpp
class class_name
{
    Data Members;
    Methods;
};
```

**Listing 13.2: Showing the Code Snippet for a Well-Structured Class**

```cpp
class A
{
    int i ;
    char *string;
    void func (int , char *);
    int g_func() ;
};

class Circle
{
    int radius;
    int xcentre;
    int ycentre;
    int GetRadius ();
    int SetData();
    int GetXCentre ();
    int GetYCentre ();
};
```

Designing a class is an art and each designer uses different implementations to identify classes. However, according to the Object-Oriented Design Principles, we must follow five principles to design a class, which are shown in Figure 13.15:

![](img/43c5f409f9b17790a628c4b4df854b61_379_0.png)

Following is the explanation of each of these principles:

- **Single Responsibility Principle**—States that a class should have only one reason to change. This helps in identifying and recognizing the classes during the design phase. This also helps in identifying all the possible ways in which a class can evolve.
- **Open Closed Principle**—States that a class must be designed in a way that it should remain open for extensions and close for modifications. In other words, classes should be designed in a manner that when new functionalities are added to them, there should be minimal changes in the code.
- **Liskov Substitution Principle**—States that the derived classes should be completely substitutable for their base classes. In other words, if any module of a program is using a base class, then the reference to the base class can easily be replaced with a derived class. This should not affect the functionality of that particular module.
- **Dependency Inversion Principle**—States that the high-level modules should not depend on the low-level modules but both should depend upon abstractions. On the other hand, abstractions should not depend upon the details but details should depend upon abstractions.
- **Interface Segregation Principle**—States that users should not be compelled to depend upon the interfaces that they do not use. To implement this, a lot of time should be invested during the design phase to make the design flexible.

To summarize the discussion over classes, consider the code snippet given in Listing 13.3:

**Listing 13.3: Implementing a Class**

```cpp
class Employee {
public:
    int GetSalary();
    void SetSalary (int NewSalary);
    void PromoteEmployee (char NewDesignation, int NewSalary);
    void ChangeProject (char* NewProject);
    void Work();
private:
    char Name[30];
    int Salary;
    char Designation [30];
    char ProjectName [50];
};
```

The properties of the Employee class are name, salary, designation, and an associated project. These properties are static; however, the values that these properties can hold are dynamic. The behavior of an object is captured in terms of operation. The PromoteEmployee() operation changes the state of object; whereas, the GetSalary() operation does not alter the state of object.

After learning about classes and objects, let's discuss constructors, in detail.

## Constructors

Constructors are member functions with the same name as that of the class and are called automatically at the time of object creation. These are used to initialize the members of a class; therefore, they turn raw memory into objects. Constructors have no return type, but they can be overloaded. Consider the code snippet given in Listing 13.4:

**Listing 13.4:** Showing the Example of a Constructor

```cpp
class A
{
    int b, c;
    public:
    A();                      //default constructor
    A(int, int);              //overloaded constructor
};

A::A()
{
    b=10;
    c=20;
}

A::A(int k, int j)
{
    b=k;
    c=j;
}
```

In the class A, we have declared a default constructor as A() and the overloaded constructor as A(int, int).

Next, let's learn about the copy constructors, in detail.

### Copy Constructors

Copy constructor of a class is a constructor that makes the copy of an object of the class. A copy constructor helps in creating a new object from an existing one by initialization. In case we do not declare a copy constructor, the C++ compiler will implicitly declare it; however, this will be an inline public member. A declaration of type A::A(const A & right) is an example of a copy constructor.

There are certain rules that need to be kept in mind while working with both constructors and copy constructors. The set of rules are as follows:

1. A copy constructor can accept only one argument of reference to the same class type. However, more arguments can be supplied, but all those should be default.
2. An error is generated if we specify a copy constructor with the first argument as an object and not a reference.
3. The compiler generates a default copy constructor if it is not provided.
4. Constructors of base classes are not inherited by derived classes (except in cases of virtual derivation).

```cpp
void Person :: Set(char *_name, int _age){
strcpy(name, _name);
*age = _age;
}
char *Person :: GetName(){
return name;
}
int Person :: GetAge(){
return *age;
}
void Person :: Display(){
cout << "Name : " << name << endl;
cout << "Age : " << *age << endl;
}
void main(){
    Person programmer;
    programmer.Set("Rahim", 10);
    programmer.Display();
    Person manager(programmer);
    cout << "................................" << endl;
    manager.Display();
    programmer.Display();
    cout << "................................" << endl;
    programmer.Set("Jasim", 50);
    programmer.Display();
    manager.Display();
    getch();
}
```

The output of the preceding code is as follows:

```text
Name : Rahim
Age : 10
................................
Name : Rahim
Age : 10
Name : Rahim
Age : 10
................................
Name : Jasim
Age : 50
Name : Rahim
Age : 10
```

As mentioned, a copy constructor provided by the compiler carries out member-wise copy. Therefore, if a class contains pointers or arrays, then we should define our own copy constructor; otherwise, default copy constructor will be used.

### Public, Private, and Protected Constructors

Sometimes, we do not want other users to use our constructors. In such cases, we may define the access specification for a constructor. Therefore, the constructor of a class can be public, private, or protected. A public constructor can be used by other users outside its class. A protected constructor can be used only by the users belonging to that class and by the users of those classes that are derived from that class. A private constructor can only be used by the users of its class only. A class with private constructor cannot be initialized by any function other than the member functions of its class. It can be used to create a singleton class, which is a popular design pattern in C++.
