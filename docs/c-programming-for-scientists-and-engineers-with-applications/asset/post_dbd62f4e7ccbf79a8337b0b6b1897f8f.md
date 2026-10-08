
Notice the first occurrence of character 'c' is in the word "electronic" because the "C" in "Computers" is capitalized. In the output, the string returned starts with the first occurrence of the character 'c' and continues to the end of the string. If the character is not present in the string, which is the case with the character 'k', the function strchr returns a null string.

Function: strchr This function searches for the rightmost or last occurrence of a specified character in the string and returns the rest of the string. The following-code shows the use of this function.

```c
#include <stdio.h>
#include <string.h>

int main() {
  char strname[40] = "Computers are electronic machines";
  printf("strchr string is: %s\n", strchr(strname, 'c'));
  printf("strchr string is: %s\n", strchr(strname, 'k'));
  return 0;
}
```

The output is as follows:
strchr string is: chines
strchr string is:

Notice that the string returned is "chines", which is the string starting from the last occurrence of the character 'c' to the end of the string strname. If the character is not in the string the function strchr returns a null string.

## 9.4.6 Review Questions

Indicate whether the following statements are true or false.
a. There are no operators in C to manipulate character strings.
b. All string concatenation functions have three arguments.
c. Two strings cannot be compared using a relational operator to generate a logical value.
d. String comparison functions must be used to compare two strings to generate a value > 0, = 0, or < 0.
e. The string copy function has two forms, one with two arguments and the other with three arguments.
f. In the function strstr, if the string is not found inside another string the function returns a null value.
g. In the function strchr, if the character is found, the position of the character is returned.

2. Write the code to concatenate the following strings to form a sentence.

- Germany
- is
- in
- Europe

3. Compare the following strings and show the logical value generated for the first string to be greater than the second string, the first string to be less than the second string, and the first string to be equal to the second string.

- computers and and compute
- Value Line and limited value
- constant and concern
- Collaboration and Collaborator

4. Copy str2 to str1 and show what is in the storage before and after the copy.

a. str1[] = "Vanlines used for transportation";
   str2[] = "valentines day";

b. str1[] = "computers";
   str2[] = "electrons";

c. str1[] = "communications";
   str2[] = "electronic communications";

## 9.5 Sample Programs

These programs show the storage and manipulation of strings. These programs also show the sorting and searching operations performed on string arrays. The results are presented along with the code.

## 9.5.1 Creating a List of Names from a File

A list of names is stored in a file. Make a copy of the file, temporarily storing the names in an array.

Problem: Write a program to input and store a list of names in an array, then put them.

Method
- Declare an array for strings.
- Use a function to input strings from a file into the array.
- Use another function to write the strings to a second file.

Pseudocode
```
main:
  funcinput()
  funcoutput()
  stop

funcinput:
  for each string
    input the string
  end for
  return
end

funcoutput:
  for each string
    output the string
  end for
  return
end
```

Program
```c
*********************************************************************************/
/*
/* main: Input and Store Strings
/* **********************************************************************************/
/* Input Variables:
/* name[NUM] [STRLNG] - list of names
/* Output Variables:
/* name[NUM] [STRLNG] - list of names
/*
/* Functions Called:
/* funcinput() - function to input names
/* funcoutput() - function to output names
/* **********************************************************************************/

#include <stdio.h>
#include <string.h>

#define NUM 10
#define STRLNG 40

void funcinput(char [][STRLNG]);
void funcoutput(char [][STRLNG]);

int main()
{
    char name[NUM] [STRLNG];

    funcinput(name);
    funcoutput(name);

    return 0;
}
*********************************************************************************/
/*
/* funcinput - Input Strings
/*
*********************************************************************************/
/*
/* Input Parameters:
/* strname[NUM][STRLNG] - array storage
/*
/* Output Parameters: - list of names
/* name[NUM] [STRLNG] */

# Characters and Strings

```c
/* Data Files used: */
/* strinfile.dat - input data file */
/******************************************************************/
```

```c
void funcinput(char name[], STRLNG)
{
    FILE *inptr;
    int i;

    inptr = fopen("strinfile.dat", "r");

    for(i = 0; i < NUM; i++)
        fgets(name[i], STRLNG, inptr);

    fclose(inptr);
    return;
}
```

```c
******************************************************************
/*
funcoutput - Output the Strings
 */
******************************************************************
/*
/* Input Parameters:
/* name[NUM] [STRLNG] - list of names */
/*
/* Data Files used: */
/* outfile.dat - output data file */
/**************************************************/
```

```c
void funcoutput(char name[], STRLNG)
{
    FILE *outptr;
    int i;

    outptr = fopen("outfile.dat", "w");

    for(i = 0; i < NUM; i++)
        fputs(name[i], outptr);

    fclose(outptr);
    return;
}
```

In this program every string is allocated 40 locations, which is specified in the second dimension of the string. There is a large variation in the string lengths, hence wasted storage. In Chapter 10 we will show how to store strings more efficiently.

## 9.5.2 Sorting a List of Names

Often there is a need for strings to be in order. In engineering applications the names of parts and part numbers of various machines such as machine shop machinery, airplanes, cars, farm equipment, and other engineering equipment may need to stored in order.

# Sorting Strings Stored as a List

Problem Write a program to sort the names stored in a list into alphabetical order. Print the unsorted and sorted names.

Method
- Input the names into a list.
- Output the unsorted names.
- Sort the names in alphabetical order.
- Output the sorted names.

Data
Input 11 names.

Pseudocode
```
main:
  call funcinput
  call funcsort
  call funcoutput
stop
funcinput:
  for each name
    input the name
  end for
  return
end
funcsort:
  for each name i
    for each name j > i
      if ( name j should be followed by name i)
        swap the names
      end if
    end for
end for
end
```

```c
fcoutput:
for each name
    output the name
end for
return
end
```

# Program
```c
********************************************************************
/*
/*   main: Sort the String in Alphabetical Order
/*
********************************************************************
/*   Input Variables:
/*   name[NUMSTR][STRLNG] – list of names
/*
/*   Output Variables:
/*   name[NUMSTR][STRLNG] – list of names
/*
/*   Functions Called:
/*   finput - function to input the data
/*   funscort - function to sort the data
/*   fcoutput - function to output the data
/*
/*
/*   Data Files Used:
/*   out.datsort – output data file
/*
********************************************************************
```

```c
#include <stdio.h>
#include <string.h>

#define NUMSTR 11
#define STRLNG 40

void fininput(char [][STRLNG]);
void funscort(char [][STRLNG]);
void fcoutput(char [][STRLNG]);

FILE *outptr;
```
