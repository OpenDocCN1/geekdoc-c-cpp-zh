```
```cpp
6  int main()
7  {
8      int widthValue = 4;
9      char sentence[ 10 ];
10
11     cout << "Enter a sentence:" << endl;
12     cin.width( 5 ); // input only 5 characters from sentence
13
14     // set field width, then display characters based on that width
15     while ( cin >> sentence )
16     {
17         cout.width(widthValue++);
18         cout << sentence << endl;
19         cin.width( 5 ); // input 5 more characters from sentence
20     } // end while
21 } // end main
```
```

```
```text
Enter a sentence:
This is a test of the width member function
This
   is
     a
       t
         of
           the
             widt
                h
                 memb
                     er
                      func
                           tion
```
```

**Fig. 13.10**  |  width member function of class ios_base. (Part 2 of 2.)

# 13.6.4 User-Defined Output Stream Manipulators

You can create your own stream manipulators. Figure 13.11 shows how to create and use *new* nonparameterized stream manipulators `bell` (lines 8–11), `carriageReturn` (lines 14–17), `tab` (lines 20–23) and `endl` (line 27–30). For output stream manipulators, the return type and parameter must be of type `ostream &`. When line 35 inserts the `endlLine` manipulator in the output stream, function `endlLine` is called and line 29 outputs the escape sequence `\n` and the `flush` manipulator (which flushes the output buffer) to the standard output stream `cout`. Similarly, when lines 35–44 insert the manipulators `tab`, `bell` and `carriageReturn` in the output stream, their corresponding functions—`tab` (line 20), `bell` (line 8) and `carriageReturn` (line 14) are called, which in turn output various escape sequences.

```
```cpp
1  // Fig. 13.11: fig13_11.cpp
2  // Creating and testing user-defined, nonparameterized
3  // stream manipulators.
4  #include <iostream>
5  using namespace std;
```
```

**Fig. 13.11**  |  User-defined, nonparameterized stream manipulators. (Part 2 of 2.)