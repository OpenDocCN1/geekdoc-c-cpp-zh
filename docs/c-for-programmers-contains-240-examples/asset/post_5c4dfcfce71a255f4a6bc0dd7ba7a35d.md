
```
17     { 85, 75, 83 },
18     { 91, 94, 100 },
19     { 76, 72, 84 },
20     { 87, 93, 73 } };
21

22     GradeBook myGradeBook(
23     "CS101 Introduction to C++ Programming", gradesArray );
24     myGradeBook.displayMessage();
25     myGradeBook.processGrades();
26     return 0; // indicates successful termination
27 } // end main
```

Welcome to the grade book for
CS101 Introduction to C++ Programming!

The grades are:

|          | Test 1 | Test 2 | Test 3 | Average |
|----------|--------|--------|--------|---------|
| Student 1| 87     | 96     | 70     | 84.33   |
| Student 2| 68     | 87     | 90     | 81.67   |
| Student 3| 94     | 100    | 90     | 94.67   |
| Student 4| 100    | 81     | 82     | 87.67   |
| Student 5| 83     | 65     | 85     | 77.67   |
| Student 6| 78     | 87     | 65     | 76.67   |
| Student 7| 85     | 75     | 83     | 81.00   |
| Student 8| 91     | 94     | 100    | 95.00   |
| Student 9| 76     | 72     | 84     | 77.33   |
| Student 10| 87    | 93     | 73     | 84.33   |

Lowest grade in the grade book is 65
Highest grade in the grade book is 100

Overall grade distribution:
0-9:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69: ***
70-79: ******
80-89: ************
90-99: *********
100: ***

Fig. 7.25 | Creates a GradeBook object using a two-dimensional array of grades, then invokes member function processGrades to analyze them. (Part 2 of 2.)

## 7.11 Introduction to C++ Standard Library Class Template vector

We now introduce C++ Standard Library class template vector, which represents a more robust type of array featuring many additional capabilities. As you'll see in later chapters, C-style pointer-based arrays (i.e., the type of arrays presented thus far) have great potential

for errors. For example, as mentioned earlier, a program can easily “walk off” either end of an array, because C++ does not check whether subscripts fall outside the range of an array. Two arrays cannot be meaningfully compared with equality operators or relational operators. As you’ll see in Chapter 8, pointer variables (known more commonly as pointers) contain memory addresses as their values. Array names are simply pointers to where the arrays begin in memory, and, of course, two arrays will always be at different memory locations. When an array is passed to a general-purpose function designed to handle arrays of any size, the size of the array must be passed as an additional argument. Furthermore, one array cannot be assigned to another with the assignment operator(s)—array names are const pointers, and, as you’ll see in Chapter 8, a constant pointer cannot be used on the left side of an assignment operator. These and other capabilities certainly seem like “naturals” for dealing with arrays, but C++ does not provide such capabilities. However, the C++ Standard Library provides class template vector to allow programmers to create a more powerful and less error-prone alternative to arrays. In Chapter 11, Operator Overloading; String and Array Objects, we present the means to implement such array capabilities as those provided by vector. You’ll see how to customize operators for use with your own classes (a technique known as operator overloading).

The vector class template is available to anyone building applications with C++. The notations that the vector example uses might be unfamiliar to you, because vectors use template notation. Recall that Section 6.18 discussed function templates. In Chapter 14, we discuss class templates. For now, you should feel comfortable using class template vector by mimicking the syntax in the example we show in this section. You’ll deepen your understanding as we study class templates in Chapter 14. Chapter 20 presents class template vector (and several other standard C++ container classes) in detail.

The program of Fig. 7.26 demonstrates capabilities provided by C++ Standard Library class template vector that are not available for C-style pointer-based arrays. Standard class template vector provides many of the same features as the Array class that we construct in Chapter 11, Operator Overloading; String and Array Objects. Standard class template vector is defined in header <vector> (line 11) and belongs to namespace std (line 12). Chapter 20 discusses the full functionality of standard class template vector.

Lines 19–20 create two vector objects that store values of type int—integers1 contains seven elements, and integers2 contains 10 elements. By default, all the elements of each vector object are set to 0. Note that vectors can be defined to store any data type, by replacing int in vector<int> with the appropriate data type. This notation, which specifies the type stored in the vector, is similar to the template notation that Section 6.18 introduced with function templates. Again, Chapter 14 discusses this syntax in detail.

```
1 // Fig. 7.26: fig07_26.cpp
2 // Demonstrating C++ Standard Library class template vector.
3 #include <iostream>
4 using std::cout;
5 using std::cin;
6 using std::endl;
7 
8 #include <iomanip>
9 using std::setw;
```

Fig. 7.26 | C++ Standard Library class template vector. (Part 1 of 4.)

```
10
11 #include <vector>
12 using std::vector;
13
14 void outputVector( const vector< int > & ); // display the vector
15 void inputVector( vector< int > & ); // input values into the vector
16
17 int main()
18 {
19     vector< int > integers1( 7 ); // 7-element vector< int >
20     vector< int > integers2( 10 ); // 10-element vector< int >
21
22     // print integers1 size and contents
23     cout << "Size of vector integers1 is " << integers1.size()
24         << "\nvector after initialization:" << endl;
25     outputVector( integers1 );
26
27     // print integers2 size and contents
28     cout << "\nSize of vector integers2 is " << integers2.size()
29         << "\nvector after initialization:" << endl;
30     outputVector( integers2 );
31
32     // input and print integers1 and integers2
33     cout << "\nEnter 17 integers:" << endl;
34     inputVector( integers1 );
35     inputVector( integers2 );
36
37     cout << "\nAfter input, the vectors contain:\n"
38         << "integers1:" << endl;
39     outputVector( integers1 );
40     cout << "integers2:" << endl;
41     outputVector( integers2 );
42
43     // use inequality (!=) operator with vector objects
44     cout << "\nEvaluating: integers1 != integers2" << endl;
45
46     if ( integers1 != integers2 )
47         cout << "integers1 and integers2 are not equal" << endl;
48
49     // create vector integers3 using integers1 as an
50     // initializer; print size and contents
51     vector< int > integers3( integers1 ); // copy constructor
52
53     cout << "\nSize of vector integers3 is " << integers3.size()
54         << "\nvector after initialization:" << endl;
55     outputVector( integers3 );
56
57     // use overloaded assignment (=) operator
58     cout << "\nAssigning integers2 to integers1:" << endl;
59     integers1 = integers2; // assign integers2 to integers1
60
61     cout << "integers1:" << endl;
62     outputVector( integers1 );
```

```
cout << "integers2: " << endl;
outputVector( integers2 );

// use equality (==) operator with vector objects
cout << "\nEvaluating: integers1 == integers2" << endl;

if ( integers1 == integers2 )
   cout << "integers1 and integers2 are equal" << endl;

// use square brackets to create rvalue
cout << "\nintegers1[5] is " << integers1[ 5 ];

// use square brackets to create lvalue
cout << "\n\nAssigning 1000 to integers1[5]" << endl;
integers1[ 5 ] = 1000;
cout << "integers1: " << endl;
outputVector( integers1 );

// attempt to use out-of-range subscript
cout << "\nAttempt to assign 1000 to integers1.at( 15 )" << endl;
integers1.at( 15 ) = 1000; // ERROR: out of range
return 0;
} // end main

// output vector contents
void outputVector( const vector< int > &array )
{
   size_t i; // declare control variable

   for ( i = 0; i < array.size(); i++ )
   {
      cout << setw( 12 ) << array[ i ];

      if ( ( i + 1 ) % 4 == 0 ) // 4 numbers per row of output
         cout << endl;
   } // end for

   if ( i % 4 != 0 )
      cout << endl;
} // end function outputVector

// input vector contents
void inputVector( vector< int > &array )
{
   for ( size_t i = 0; i < array.size(); i++ )
      cin >> array[ i ];
} // end function inputVector
```

```
Size of vector integers1 is 7
vector after initialization:

             0             0             0             0
             0             0             0
```

**Fig. 7.26** | C++ Standard Library class template vector. (Part 3 of 4.)
