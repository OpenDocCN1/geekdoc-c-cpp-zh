
```
Program
main()
{
    char c;
    printf("\n\n");
    for( c = 65 ; c <= 122 ; c = c + 1 )
    {
        if( c > 90 && c < 97 )
            continue;
        printf("|%4d - %c ", c, c);
    }
    printf("\n\n");
}
```

Output
| 65 - A | 66 - B | 67 - C | 68 - D | 69 - E | 70 - F
| 71 - G | 72 - H | 73 - I | 74 - J | 75 - K | 76 - L
| 77 - M | 78 - N | 79 - O | 80 - P | 81 - Q | 82 - R
| 83 - S | 84 - T | 85 - U | 86 - V | 87 - W | 88 - X
| 89 - Y | 90 - Z | 97 - a | 98 - b | 99 - c | 100 - d
| 101 - e | 102 - f | 103 - g | 104 - h | 105 - i | 106 - j
| 107 - k | 108 - l | 109 - m | 110 - n | 111 - o | 112 - p
| 113 - q | 114 - r | 115 - s | 116 - t | 117 - u | 118 - v
| 119 - w | 120 - x | 121 - y | 122 - z |

Fig. 4.7 Printing of the alphabet set in decimal and character form

## 4.6 PUTTING STRINGS TOGETHER

Just as we cannot assign one string to another directly, we cannot join two strings together by the simple arithmetic addition. That is, the statements such as

```
string3 = string1 + string2;
string2 = string1 + "hello";
```

are not valid. The characters from string1 and string2 should be copied into the string3 one after the other. The size of the array string3 should be large enough to hold the total characters.

The process of combining two strings together is called concatenation. Example 4.7 illustrates the concatenation of three strings.

EXAMPLE 4.7 The names of employees of an organization are stored in three arrays, namely first_name, second_name, and last_name. Write a program to concatenate the three parts into one string to be called name.

The program is given in Fig. 4.8. Three for loops are used to copy the three strings. In the first loop, the characters contained in the first_name are copied into the variable name until the null character is reached. The null character is not copied; instead it is replaced by a space by the assignment statement

```
name[i] = ' ' ;
```

Similarly, the second_name is copied into name, starting from the column just after the space created by the above statement. This is achieved by the assignment statement

```
name[i+j+1] = second_name[j];
```

If first_name contains 4 characters, then the value of i at this point will be 4 and therefore the first character from second_name will be placed in the fifth cell of name. Note that we have stored a space in the fourth cell.

In the same way, the statement

`name[i+j+k+2] = last_name[k];`

is used to copy the characters from last_name into the proper locations of name.

At the end, we place a null character to terminate the concatenated string name. In this example, it is important to note the use of the expressions i+j+1 and i+j+k+2.

```c
Program
main()
{
    int i, j, k;
    char first_name[10] = {"VISWANATH"};
    char second_name[10] = {"PRATAP"};
    char last_name[10] = {"SINGH"};
    char name[30];
    /* Copy first name into name */
    for( i = 0; first_name[i] != '\0' ; i++ )
        name[i] = first_name[i];
    /* End first name with a space */
    name[i] = ' ';
    /* Copy second name into name */
    for( j = 0; second_name[j] != '\0' ; j++ )
        name[i+j+1] = second_name[j];
    /* End second name with a space */
    name[i+j+1] = ' ';
    /* Copy last name into name */
    for( k = 0; last_name[k] != '\0' ; k++ )
        name[i+j+k+2] = last_name[k];
    /* End name with a null character */
    name[i+j+k+2] = '\0';
    printf("\n\n");
    printf("%s\n", name);
}
```

Output

VISWANATH PRATAP SINGH

Fig. 4.8 Concatenation of strings

## 4.7 COMPARISON OF TWO STRINGS

Once again, C does not permit the comparison of two strings directly. That is, the statements such as

`if(name1 == name2)`
`if(name == "ABC")`

are not permitted. It is therefore necessary to compare the two strings to be tested, character by character. The comparison is done until there is a mismatch or one of the strings terminates into a null character, whichever occurs first. The following segment of a program illustrates this.

```
i=0;
while(str1[i] == str2[i] && str1[i] != '\0'
&& str2[i] != '\0')
    i +=1;
if (str1[i] == '\0' && str2[i] == '\0')
    printf("strings are equal\n");
else
    printf("strings are not equal\n");
```

## 4.8 STRING-HANDLING FUNCTIONS

Fortunately, the C library supports a large number of string-handling functions that can be used to carry out many of the string manipulations discussed so far. Following are the most commonly used string-handling functions.

| Function | Action |
|---|---|
| strcat() | concatenates two strings |
| strcmp() | compares two strings |
| strcpy() | copies one string over another |
| strlen() | finds the length of a string |

We shall discuss briefly how each of these functions can be used in the processing of strings.

### 4.8.1 strcat() Function

The strcat function joins two strings together. It takes the following form:

```
strcat(string1, string2);
```

string1 and string2 are character arrays. When the function strcat is executed, string2 is appended to string1. It does so by removing the null character at the end of string1 and placing string2 from there. The string at string2 remains unchanged. For example, consider the following three strings:

![](img/fe6da5f61b1e2c77309bbee135b45e35_239_0.png)

```
strcat(part1, part2);
```

![](img/fe6da5f61b1e2c77309bbee135b45e35_240_0.png)

while the statement
will result in:

![](img/fe6da5f61b1e2c77309bbee135b45e35_240_1.png)

![](img/fe6da5f61b1e2c77309bbee135b45e35_240_2.png)

We must make sure that the size of string1 (to which string2 is appended) is large enough to accommodate the final string.

strcat function may also append a string constant to a string variable. The following is valid:

```
strcat(part1,"GOOD");
```

C permits nesting of strcat functions. For example, the statement

```
strcat(strcat(string1,string2), string3);
```

is allowed and concatenates all the three strings together. The resultant string is stored in string1.

### 4.8.2 strcmp() Function

The strcmp function compares two strings identified by the arguments and has a value 0 if they are equal. If they are not, it has the numeric difference between the first nonmatching characters in the strings. It takes the form:
strcmp(string1, string2);
string1 and string2 may be string variables or string constants. Examples are:
strcmp(name1, name2);
strcmp(name1, "John");
strcmp("Rom", "Ram");
Our major concern is to determine whether the strings are equal; if not, which is alphabetically above. The value of the mismatch is rarely important. For example, the statement
strcmp("their", "there");
will return a value of -9 which is the numeric difference between ASCII "i" and ASCII "r". That is, "i" minus "r" in ASCII code is -9. If the value is negative, string1 is alphabetically above string2.

### 4.8.3 strcpy() Function

The strcpy function works almost like a string-assignment operator. It takes the form:
strcpy(string1, string2);
and assigns the contents of string2 to string1. string2 may be a character array variable or a string constant. For example, the statement
strcpy(city, "DELHI");
will assign the string "DELHI" to the string variable city. Similarly, the statement

```
strcpy(city1, city2);
```

will assign the contents of the string variable city2 to the string variable city1. The size of the array city1 should be large enough to receive the contents of city2.

### 4.8.4 strlen() Function

This function counts and returns the number of characters in a string. It takes the form

```
n = strlen(string);
```

Where n is an integer variable, which receives the value of the length of the string. The argument may be a string constant. The counting ends at the first null character.

EXAMPLE 4.8 s1, s2, and s3 are three string variables. Write a program to read two string constants into s1 and s2 and compare whether they are equal or not. If they are not, join them together. Then copy the contents of s1 to the variable s3. At the end, the program should print the contents of all the three variables and their lengths.

The program is shown in Fig. 4.9. During the first run, the input strings are "New" and "York". These strings are compared by the statement

```
x = strcmp(s1, s2);
```

Since they are not equal, they are joined together and copied into s3 using the statement

```
strcpy(s3, s1);
```

The program outputs all the three strings with their lengths.

During the second run, the two strings s1 and s2 are equal, and therefore, they are not joined together. In this case all the three strings contain the same string constant "London".

```
Program
#include <string.h>
main()
{
 char s1[20], s2[20], s3[20];
 int x, l1, l2, l3;
 printf("\nEnter two string constants \n");
 printf("*");
 scanf("%s %s", s1, s2);
 /* comparing s1 and s2 */
 x = strcmp(s1, s2);
 if(x != 0)
 {
  printf("\n\nStrings are not equal \n");
  strcat(s1, s2); /* joining s1 and s2 */
 }
 else
  printf("\n\nStrings are equal \n");
 /* copying s1 to s3 */
 strcpy(s3, s1);
 /* Finding length of strings */
 l1 = strlen(s1);
 l2 = strlen(s2);
 l3 = strlen(s3);
```
