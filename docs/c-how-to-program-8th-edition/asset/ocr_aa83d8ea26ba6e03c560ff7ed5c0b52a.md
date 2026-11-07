![](bbox=[0.157, 0.116, 0.214, 0.16])

# Software Engineering Observation 3.1

Generally, data members should be declared private and member functions should be declared public.

![](bbox=[0.157, 0.19, 0.214, 0.236])

# Error-Prevention Tip 3.1

Make the data members of a class private and the member functions of the class public. This facilitates debugging because problems with data manipulations are localized to either the class’s member functions or the friends of the class.

![](bbox=[0.157, 0.284, 0.214, 0.329])

# Common Programming Error 3.2

An attempt by a function, which is not a member of a particular class (or a friend of that class) to access a private member of that class is a compilation error.

The default access for class members is private so all members after the class header and before the first access specifier (if there are any) are private. The access specifiers public and private may be repeated, but this is unnecessary and can be confusing. Declaring data members with access specifier private is known as data hiding. When a program creates a GradeBook object, data member courseName is encapsulated (hidden) in the object and can be accessed only by member functions of the object’s class. In class GradeBook, member functions setCourseName and getCourseName manipulate the data member courseName directly.

# Member Functions setCourseName and getCourseName

Member function setCourseName (lines 14–17) does not return any data when it completes its task, so its return type is void. The member function receives one parameter—name—which represents the course name that will be passed to it as an argument (as we’ll see in line 50 of main). Line 16 assigns name to data member courseName. In this example, setCourseName does not validate the course name—i.e., the function does not check that the course name adheres to any particular format or follows any other rules regarding what a “valid” course name looks like. Suppose, for instance, that a university can print student transcripts containing course names of only 25 characters or fewer. In this case, we might want class GradeBook to ensure that its data member courseName never contains more than 25 characters. We discuss validation in Section 3.8.

Member function getCourseName (lines 20–23) returns a particular GradeBook object’s courseName. The member function has an empty parameter list, so it does not require additional data to perform its task. The function specifies that it returns a string. When a function that specifies a return type other than void is called and completes its task, the function uses a return statement (as in line 22) to return a result to its calling function. For example, when you go to an automated teller machine (ATM) and request your account balance, you expect the ATM to give you back a value that represents your balance. Similarly, when a statement calls member function getCourseName on a GradeBook object, the statement expects to receive the GradeBook’s course name (in this case, a string, as specified by the function’s return type).

If you have a function square that returns the square of its argument, the statement

```
result = square( 2 );
```