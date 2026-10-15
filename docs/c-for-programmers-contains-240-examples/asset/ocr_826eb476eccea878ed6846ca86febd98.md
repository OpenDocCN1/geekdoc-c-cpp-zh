```
32 // function to retrieve the course name
33 string GradeBook::getCourseName()
34 {
35     return courseName;
36 } // end function getCourseName
37
38 // display a welcome message to the GradeBook user
39 void GradeBook::displayMessage()
40 {
41     // this statement calls getCourseName to get the
42     // name of the course this GradeBook represents
43     cout << "Welcome to the grade book for\n" << getCourseName() << "!"
44         << endl;
45 } // end function displayMessage
46
47 // perform various operations on the data
48 void GradeBook::processGrades()
49 {
50     // output grades array
51     outputGrades();
52
53     // call function getAverage to calculate the average grade
54     cout << "\nClass average is " << setprecision( 2 ) << fixed <<
55         getAverage() << endl;
56
57     // call functions getMinimum and getMaximum
58     cout << "Lowest grade is " << getMinimum() << "\nHighest grade is "
59         << getMaximum() << endl;
60
61     // call function outputBarChart to print grade distribution chart
62     outputBarChart();
63 } // end function processGrades
64
65 // find minimum grade
66 int GradeBook::getMinimum()
67 {
68     int lowGrade = 100; // assume lowest grade is 100
69
70     // loop through grades array
71     for ( int grade = 0; grade < students; grade++ )
72     {
73         // if current grade lower than lowGrade, assign it to lowGrade
74         if ( grades[ grade ] < lowGrade )
75             lowGrade = grades[ grade ]; // new lowest grade
76     } // end for
77
78     return lowGrade; // return lowest grade
79 } // end function getMinimum
80
81 // find maximum grade
82 int GradeBook::getMaximum()
83 {
84     int highGrade = 0; // assume highest grade is 0
```