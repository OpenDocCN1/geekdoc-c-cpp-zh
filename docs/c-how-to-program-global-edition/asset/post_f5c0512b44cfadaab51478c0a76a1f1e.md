
same name as the class, so that the compiler can distinguish it from the class’s other member functions. An important difference between constructors and other functions is that constructors cannot return values, so they cannot specify a return type (not even void). Normally, constructors are declared public. You can also create classes with more than one constructor using function overloading.

C++ automatically calls a constructor for each object that’s created, which helps ensure that objects are initialized properly before they’re used in a program. The constructor call occurs when the object is created. If a class does not explicitly include constructors, the compiler provides a default constructor with no parameters. For example, when line 41 of Fig. 16.5 creates a GradeBook object, the default constructor is called. The default constructor provided by the compiler creates a GradeBook object without giving any initial values to the object’s fundamental type data members. For data members that are objects of other classes, the default constructor implicitly calls each data member’s default constructor to ensure that the data member is initialized properly. This is why the string data member courseName (in Fig. 16.5) was initialized to the empty string—the default constructor for class string sets the string’s value to the empty string.

In the example of Fig. 16.7, we specify a course name for a GradeBook object when the object is created (e.g., line 47). In this case, the argument "CS101 Introduction to C++ Programming" is passed to the GradeBook object’s constructor (lines 14–18) and used to initialize the courseName. Figure 16.7 defines a modified GradeBook class containing a constructor with a string parameter that receives the initial course name.

```cpp
1  // Fig. 16.7: fig16_07.cpp
2  // Instantiating multiple objects of the GradeBook class and using
3  // the GradeBook constructor to specify the course name
4  // when each GradeBook object is created.
5  #include <iostream>
6  #include <string> // program uses C++ standard string class
7  using namespace std;
8
9  // GradeBook class definition
10 class GradeBook
11 {
12 public:
13    // constructor initializes courseName with string supplied as argument
14    explicit GradeBook( string name )
15        : courseName( name ) // member initializer to initialize courseName
16    {
17    } // end GradeBook constructor
18
19    // function to set the course name
20    void setCourseName( string name )
21    {
22        courseName = name; // store the course name in the object
23    } // end function setCourseName
```

**Fig. 16.7 |** Instantiating multiple objects of the GradeBook class and using the GradeBook constructor to specify the course name when each GradeBook object is created. (Part 1 of 2.)

```
// function to get the course name
string getCourseName() const
{
    return courseName; // return object's courseName
} // end function getCourseName

// display a welcome message to the GradeBook user
void displayMessage() const
{
    // call getCourseName to get the courseName
    cout << "Welcome to the grade book for\n" << getCourseName()
         << "!" << endl;
} // end function displayMessage
private:
    string courseName; // course name for this GradeBook
}; // end class GradeBook

// function main begins program execution
int main()
{
    // create two GradeBook objects
    GradeBook gradeBook1( "CS101 Introduction to C++ Programming" );
    GradeBook gradeBook2( "CS102 Data Structures in C++" );

    // display initial value of courseName for each GradeBook
    cout << "gradeBook1 created for course: " << gradeBook1.getCourseName()
         << "\nGradeBook2 created for course: " << gradeBook2.getCourseName()
         << endl;
} // end main
```

```
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

Fig. 16.7 | Instantiating multiple objects of the GradeBook class and using the GradeBook constructor to specify the course name when each GradeBook object is created. (Part 2 of 2.)

## Defining a Constructor

Lines 14–18 of Fig. 16.7 define a constructor for class GradeBook. The constructor has the same name as its class, GradeBook. A constructor specifies in its parameter list the data it requires to perform its task. When you create a new object, you place this data in the parentheses that follow the object name (as we did in lines 47–48). Line 14 indicates that class GradeBook’s constructor has a string parameter called name. We declared this constructor explicit, because it takes a single parameter—this is important for subtle reasons that you’ll learn in Section 18.13. For now, just declare all single-parameter constructors explicit. Line 14 does not specify a return type, because constructors cannot return values (or even void). Also, constructors cannot be declared const (because initializing an object modifies it).

The constructor uses a member-initializer list (line 15) to initialize the courseName data member with the value of the constructor’s parameter name. Member initializers appear between a constructor’s parameter list and the left brace that begins the constructor.

constructor's body. The member initializer list is separated from the parameter list with a colon (:). A member initializer consists of a data member's variable name followed by parentheses containing the member's initial value. In this example, courseName is initialized with the value of the parameter name. If a class contains more than one data member, each data member's initializer is separated from the next by a comma. The member initializer list executes before the body of the constructor executes. You can perform initialization in the constructor's body, but as you'll learn later it's more efficient to do it with member initializers, and some types of data members must be initialized this way.

Notice that both the constructor (line 14) and the setCourseName function (line 21) use a parameter called name. You can use the same parameter names in different functions because the parameters are local to each function—they do not interfere with one another.

### Testing Class GradeBook

Lines 44–54 of Fig. 16.7 define the main function that tests class GradeBook and demonstrates initializing GradeBook objects using a constructor. Line 47 creates and initializes GradeBook object gradeBook1. When this line executes, the GradeBook constructor (lines 14–18) is called with the argument "CS101 Introduction to C++ Programming" to initialize gradeBook1's course name. Line 48 repeats this process for GradeBook object gradeBook2, this time passing the argument "CS102 Data Structures in C++" to initialize gradeBook2's course name. Lines 51–52 use each object's getCourseName member function to obtain the course names and show that they were indeed initialized when the objects were created. The output confirms that each GradeBook object maintains its own data member courseName.

### Ways to Provide a Default Constructor for a Class

Any constructor that takes no arguments is called a default constructor. A class can get a default constructor in one of several ways:

- 1. The compiler *implicitly* creates a default constructor in every class that does *not* have any user-defined constructors. The default constructor does *not* initialize the class's data members, but *does* call the default constructor for each data member that's an object of another class. An uninitialized variable contains an undefined ("garbage") value.
- 2. You *explicitly* define a constructor that takes no arguments. Such a default constructor will call the default constructor for each data member that's an object of another class and will perform additional initialization specified by you.
- 3. If you *define* any constructors with arguments, C++ will *not* implicitly create a default constructor for that class. We'll show later that C++11 allows you to force the compiler to create the default constructor even if you've defined non-default constructors.

![](img/bf54db922e6fa8319cba11069e785521_631_0.png)

For each version of class GradeBook in Fig. 16.1, Fig. 16.3 and Fig. 16.5 the compiler *implicitly* defined a default constructor.

> > **Error-Prevention Tip 16.2**
> > *Unless no initialization of your class's data members is necessary (almost never), provide constructors to ensure that your class's data members are initialized with meaningful values when each new object of your class is created.*
