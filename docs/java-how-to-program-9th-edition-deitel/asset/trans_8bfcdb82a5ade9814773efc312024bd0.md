

```
75        else
76            throw new IllegalArgumentException( "second must be 0-59" );
77    } // end method setSecond
78
79    // Get Methods
80    // get hour value
81    public int getHour()
82    {
83        return hour;
84    } // end method getHour
85
86    // get minute value
87    public int getMinute()
88    {
89        return minute;
90    } // end method getMinute
91
92    // get second value
93    public int getSecond()
94    {
95        return second;
96    } // end method getSecond
97
98    // convert to String in universal-time format (HH:MM:SS)
99    public String toUniversalString()
100    {
101        return String.format(
102            "%02d:%02d:%02d", getHour(), getMinute(), getSecond() );
103    } // end method toUniversalString
104
105    // convert to String in standard-time format (H:MM:SS AM or PM)
106    public String toString()
107    {
108        return String.format( "%d:%02d:%02d %s",
109            ( (getHour() == 0 || getHour() == 12) ? 12 : getHour() % 12 ),
110            getMinute(), getSecond(), ( getHour() < 12 ? "AM" : "PM" ) );
111    } // end method toString
112 } // end class Time2
```

Fig. 8.5 | Time2 class with overloaded constructors. (Part 3 of 3.)

## Class Time2's Constructors

Lines 12–15 declare a so-called no-argument constructor that's invoked without arguments. Once you declare any constructors in a class, the compiler will not provide a default constructor. This no-argument constructor ensures that class Time2's clients can create Time2 objects with default values. Such a constructor simply initializes the object as specified in the constructor's body. In the body, we introduce a use of the this reference that's allowed only as the first statement in a constructor's body. Line 14 uses this in method-call syntax to invoke the Time2 constructor that takes three parameters (lines 30–33) with values of 0 for the hour, minute and second. Using the this reference as shown here is a popular way to reuse initialization code provided by another of the class's constructors rather than defining similar code in the no-argument constructor's body. We use this syntax to reuse initialization code.

toUniversalString and toString call methods getHour, getMinute and getSecond in line 93 and lines 100–101, respectively. In each case, these methods could have accessed the class’s private data directly without calling the set and get methods. However, consider changing the representation of the time from three int values (requiring 12 bytes of memory) to a single int value representing the total number of seconds that have elapsed since midnight (requiring only 4 bytes of memory). If we made such a change, only the bodies of the methods that access the private data directly would need to change—in particular, the individual set and get methods for the hour, minute and second. There would be no need to modify the bodies of methods setTime, toUniversalString or toString because they do not access the data directly. Designing the class in this manner reduces the likelihood of programming errors when altering the class’s implementation.

Similarly, each Time2 constructor could include a copy of the appropriate statements from methods setHour, setMinute and setSecond. Doing so may be slightly more efficient, because the extra calls to the constructor and setTime are eliminated. However, duplicating statements in multiple methods or constructors makes changing the class’s internal data representation more difficult. Having the Time2 constructors call the constructor with three arguments (or even call setTime directly) requires that any changes to the implementation of setTime be made only once. Also, the compiler can optimize programs by removing calls to simple methods and replacing them with the expanded code of their declarations—a technique known as inlining the code, which improves program performance.

### Software Engineering Observation 8.4

When implementing a method of a class, use the class’s set and get methods to access the class’s private data. This simplifies code maintenance and reduces the likelihood of errors.

## Using Class Time2’s Overloaded Constructors

Class Time2Test (Fig. 8.6) invokes the overloaded Time2 constructors (lines 8–12 and 40). Line 8 invokes the no-argument constructor (Fig. 8.5, lines 12–15). Lines 9–13 of the program demonstrate passing arguments to the other Time2 constructors. Line 9 invokes the single-argument constructor that receives an int at lines 18–21 of Fig. 8.5. Line 10 invokes the two-argument constructor at lines 24–27 of Fig. 8.5. Line 11 invokes the three-argument constructor at lines 30–33 of Fig. 8.5. Line 12 invokes the single-argument constructor that takes a Time2 at lines 36–40 of Fig. 8.5. Next, the application displays the String representations of each Time2 object to confirm that it was initialized properly. Line 40 attempts to initialize t6 by creating a new Time2 object and passing three invalid values to the constructor. When the constructor attempts to use the invalid hour value to initialize the object’s hour, an IllegalArgumentException occurs. We catch this exception at line 42 and display its error message, which results in the last line of the output.

```
1  // Fig. 8.6: Time2Test.java
2  // Overloaded constructors used to initialize Time2 objects.
3
4  public class Time2Test
5  {
```

Fig. 8.6 | Overloaded constructors used to initialize Time2 objects. (Part 1 of 3.)

```
public static void main( String[] args )
{
    Time2 t1 = new Time2(); // 00:00:00
    Time2 t2 = new Time2( 2 ); // 02:00:00
    Time2 t3 = new Time2( 21, 34 ); // 21:34:00
    Time2 t4 = new Time2( 12, 25, 42 ); // 12:25:42
    Time2 t5 = new Time2( t4 ); // 12:25:42

    System.out.println( "Constructed with:" );
    System.out.println( "t1: all arguments defaulted" );
    System.out.printf( "    %s\n", t1.toUniversalString() );
    System.out.printf( "    %s\n", t1.toString() );

    System.out.println(
        "t2: hour specified; minute and second defaulted" );
    System.out.printf( "    %s\n", t2.toUniversalString() );
    System.out.printf( "    %s\n", t2.toString() );

    System.out.println(
        "t3: hour and minute specified; second defaulted" );
    System.out.printf( "    %s\n", t3.toUniversalString() );
    System.out.printf( "    %s\n", t3.toString() );

    System.out.println( "t4: hour, minute and second specified" );
    System.out.printf( "    %s\n", t4.toUniversalString() );
    System.out.printf( "    %s\n", t4.toString() );

    System.out.println( "t5: Time2 object t4 specified" );
    System.out.printf( "    %s\n", t5.toUniversalString() );
    System.out.printf( "    %s\n", t5.toString() );

    // attempt to initialize t6 with invalid values
    try
    {
        Time2 t6 = new Time2( 27, 74, 99 ); // invalid values
    } // end try
    catch ( IllegalArgumentException e )
    {
        System.out.printf( "\nException while initializing t6: %s\n",
            e.getMessage() );
    } // end catch
} // end main
} // end class Time2Test
```

Constructed with:
t1: all arguments defaulted
00:00:00
12:00:00 AM
t2: hour specified; minute and second defaulted
02:00:00
2:00:00 AM

Fig. 8.6 | Overloaded constructors used to initialize Time2 objects. (Part 2 of 3.)

```
t3: hour and minute specified; second defaulted
    21:34:00
    9:34:00 PM
t4: hour, minute and second specified
    12:25:42
    12:25:42 PM
t5: Time2 object t4 specified
    12:25:42
    12:25:42 PM

Exception while initializing t6: hour must be 0–23
```

## 8.6 Default and No-Argument Constructors

Every class must have at least one constructor. If you do not provide any in a class’s declaration, the compiler creates a default constructor that takes no arguments when it’s invoked. The default constructor initializes the instance variables to the initial values specified in their declarations or to their default values (zero for primitive numeric types, false for boolean values and null for references). In Section 9.4.1, you’ll learn that the default constructor performs another task also.

If your class declares constructors, the compiler will not create a default constructor. In this case, you must declare a no-argument constructor if default initialization is required. Like a default constructor, a no-argument constructor is invoked with empty parentheses. The Time2 no-argument constructor (lines 12–15 of Fig. 8.5) explicitly initializes a Time2 object by passing to the three-argument constructor 0 for each parameter. Since 0 is the default value for int instance variables, the no-argument constructor in this example could actually be declared with an empty body. In this case, each instance variable would receive its default value when the no-argument constructor was called. If we omit the no-argument constructor, clients of this class would not be able to create a Time2 object with the expression new Time2().

> **Common Programming Error 8.5**
> 
> A compilation error occurs if a program attempts to initialize an object of a class by passing the wrong number or types of arguments to the class’s constructor.

> **Error-Prevention Tip 8.2**
> 
> Ensure that you do not include a return type in a constructor definition. Java allows other methods of the class besides its constructors to have the same name as the class and to specify return types. Such methods are not constructors and will not be called when an object of the class is instantiated.

## 8.7 Notes on Set and Get Methods

As you know, a class’s private fields can be manipulated only by its methods. A typical manipulation might be the adjustment of a customer’s bank balance (e.g., a private instance variable of a class BankAccount) by a method computeInterest. Classes often provide public methods to allow clients of the class to set (i.e., assign values to) or get (i.e., obtain the values of) private instance variables.

