```
~~~cpp
6  int main()
7  {
8     char x[] = "Home Sweet Home";
9
10    cout << "The string in array x before memmove is: " << x;
11    cout << "\nThe string in array x after memmove is: "
12       << static_cast< char * >( memmove( x, &x[ 5 ], 10 ) ) << endl;
13
14 } // end main
~~~
```

```
~~~text
The string in array x before memmove is: Home Sweet Home
The string in array x after memmove is: Sweet Home Home
~~~
```

Fig. 21.43 | Memory-handling function memmove. (Part 2 of 2.)

Function memcmp (Fig. 21.44, lines 14–16) compares the specified number of characters of its first argument with the corresponding characters of its second argument. The function returns a value greater than zero if the first argument is greater than the second argument, zero if the arguments are equal, and a value less than zero if the first argument is less than the second argument. [Note: With some compilers, function memcmp returns –1, 0 or 1, as in the sample output of Fig. 21.44. With other compilers, this function returns 0 or the difference between the numeric codes of the first characters that differ in the strings being compared. For example, when s1 and s2 are compared, the first character that differs between them is the fifth character of each string—e (numeric code 69) for s1 and X (numeric code 72) for s2. In this case, the return value will be 19 (or –19 when s2 is compared to s1).]

```
~~~cpp
1  // Fig. 21.44: fig21_38.cpp
2  // Using memcmp
3  #include <iostream>
4  #include <iomanip>
5  #include <cstring> // memcmp prototype
6  using namespace std;
7
8  int main()
9  {
10    char s1[] = "ABCDEFG";
11    char s2[] = "ABCDXYZ";
12
13    cout << "s1 = " << s1 << "\ns2 = " << s2 << endl;
14       << "\n\nmemcmp(s1, s2, 4) = " << setw( 3 ) << memcmp( s1, s2, 4 )
15       << "\nmemcmp(s1, s2, 7) = " << setw( 3 ) << memcmp( s1, s2, 7 )
16       << "\nmemcmp(s2, s1, 7) = " << setw( 3 ) << memcmp( s2, s1, 7 )
17       << endl;
18 } // end main
~~~
```

```
~~~text
s1 = ABCDEFG
s2 = ABCDXYZ
~~~
```

Fig. 21.44 | Memory-handling function memcmp. (Part 1 of 2.)