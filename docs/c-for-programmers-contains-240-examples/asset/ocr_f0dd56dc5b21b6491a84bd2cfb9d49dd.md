Fig. 4.12 | Examination-results problem: Analysis header file. (Part 2 of 2.)

```
8  public:
9      void processExamResults(); // process 10 students' examination results
10 }; // end class Analysis
```

```
1  // Fig. 4.13: Analysis.cpp
2  // Member-function definitions for class Analysis that
3  // analyzes examination results.
4  #include <iostream>
5  using std::cout;
6  using std::cin;
7  using std::endl;
8  
9  // include definition of class Analysis from Analysis.h
10 #include "Analysis.h"
11 
12 // process the examination results of 10 students
13 void Analysis::processExamResults()
14 {
15     // initializing variables in declarations
16     int passes = 0; // number of passes
17     int failures = 0; // number of failures
18     int studentCounter = 1; // student counter
19     int result; // one exam result (1 = pass, 2 = fail)
20 
21     // process 10 students using counter-controlled loop
22     while ( studentCounter <= 10 )
23     {
24         // prompt user for input and obtain value from user
25         cout << "Enter result (1 = pass, 2 = fail): ";
26         cin >> result; // input result
27 
28         // if...else nested in while
29         if ( result == 1 )      // if result is 1,
30             passes = passes + 1;    // increment passes;
31         else                    // else result is not 1, so
32             failures = failures + 1; // increment failures
33 
34         // increment studentCounter so loop eventually terminates
35         studentCounter = studentCounter + 1;
36     } // end while
37 
38     // termination phase; display number of passes and failures
39     cout << "Passed " << passes << "\nFailed " << failures << endl;
40 
41     // determine whether more than eight students passed
42     if ( passes > 8 )
43         cout << "Raise tuition " << endl;
44 } // end function processExamResults
```

Fig. 4.13 | Examination-results problem: Nested control statements in Analysis source code file.