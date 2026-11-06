```
```cpp
// Fig. 7.13: GradeBook.h
// Definition of class GradeBook that uses an array to store test grades.
#include <string>
#include <array>
#include <iostream>
#include <iomanip> // parameterized stream manipulators

// GradeBook class definition
class GradeBook {
public:
   // constant number of students who took the test
   static const size_t students[10]; // note public data

   // constructor initializes courseName and grades array
   GradeBook(const std::string& name,
      const std::array<int, students>& gradesArray)
      : courseName{name}, grades{gradesArray} {
   }

   // function to set the course name
   void setCourseName(const std::string& name) {
      courseName = name; // store the course name
   }

   // function to retrieve the course name
   const std::string& getCourseName() const {
      return courseName;
   }

   // display a welcome message to the GradeBook user
   void displayMessage() const {
      // call getCourseName to get the name of this GradeBook's course
      std::cout << "Welcome to the grade book for\n" << getCourseName()
         << "!" << std::endl;
   }

   // perform various operations on the data (none modify the data)
   void processGrades() const {
      outputGrades(); // output grades array

      // call function getAverage to calculate the average grade
      std::cout << std::setprecision(2) << std::fixed;
      std::cout << "\nClass average is " << getAverage() << std::endl;

      // call functions getMinimum and getMaximum
      std::cout << "Lowest grade is " << getMinimum()
         << "\nHighest grade is " << getMaximum() << std::endl;
```
```