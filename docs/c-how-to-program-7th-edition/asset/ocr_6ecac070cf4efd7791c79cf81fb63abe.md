```
~~~cpp
11   setCourseName( name ); // validate and store courseName
12 } // end GradeBook constructor
13
14 // function to set the course name;
15 // ensures that the course name has at most 25 characters
16 void GradeBook::setCourseName( string name )
17 {
18   if ( name.length() <= 25 ) // if name has 25 or fewer characters
19      courseName = name; // store the course name in the object
20   else // if name is longer than 25 characters
21   { // set courseName to first 25 characters of parameter name
22      courseName = name.substr( 0, 25 ); // select first 25 characters
23      cout << "Name \"" << name << "\" exceeds maximum length (25).\n"
24         << "Limiting courseName to first 25 characters.\n" << endl;
25   } // end if...else
26 } // end function setCourseName
27
28 // function to retrieve the course name
29 string GradeBook::getCourseName()
30 {
31   return courseName;
32 } // end function getCourseName
33
34 // display a welcome message to the GradeBook user
35 void GradeBook::displayMessage()
36 {
37   cout << "Welcome to the grade book for\n" << getCourseName() << "!"
38        << endl;
39 } // end function displayMessage
40
41 // determine class average based on 10 grades entered by user
42 void GradeBook::determineClassAverage()
43 {
44   int total; // sum of grades entered by user
45   int gradeCounter; // number of the grade to be entered next
46   int grade; // grade value entered by user
47   int average; // average of grades
48
49   // initialization phase
50   total = 0; // initialize total
51   gradeCounter = 1; // initialize loop counter
52
53   // processing phase
54   while ( gradeCounter <= 10 ) // loop 10 times
55   {
56      cout << "Enter grade: "; // prompt for input
57      cin >> grade; // input next grade
58      total = total + grade; // add grade to total
59      gradeCounter = gradeCounter + 1; // increment counter by 1
60   } // end while
61
~~~
```

Fig. 4.9 | Class average problem using counter-controlled repetition: GradeBook source code file. (Part 2 of 3.)