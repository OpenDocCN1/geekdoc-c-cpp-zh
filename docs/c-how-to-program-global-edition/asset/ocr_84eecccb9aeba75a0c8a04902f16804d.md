# ## 17.5 Time Class Case Study: Constructors with Default Arguments

The program of Figs. 17.4–17.6 enhances class Time to demonstrate how arguments are implicitly passed to a constructor. The constructor defined in Fig. 17.2 initialized hour, minute and second to 0 (i.e., midnight in universal time). Like other functions, constructors can specify default arguments. Line 13 of Fig. 17.4 declares the Time constructor to include default arguments, specifying a default value of zero for each argument passed to the constructor. The constructor is declared explicit because it can be called with one argument. We discuss explicit constructors in Section 18.13.

```
~~~cpp
1  // Fig. 17.4: Time.h
2  // Time class containing a constructor with default arguments.
3  // Member functions defined in Time.cpp.
4
5  // prevent multiple inclusions of header
6  #ifndef TIME_H
7  #define TIME_H
8
9  // Time class definition
10 class Time
11 {
12 public:
13    explicit Time( int = 0, int = 0, int = 0 ); // default constructor
14
15    // set functions
16    void setTime( int, int, int ); // set hour, minute, second
17    void setHour( int ); // set hour (after validation)
18    void setMinute( int ); // set minute (after validation)
19    void setSecond( int ); // set second (after validation)
20
21    // get functions
22    unsigned int getHour() const; // return hour
23    unsigned int getMinute() const; // return minute
24    unsigned int getSecond() const; // return second
25
26    void printUniversal() const; // output time in universal-time format
27    void printStandard() const; // output time in standard-time format
28 private:
29    unsigned int hour; // 0 - 23 (24-hour clock format)
30    unsigned int minute; // 0 - 59
31    unsigned int second; // 0 - 59
32 }; // end class Time
33
34 #endif
~~~
```

Fig. 17.4 | Time Class containing a constructor with default arguments.

In Fig. 17.5, lines 10–13 define the new version of the Time constructor that receives values for parameters hour, minute and second that will be used to initialize private data members hour, minute and second, respectively. The default arguments to the constructor ensure that, even if no values are provided in a constructor call, the constructor still ini-