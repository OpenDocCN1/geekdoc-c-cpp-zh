```
9
10    // test indexOf to locate a character in a string
11    System.out.printf(
12        "'c' is located at index %d\n", letters.indexOf('c') );
13    System.out.printf(
14        "'a' is located at index %d\n", letters.indexOf('a', 1) );
15    System.out.printf(
16        "'$' is located at index %d\n\n", letters.indexOf('$') );
17
18    // test lastIndexOf to find a character in a string
19    System.out.printf( "Last 'c' is located at index %d\n",
20        letters.lastIndexOf('c') );
21    System.out.printf( "Last 'a' is located at index %d\n",
22        letters.lastIndexOf('a', 25) );
23    System.out.printf( "Last '$' is located at index %d\n\n",
24        letters.lastIndexOf('$') );
25
26    // test indexOf to locate a substring in a string
27    System.out.printf( "\"def\" is located at index %d\n",
28        letters.indexOf("def") );
29    System.out.printf( "\"def\" is located at index %d\n",
30        letters.indexOf("def", 7) );
31    System.out.printf( "\"hello\" is located at index %d\n\n",
32        letters.indexOf("hello") );
33
34    // test lastIndexOf to find a substring in a string
35    System.out.printf( "Last \"def\" is located at index %d\n",
36        letters.lastIndexOf("def") );
37    System.out.printf( "Last \"def\" is located at index %d\n",
38        letters.lastIndexOf("def", 25) );
39    System.out.printf( "Last \"hello\" is located at index %d\n",
40        letters.lastIndexOf("hello") );
41    } // end main
42    } // end class StringIndexMethods
```

```
'c' is located at index 2
'a' is located at index 13
'$' is located at index -1

Last 'c' is located at index 15
Last 'a' is located at index 13
Last '$' is located at index -1

"def" is located at index 3
"def" is located at index 16
"hello" is located at index -1

Last "def" is located at index 16
Last "def" is located at index 16
Last "hello" is located at index -1
```

Fig. 16.5 | String-searching methods indexOf and lastIndexOf. (Part 2 of 2.)

All the searches in this example are performed on the String letters (initialized with "abcdefghijklmnopqrstuvwxyzklm"). Lines 11–16 use method indexOf to locate the first