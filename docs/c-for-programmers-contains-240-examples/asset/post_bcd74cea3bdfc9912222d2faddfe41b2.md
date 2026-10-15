
## Member Functions setCourseName and getCourseName

Member function setCourseName (defined in lines 19–22) does not return any data when it completes its task, so its return type is void. The member function receives one parameter—name—which represents the course name that will be passed to it as an argument (as we’ll see in line 55 of main). Line 21 assigns name to data member courseName. In this example, setCourseName does not attempt to validate the course name—i.e., the function does not check that the course name adheres to any particular format or follows any other rules regarding what a “valid” course name looks like. Suppose, for instance, that a university can print student transcripts containing course names of only 25 characters or fewer. In this case, we might want class GradeBook to ensure that its data member courseName never contains more than 25 characters. We discuss basic validation techniques in Section 3.10.

Member function getCourseName (defined in lines 25–28) returns a particular GradeBook object’s courseName. The member function has an empty parameter list, so it does not require additional data to perform its task. The function specifies that it returns a string. When a function that specifies a return type other than void is called and completes its task, the function returns a result to its calling function. For example, when you go to an automated teller machine (ATM) and request your account balance, you expect the ATM to give you back a value that represents your balance. Similarly, when a statement calls member function getCourseName on a GradeBook object, the statement expects to receive the GradeBook’s course name (in this case, a string, as specified by the function’s return type). If you have a function square that returns the square of its argument, the statement

```
result = square( 2 );
```

returns 4 from function square and assigns to variable result the value 4. If you have a function maximum that returns the largest of three integer arguments, the statement

```
biggest = maximum( 27, 114, 51 );
```

returns 114 from function maximum and assigns to variable biggest the value 114.

### Common Programming Error 3.7

> Forgetting to return a value from a function that is supposed to return a value is a compilation error.

Note that the statements in lines 21 and 27 each use variable courseName (line 39) even though it was not declared in any of the member functions. We can use courseName in the member functions of class GradeBook because courseName is a data member of the class. Also note that the order in which member functions are defined does not determine when they are called at execution time. So member function getCourseName could be defined before member function setCourseName.

## Member Function displayMessage

Member function displayMessage (lines 31–37) does not return any data when it completes its task, so its return type is void. The function does not receive parameters, so its parameter list is empty. Lines 35–36 output a welcome message that includes the value of data member courseName. Line 35 calls member function getCourseName to obtain the value of courseName. Note that member function displayMessage could also access data member courseName directly, just as member functions setCourseName and getCourseName do. We explain shortly why we choose to call member function getCourseName to obtain the value of courseName.

## Testing Class GradeBook

The main function (lines 43–60) creates one object of class GradeBook and uses each of its member functions. Line 46 creates a GradeBook object named myGradeBook. Lines 49–50 display the initial course name by calling the object’s getCourseName member function. Note that the first line of the output does not show a course name, because the object’s courseName data member (i.e., a string) is initially empty—by default, the initial value of a string is the so-called empty string, i.e., a string that does not contain any characters. Nothing appears on the screen when an empty string is displayed.

Line 53 prompts the user to enter a course name. Local string variable nameOfCourse (declared in line 45) is set to the course name entered by the user, which is obtained by the call to the getline function (line 54). Line 55 calls object myGradeBook’s setCourseName member function and supplies nameOfCourse as the function’s argument. When the function is called, the argument’s value is copied to parameter name (line 19) of member function setCourseName (lines 19–22). Then the parameter’s value is assigned to data member courseName (line 21). Line 57 skips a line in the output; then line 58 calls object myGradeBook’s displayMessage member function to display the welcome message containing the course name.

## Software Engineering with Set and Get Functions

A class’s private data members can be manipulated only by member functions of that class (and by “friends” of the class, as we’ll see in Chapter 10). So a client of an object—that is, any class or function that calls the object’s member functions from outside the object—calls the class’s public member functions to request the class’s services for particular objects of the class. This is why the statements in function main (Fig. 3.5, lines 43–60) call member functions setCourseName, getCourseName and displayMessage on a GradeBook object.

Classes often provide public member functions to allow clients of the class to set (i.e., assign values to) or get (i.e., obtain the values of) private data members. The names of these member functions need not begin with set or get, but this naming convention is common. In this example, the member function that sets the courseName data member is called setCourseName, and the member function that gets the value of the courseName data member is called getCourseName. Note that set functions are also sometimes called mutators (because they mutate, or change, values), and get functions are also sometimes called accessors (because they access values).

Recall that declaring data members with access specifier private enforces data hiding. Providing public set and get functions allows clients of a class to access the hidden data, but only indirectly. The client knows that it is attempting to modify or obtain an object’s data, but the client does not know how the object performs these operations. In some cases, a class may internally represent a piece of data one way, but expose that data to clients in a different way. For example, suppose a Clock class represents the time of day as a private int data member time that stores the number of seconds since midnight. However, when a client calls a Clock object’s getTime member function, the object could return the time with hours, minutes and seconds in a string in the format "HH:MM:SS". Similarly, suppose the Clock class provides a set function named setTime that takes a string parameter in the "HH:MM:SS" format. Using string capabilities presented in Chapter 18, the setTime function could convert this string to a number of seconds, which the function stores in its private data member. The set function could also check that the value it receives represents a valid time (e.g., "12:30:45" is valid but "42:85:70" is not). The set and get functions allow a client to interact with an object, but the object’s private data remains safely encapsulated (i.e., hidden) in the object itself.

The set and get functions of a class also should be used by other member functions within the class to manipulate the class’s private data, although these member functions can access the private data directly. In Fig. 3.5, member functions setCourseName and getCourseName are public member functions, so they are accessible to clients of the class, as well as to the class itself. Member function displayMessage calls member function getCourseName to obtain the value of data member courseName for display purposes, even though displayMessage can access courseName directly—accessing a data member via its get function creates a better, more robust class (i.e., a class that is easier to maintain and less likely to stop working). If we decide to change the data member courseName in some way, the displayMessage definition will not require modification—only the bodies of the get and set functions that directly manipulate the data member will need to change. For example, suppose we decide that we want to represent the course name as two separate data members—courseNumber (e.g., "CS101") and courseTitle (e.g., "Introduction to C++ Programming"). Member function displayMessage can still issue a single call to member function getCourseName to obtain the full course name to display as part of the welcome message. In this case, getCourseName would need to build and return a string containing the courseNumber followed by the courseTitle. Member function displayMessage would continue to display the complete course title "CS101 Introduction to C++ Programming," because it is unaffected by the change to the class’s data members. The benefits of calling a set function from another member function of a class will become clear when we discuss validation in Section 3.10.

### Good Programming Practice 3.4

> Always try to localize the effects of changes to a class’s data members by accessing and manipulating the data members through their get and set functions. Changes to the name of a data member or the data type used to store a data member then affect only the corresponding get and set functions, but not the callers of those functions.

### Software Engineering Observation 3.3

> The class designer need not provide set or get functions for each private data item; these capabilities should be provided only when appropriate. If a service is useful to the client code, that service should typically be provided in the class’s public interface.

## GradeBook’s UML Class Diagram with a Data Member and set and get Functions

Figure 3.6 contains an updated UML class diagram for the version of class GradeBook in Fig. 3.5. This diagram models GradeBook’s data member courseName as an attribute in the middle compartment. The UML represents data members as attributes by listing the attribute name, followed by a colon and the attribute type. The UML type of attribute courseName is String, which corresponds to string in C++. Data member courseName is private in C++, so the class diagram lists a minus sign (–) in front of the corresponding attribute’s name. The minus sign in the UML is equivalent to the private access specifier
