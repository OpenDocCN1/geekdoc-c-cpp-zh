# Chapter 10 Classes and Objects: A Deeper Look

```
63  minute = value;
64  }
65  }
66  
67  
68  // property that gets and sets the second
69  public int Second
70  {
71      get
72      {
73          return second;
74      }
75      set
76      {
77          if (value < 0 || value > 59)
78          {
79              throw new ArgumentOutOfRangeException(nameof(value),
80              value, $"{nameof(Second)} must be 0-59");
81          }
82      }
83  }
84  second = value;
85  }
86  
87  // convert to string in universal-time format (HH:MM:SS)
88  public string ToUniversalString() =>
89      $"{Hour:D2}:{Minute:D2}:{Second:D2}";
90
91  // convert to string in standard-format (H:MM:SS AM or PM)
92  public override string ToString() =>
93      $"{{(Hour == 0 || Hour == 12) ? 12 : Hour % 12)}:{Minute:D2}:{Second:D2} {(Hour < 12) ? "AM" : :"PM"}\}";
```

10.5 Time2 class declaration with overloaded constructors. (Part 3 of 3.)

Class Time2's Three-Argument Constructor
Lines 12-15 declare a constructor with three default parameters. We did not define a constructor with empty parameter list, for class Time2 the constructor at lines 12-15 is also considered to be the class's parameter constructor—you can call the constructor without arguments or with one argument for the hour, two for the hour and minute, or three for the hour, minute and second. This constructor calls SetTime to set the time.

# Common Programming Error 10.1

> A constructor can call methods of its class. Because the instance variables might not yet be initialized, because the constructor is in the process of initializing the object. Using instance variables before they have been initialized is a logic error.

# Constructor Initializers

Lines 18–19 declare another Time2 constructor that receives a reference to a Time2 object. In this case, the values from the Time2 argument are passed to the three-parameter con-