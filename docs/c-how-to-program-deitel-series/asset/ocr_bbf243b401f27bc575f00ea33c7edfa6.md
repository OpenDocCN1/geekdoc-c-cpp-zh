```
```cpp
// call function getAverage to calculate the average grade
cout << setprecision( 2 ) << fixed;
cout << "\\nClass average is " << getAverage() << endl;

// call functions getMinimum and getMaximum
cout << "Lowest grade is " << getMinimum() << "\\nHighest grade is "
     << getMaximum() << endl;

// call function outputBarChart to print grade distribution chart
outputBarChart();
} // end function processGrades

// find minimum grade
int GradeBook::getMinimum() const
{
   int lowestGrade = 100; // assume lowest grade is 100

   // loop through grades array
   for ( int grade : grades )
   {
      // if current grade lower than lowGrade, assign it to lowGrade
      if ( grade < lowGrade )
         lowGrade = grade; // new lowest grade
   } // end for

   return lowGrade; // return lowest grade
} // end function getMinimum

// find maximum grade
int GradeBook::getMaximum() const
{
   int highGrade = 0; // assume highest grade is 0

   // loop through grades array
   for ( int grade : grades )
   {
      // if current grade higher than highGrade, assign it to highGrade
      if ( grade > highGrade )
         highGrade = grade; // new highest grade
   } // end for

   return highGrade; // return highest grade
} // end function getMaximum

// determine average grade for test
double GradeBook::getAverage() const
{
   int total = 0; // initialize total

   // sum grades in array
   for ( int grade : grades )
      total += grade;
```
```

Fig. 7.16 | GradeBook class member functions manipulating an array of grades. (Part 2 of 3.)