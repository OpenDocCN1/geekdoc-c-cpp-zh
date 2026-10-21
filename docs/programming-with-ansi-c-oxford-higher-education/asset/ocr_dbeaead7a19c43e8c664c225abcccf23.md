```
```
{
cout << "Roll number is " << RollNumber << "\n";
cout << "Name is " << Name << "\n";
cout << "Address is " << Address << "\n";
}
};
void main()
{
// See the use of constructor to initialize both objects
student CricketStudent(1, "Brian Lara", "West Indies");
student FootballStudent(2, "David Beckham", "England");
student TennisStudent;
// The following is an explicit call to a constructor function
TennisStudent = student(3, "Steffi Graf", "Germany");
CricketStudent.PrintDetails();
FootballStudent.PrintDetails();
TennisStudent.PrintDetails();
}
```
```



Empty default constructor The empty default constructor for student should be noted. This is now needed because of the statement student TennisStudent; If there is no parameterized constructor, this statement will not have any problem, but if a parameterized constructor is present, then this statement will not be compiled.

Parameterized constructor and rerunning objects If a parameterized constructor is provided, then a default constructor (at times an empty one) should also be provided. This is a prerequisite if the objects are to be defined in the normal way.

> Note If we do not provide any constructor, the C++ compiler provides the effect of a default constructor. If we provide a constructor, be it a default or parameterized constructor, then the C++ compiler will not provide one.

Now, look at the explicit call to the constructor. TennisStudent = student(3, "Steffi Graf", "Germany"); The constructors are usually not called directly; they are almost always called automatically. Moreover, it has been mentioned that constructors do not have a return statement. Here, student() is called similar to a normal function and it seems to be returning an object of type student class. It might be surprising to observe that a function has been defined without a return type specification, with no return statement, though it returns something. Let us try to understand this. A constructor always returns the object for which it is written. It returns the object it has constructed, but cannot return anything else. If any return type is specified in the definition of the constructor, it means (to the compiler) that the intention is to send something else back. It means the same even if a return statement is written in the body of the constructor. So, both are prohibited. Though no return type is specified and the constructor contains no return statements inside the function body, it is always implicitly specified to be the native object.

> The constructor always returns newly created objects without an explicit return statement.