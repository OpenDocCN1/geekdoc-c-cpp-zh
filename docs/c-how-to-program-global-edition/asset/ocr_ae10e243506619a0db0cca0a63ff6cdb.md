```
1 // Fig. 7.21: fig07_21.c
2 // Copying a string using array notation and pointer notation.
3 #include <stdio.h>
4 #define SIZE 10
5
6 void copy1(char * const s1, const char * const s2); // prototype
7 void copy2(char *s1, const char *s2); // prototype
8
9 int main(void)
10 {
11     char string1[SIZE]; // create array string1
12     char *string2 = "Hello"; // create a pointer to a string
13
14     copy1(string1, string2);
15     printf("string1 = %s\n", string1);
16
17     char string3[SIZE]; // create array string3
18     char string4[] = "Good Bye"; // create an array containing a string
19
20     copy2(string3, string4);
21     printf("string3 = %s\n", string3);
22 }
23
24 // copy s2 to s1 using array notation
25 void copy1(char * const s1, const char * const s2)
26 {
27     // loop through strings
28     for (size_t i = 0; s1[i] = s2[i] != '\0'; ++i) {
29         ; // do nothing in body
30     }
31 }
32
33 // copy s2 to s1 using pointer notation
34 void copy2(char *s1, const char *s2)
35 {
36     // loop through strings
37     for ( ; (*s1 = *s2) != '\0'; ++s1, ++s2) {
38         ; // do nothing in body
39     }
40 }
```

string1 = Hello
string3 = Good Bye

# Fig. 7.21 | Copying a string using array notation and pointer notation.

# Copying with Array Index Notation

Function copy1 uses array index notation to copy the string in s2 to the character array s1. The function defines counter variable i as the array index. The for statement header (line 28) performs the entire copy operation—its body is the empty statement. The header specifies that i is initialized to zero and incremented by one on each iteration of the loop. The expression s1[i] = s2[i] copies one character from s2 to s1. When the null character