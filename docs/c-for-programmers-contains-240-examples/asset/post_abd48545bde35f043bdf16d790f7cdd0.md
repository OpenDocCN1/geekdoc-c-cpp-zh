
```cpp
20    // empty body
21 } // end constructor Test

23 // print x using implicit and explicit this pointers;
24 // the parentheses around *this are required
25 void Test::print() const
26 {
27     // implicitly use the this pointer to access the member x
28     cout << "       x = " << x;

30     // explicitly use the this pointer and the arrow operator
31     // to access the member x
32     cout << "\n this->x = " << this->x;

34     // explicitly use the dereferenced this pointer and
35     // the dot operator to access the member x
36     cout << "\n(*this).x = " << (*this).x << endl;
37 } // end function print

39 int main()
40 {
41     Test testObject( 12 ); // instantiate and initialize testObject

43     testObject.print();
44     return 0;
45 } // end main
```

```
       x = 12
   this->x = 12
  (*this).x = 12
```

**Fig. 10.17** | *this pointer implicitly and explicitly accessing an object’s members. (Part 2 of 2.)

For illustration purposes, member function `print` (lines 25–37) first prints x by using the `this` pointer implicitly (line 28)—only the name of the data member is specified. Then `print` uses two different notations to access x through the `this` pointer—the arrow operator (`->`) off the `this` pointer (line 32) and the dot operator (`.`) off the dereferenced `this` pointer (line 36).

Note the parentheses around `*this` (line 36) when used with the dot member selection operator (`.`). The parentheses are required because the dot operator has higher precedence than the `*` operator. Without the parentheses, the expression `*this.x` would be evaluated as if it were parenthesized as `*(this.x)`, which is a compilation error, because the dot operator cannot be used with a pointer.

# Common Programming Error 10.7

> Attempting to use the member selection operator (`.`) with a pointer to an object is a compilation error—the dot member selection operator may be used only with an lvalue such as an object’s name, a reference to an object or a dereferenced pointer to an object.

One interesting use of the `this` pointer is to prevent an object from being assigned to itself. As we’ll see in Chapter 11, self-assignment can cause serious errors when the object contains pointers to dynamically allocated storage.

```
5
6 #include <iomanip>
7 using std::setfill;
8 using std::setw;
9
10 #include "Time.h" // Time class definition
11
12 // constructor function to initialize private data;
13 // calls member function setTime to set variables;
14 // default values are 0 (see class definition)
15 Time::Time( int hr, int min, int sec )
16 {
17     setTime( hr, min, sec );
18 } // end Time constructor
19
20 // set values of hour, minute, and second
21 Time &Time::setTime( int h, int m, int s ) // note Time & return
22 {
23     setHour( h );
24     setMinute( m );
25     setSecond( s );
26     return *this; // enables cascading
27 } // end function setTime
28
29 // set hour value
30 Time &Time::setHour( int h ) // note Time & return
31 {
32     hour = ( h >= 0 && h < 24 ) ? h : 0; // validate hour
33     return *this; // enables cascading
34 } // end function setHour
35
36 // set minute value
37 Time &Time::setMinute( int m ) // note Time & return
38 {
39     minute = ( m >= 0 && m < 60 ) ? m : 0; // validate minute
40     return *this; // enables cascading
41 } // end function setMinute
42
43 // set second value
44 Time &Time::setSecond( int s ) // note Time & return
45 {
46     second = ( s >= 0 && s < 60 ) ? s : 0; // validate second
47     return *this; // enables cascading
48 } // end function setSecond
49
50 // get hour value
51 int Time::getHour() const
52 {
53     return hour;
54 } // end function getHour
55
```

Fig. 10.19 | Time class member-function definitions modified to enable cascaded member-function calls. (Part 2 of 3.)

```
56 // get minute value
57 int Time::getMinute() const
58 {
59     return minute;
60 } // end function getMinute
61
62 // get second value
63 int Time::getSecond() const
64 {
65     return second;
66 } // end function getSecond
67
68 // print Time in universal-time format (HH:MM:SS)
69 void Time::printUniversal() const
70 {
71     cout << setfill('0') << setw(2) << hour << ":"
72         << setw(2) << minute << ":" << setw(2) << second;
73 } // end function printUniversal
74
75 // print Time in standard-time format (HH:MM:SS AM or PM)
76 void Time::printStandard() const
77 {
78     cout << ( ( hour == 0 || hour == 12 ) ? 12 : hour % 12 )
79         << ":" << setfill('0') << setw(2) << minute
80         << ":" << setw(2) << second << ( hour < 12 ? " AM" : " PM" );
81 } // end function printStandard
```

Fig. 10.19 | Time class member-function definitions modified to enable cascaded member-function calls. (Part 3 of 3.)

```
1 // Fig. 10.20: fig10_20.cpp
2 // Cascading member-function calls with the this pointer.
3 #include <iostream>
4 using std::cout;
5 using std::endl;
6
7 #include "Time.h" // Time class definition
8
9 int main()
10 {
11     Time t; // create Time object
12
13     // cascaded function calls
14     t.setHour( 18 ).setMinute( 30 ).setSecond( 22 );
15
16     // output time in universal and standard formats
17     cout << "Universal time: ";
18     t.printUniversal();
19
20     cout << "\nStandard time: ";
21     t.printStandard();
```

Fig. 10.20 | Cascading member-function calls with the this pointer. (Part 1 of 2.)

```
22
23     cout << "\n\nNew standard time: ";
24
25     // cascaded function calls
26     t.setTime( 20, 20, 20 ).printStandard();
27     cout << endl;
28     return 0;
29 } // end main
```

Universal time: 18:30:22
Standard time: 6:30:22 PM

New standard time: 8:20:20 PM

Fig. 10.20 | Cascading member-function calls with the this pointer. (Part 2 of 2.)

The program of Fig. 10.20 creates Time object t (line 11), then uses it in cascaded member-function calls (lines 14 and 26). Why does the technique of returning *this as a reference work? The dot operator (.) associates from left to right, so line 14 first evaluates t.setHour( 18 ), then returns a reference to object t as the value of this function call. The remaining expression is then interpreted as

    t.setMinute( 30 ).setSecond( 22 );

The t.setMinute( 30 ) call executes and returns a reference to the object t. The remaining expression is interpreted as

    t.setSecond( 22 );

Line 26 also uses cascading. The calls must appear in the order shown in line 26, because printStandard as defined in the class does not return a reference to t. Placing the call to printStandard before the call to setTime in line 26 results in a compilation error. Chapter 11 presents several practical examples of using cascaded function calls. One such example uses multiple << operators with cout to output multiple values in a single statement.

## 10.6 Dynamic Memory Management with Operators new and delete

C++ enables programmers to control the allocation and deallocation of memory in a program for any built-in or user-defined type. This is known as dynamic memory management and is performed with operators new and delete. Recall that class Employee (Figs. 10.12–10.13) uses two 25-character arrays to represent the first and last name of an Employee. The Employee class definition (Fig. 10.12) must specify the number of elements in each of these arrays when it declares them as data members, because the size of the data members dictates the amount of memory required to store an Employee object. As we discussed earlier, these arrays may waste space for names shorter than 24 characters. Also, names longer than 24 characters must be truncated to fit in these fixed-size arrays.

Wouldn’t it be nice if we could use arrays containing exactly the number of elements needed to store an Employee’s first and last name? Dynamic memory management allows us to do exactly that. As you’ll see in the example of Section 10.7, if we replace array data members firstName and lastName with pointers to char, we can use the new operator to dynamically allocate (i.e., reserve) the exact amount of memory required to hold each name at execution time. Dynamically allocating memory in this fashion causes an array (or any other built-in or user-defined type) to be created in the free store (sometimes called the heap)—a region of memory assigned to each program for storing dynamically allocated objects. Once the memory for an array is allocated in the free store, we can gain access to it by aiming a pointer at the first element of the array. When we no longer need the array, we can return the memory to the free store by using the delete operator to deallocate (i.e., release) the memory, which can then be reused by future new operations.

Again, we present the modified Employee class as described here in the example of Section 10.7. First, we present the details of using the new and delete operators to dynamically allocate memory to store objects, fundamental types and arrays.

Consider the following declaration and statement:

```
Time *timePtr;
 timePtr = new Time;
```

The new operator allocates storage of the proper size for an object of type Time, calls the default constructor to initialize the object and returns a pointer to the type specified to the right of the new operator (i.e., a Time *). Note that new can be used to dynamically allocate any fundamental type (such as int or double) or class type. If new is unable to find sufficient space in memory for the object, it indicates that an error occurred by “throwing an exception.” Chapter 16, Exception Handling, discusses how to deal with new failures in the context of the ISO/IEC C++ standard. In particular, we’ll show how to “catch” the exception thrown by new and deal with it. When a program does not “catch” an exception, the program terminates immediately.

# Portability Tip 10.1

> On failure, the new operator returns a 0 pointer in versions of C++ prior to the ISO/IEC standard. We use the standard version of operator new throughout this book.

To destroy a dynamically allocated object and free the space for the object, use the delete operator as follows:

```
delete timePtr;
```

This statement first calls the destructor for the object to which timePtr points, then deallocates the memory associated with the object. After the preceding statement, the memory can be reused by the system to allocate other objects.

# Common Programming Error 10.8

> Not releasing dynamically allocated memory when it is no longer needed can cause the system to run out of memory prematurely. This is sometimes called a “memory leak.”

You can provide an initializer for a newly created fundamental-type variable, as in

```
double *ptr = new double( 3.14159 );
```

which initializes a newly created double to 3.14159 and assigns the resulting pointer to ptr. The same syntax can be used to specify a comma-separated list of arguments to the constructor of an object. For example,
