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