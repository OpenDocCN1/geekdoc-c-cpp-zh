```
~~~cpp
 4  #include <iomanip>
 5  using namespace std;
 6
 7  int main()
 8  {
 9     int x = 12345;
10
11     // display x right justified (default)
12     cout << "Default is right justified:" << endl
13          << setw( 10 ) << x;
14
15     // use left manipulator to display x left justified
16     cout << "\n\nUse std::left to left justify x:\n"
17          << left << setw( 10 ) << x;
18
19     // use right manipulator to display x right justified
20     cout << "\n\nUse std::right to right justify x:\n"
21          << right << setw( 10 ) << x << endl;
22  } // end main
~~~
```

```
~~~text
Default is right justified:
     12345

Use std::left to left justify x:
12345

Use std::right to right justify x:
     12345
~~~
```

![](bbox=[0.066, 0.671, 0.934, 0.694])

Stream manipulator internal indicates that a number’s sign (or base when using stream manipulator showbase) should be left justified within a field, that the number’s magnitude should be right justified and that intervening spaces should be padded with the fill character. Figure 21.15 shows the internal stream manipulator specifying internal spacing (line 10). Note that showpos forces the plus sign to print (line 10). To reset the showpos setting, output the stream manipulator noshowpos.

```
~~~cpp
 1  // Fig. 21.15: fig21_15.cpp
 2  // Printing an integer with internal spacing and plus sign.
 3  #include <iostream>
 4  #include <iomanip>
 5  using namespace std;
 6
 7  int main()
 8  {
 9     // display value with internal spacing and plus sign
10     cout << internal << showpos << setw( 10 ) << 123 << endl;
11  } // end main
~~~
```

![](bbox=[0.066, 0.955, 0.923, 0.978])