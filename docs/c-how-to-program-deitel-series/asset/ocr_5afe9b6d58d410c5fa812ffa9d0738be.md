```
```cpp
// function to retrieve the course name
string GradeBook::getCourseName() const
{
   return courseName;
} // end function getCourseName

// display a welcome message to the GradeBook user
void GradeBook::displayMessage() const
{
   cout << "Welcome to the grade book for\n" << getCourseName() << "\n\n"
        << endl;
} // end function displayMessage

// determine class average based on 10 grades entered by user
void GradeBook::determineClassAverage() const
{
   // initialization phase
   int total = 0; // sum of grades entered by user
   unsigned int gradeCounter = 0; // number of grades entered

   // processing phase
   // prompt for input and read grade from user
   cout << "Enter grade or -1 to quit: ";
   int grade = 0; // grade value
   cin >> grade; // input grade or sentinel value

   // loop until sentinel value read from user
   while (grade != -1) // while grade is not -1
   {
      total = total + grade; // add grade to total
      gradeCounter = gradeCounter + 1; // increment counter

      // prompt for input and read next grade from user
      cout << "Enter grade or -1 to quit: ";
      cin >> grade; // input grade or sentinel value
   } // end while

   // termination phase
   if (gradeCounter != 0) // if user entered at least one grade...
   {
      // calculate average of all grades entered
      double average = static_cast< double > (total) / gradeCounter;

      // display total and average (with two digits of precision)
      cout << "\nTotal of all " << gradeCounter << " grades entered is "
           << total << endl;
      cout << setprecision(2) << fixed;
      cout << "Class average is " << average << endl;
   } // end if
```
```

Fig. 4.13 | Class average problem using sentinel-controlled repetition: GradeBook source code file. (Part 2 of 3.)