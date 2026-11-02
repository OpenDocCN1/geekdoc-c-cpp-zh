of reusable software components, such as type `string` provided in the C++ Standard Library and user-defined types like class `GradeBook`.

Our next example separates the code from Fig. 16.7 into two files—`GradeBook.h` (Fig. 16.9) and `fig16_10.cpp` (Fig. 16.10). As you look at the header in Fig. 16.9, notice that it contains only the `GradeBook` class definition (lines 7–38) and the headers on which the class depends. The `main` function that *uses* class `GradeBook` is defined in the source-code file `fig16_10.cpp` (Fig. 16.10) in lines 8–18. To help you prepare for the larger programs you'll encounter later in this book and in industry, we often use a separate source-code file containing function `main` to test our classes (this is called a driver program). You'll soon learn how a source-code file with `main` can use the class definition found in a header to create objects of a class.

```
```cpp
1 // Fig. 16.9: GradeBook.h
2 // GradeBook class definition in a separate file from main.
3 #include <iostream>
4 #include <string> // class GradeBook uses C++ standard string class
5
6 // GradeBook class definition
7 class GradeBook
8 {
9 public:
10    // constructor initializes courseName with string supplied as argument
11    explicit GradeBook( std::string name )
12       : courseName( name ) // member initializer to initialize courseName
13    { // empty body
14    } // end GradeBook constructor
15
16    // function to set the course name
17    void setCourseName( std::string name )
18    {
19       courseName = name; // store the course name in the object
20    } // end function setCourseName
21
22    // function to get the course name
23    std::string getCourseName() const
24    {
25       return courseName; // return object's courseName
26    } // end function getCourseName
27
28    // display a welcome message to the GradeBook user
29    void displayMessage() const
30    {
31       // call getCourseName to get the courseName
32       std::cout << "Welcome to the grade book for\n" << getCourseName()
33          << "!" << std::endl;
34    } // end function displayMessage
35 private:
36    std::string courseName; // course name for this GradeBook
37 }; // end class GradeBook
```
```

**Fig. 16.9** | GradeBook class definition in a separate file from main.