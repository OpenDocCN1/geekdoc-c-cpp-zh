```
```cpp
// use the default random-number generation engine to
// produce uniformly distributed pseudorandom int values from 1 to 6
default_random_engine engine( static_cast<unsigned int>( time() ) );
uniform_int_distribution<unsigned int> randInt( 1, 6 );

// loop 10 times
for ( unsigned int counter = 1; counter <= 10; ++counter )
{
   // pick random number from 1 to 6 and output it
   cout << setw( 10 ) << randInt( engine );

   // if counter is divisible by 5, start a new line of output
   if ( counter % 5 == 0 )
      cout << endl;
} // end for
} // end main
```
```

![](bbox=[0.086, 0.364, 0.917, 0.415])

**Fig. 6.12** | Using a C++11 random-number generation engine and distribution to roll a six-sided die. (Part 2 of 2.)

The notation `<unsigned int>` in line 15 indicates that uniform_int_distribution is a class template. In this case, any integer type can be specified in the angle brackets (< and >). In Chapter 18, we discuss how to create class templates and various other chapters show how to use existing class templates from the C++ Standard Library. For now, you should feel comfortable using class template uniform_int_distribution by mimicking the syntax shown in the example.

# 6.10 Storage Classes and Storage Duration

The programs you’ve seen so far use identifiers for variable names and functions. The attributes of variables include *name*, *type*, *size* and *value*. Each identifier in a program also has other attributes, including **storage duration**, **scope** and **linkage**.

C++ provides five **storage-class specifiers** that determine a variable’s storage duration: **register**, **extern**, **mutable** and **static**. This section discusses storage-class specifiers register, extern and static. Storage-class specifier mutable is used exclusively with classes and thread_local is used in multithreaded applications—these are discussed in Chapters 23 and 24, respectively.

# Storage Duration

An identifier’s *storage duration* determines the period during which that identifier exists in memory. Some exist briefly, some are repeatedly created and destroyed and others exist for a program’s entire execution. First we discuss the storage durations **static** and **automatic**.

# Scope

An identifier’s *scope* is where the identifier can be referenced in a program. Some identifiers can be referenced throughout a program; others can be referenced from only limited portions of a program. Section 6.11 discusses the scope of identifiers.