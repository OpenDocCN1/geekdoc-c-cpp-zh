```
~~~cpp
15     << " lowercase letter\n"
16     << ( islower( '!' ) ? "! is a" : "! is not a" )
17     << " lowercase letter\n";
18
19  cout << "\nAccording to isupper:\n"
20     << ( isupper( 'D' ) ? "D is an" : "D is not an" )
21     << " uppercase letter\n"
22     << ( isupper( 'd' ) ? "d is an" : "d is not an" )
23     << " uppercase letter\n"
24     << ( isupper( '8' ) ? "8 is an" : "8 is not an" )
25     << " uppercase letter\n"
26     << ( isupper( '$' ) ? "$ is an" : "$ is not an" )
27     << " uppercase letter\n";
28
29  cout << "\nu converted to uppercase is "
30     << static_cast< char >( toupper( 'u' ) )
31     << "\n7 converted to uppercase is "
32     << static_cast< char >( toupper( '7' ) )
33     << "\n$ converted to uppercase is "
34     << static_cast< char >( toupper( '$' ) )
35     << "\nL converted to lowercase is "
36     << static_cast< char >( tolower( 'L' ) ) << endl;
37 } // end main
~~~
```

```
~~~
According to islower:
D is a lowercase letter
P is not a lowercase letter
5 is not a lowercase letter
! is not a lowercase letter

According to isupper:
D is an uppercase letter
d is not an uppercase letter
8 is not an uppercase letter
$ is not an uppercase letter

u converted to uppercase is U
7 converted to uppercase is 7
$ converted to uppercase is $
L converted to lowercase is l
~~~
```

Fig. 21.19 | Character-handling functions islower, isupper, tolower and toupper. (Part 2 of 2.)

Figure 21.20 demonstrates functions **isspace**, **iscntrl**, **ispunct**, **isprint** and **isgraph**. Function **isspace** determines whether its argument is a white-space character, such as space (' '), form feed ('\f'), newline ('\n'), carriage return ('\r'), horizontal tab ('\t') or vertical tab ('\v'). Function **iscntrl** determines whether its argument is a control character such as horizontal tab ('\t'), vertical tab ('\v'), form feed ('\f'), alert ('\a'), backspace ('\b'), carriage return ('\r') or newline ('\n'). Function **ispunct** determines whether its argument is a printing character other than a space, digit or letter, such as $, #, (, ), [, ], {, }, ;, : or %. Function **isprint** determines whether its argument is a character that can be displayed on the screen (including the space character). Function **isgraph** tests for the same characters as isprint, but the space character is not included.