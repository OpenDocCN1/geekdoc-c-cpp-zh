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