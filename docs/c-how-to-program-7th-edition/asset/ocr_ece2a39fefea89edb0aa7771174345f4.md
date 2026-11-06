```
~~~cpp
1  // Fig. 18.4: Fig18_04.cpp
2  // Using the swap function to swap two strings.
3  #include <iostream>
4  #include <string>
5  using namespace std;
6
7  int main()
8  {
9     string first( "one" );
10    string second( "two" );
11
12    // output strings
13    cout << "Before swap:\n first: " << first << "\nsecond: " << second;
14
15    first.swap( second ); // swap strings
16
17    cout << "\n\nAfter swap:\n first: " << first
18       << "\nsecond: " << second << endl;
19  } // end main
~~~
```

```
~~~text
Before swap:
  first: one
second: two

After swap:
  first: two
second: one
~~~
```

Fig. 18.4 | Using function swap to swap two strings.

# ## 18.6 string Characteristics

Class string provides member functions for gathering information about a string's size, length, capacity, maximum length and other characteristics. A string's size or length is the number of characters currently stored in the string. A string's capacity is the number of characters that can be stored in the string without allocating more memory. The capacity of a string must be at least equal to the current size of the string, though it can be greater. The exact capacity of a string depends on the implementation. The maximum size is the largest possible size a string can have. If this value is exceeded, a length_error exception is thrown. Figure 18.5 demonstrates string class member functions for determining various characteristics of strings.

```
~~~cpp
1  // Fig. 18.5: Fig18_05.cpp
2  // Demonstrating member functions related to size and capacity.
3  #include <iostream>
4  #include <string>
5  using namespace std;
6
7  void printStatistics( const string & );
~~~
```

Fig. 18.5 | Printing string characteristics. (Part 1 of 3.)