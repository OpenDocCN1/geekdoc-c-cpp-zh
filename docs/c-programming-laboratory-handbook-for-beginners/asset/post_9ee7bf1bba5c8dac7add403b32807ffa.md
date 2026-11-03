
## String Structure

When a compiler assigns a string to character array then it automatically appends **null character ('\0')** at the end of the string. Thus, size of string = original length of string + 1.

```
char name[7];
name = "TECHNO";
```

| 'T' | 'E' | 'C' | 'H' | 'N' | 'O' | '\0' |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |

## Read Strings

To read a string, we can use *scanf()* function with format specifier `%s`.

```
char name[50];
scanf("%s", name);
```

The above format allows accepting only that string which does not have any blank space, tab, new line, form feed, or carriage return.

However, C supports a library function known as *gets* that allows reading a string of text containing whitespaces. This is a simple function with one-string parameter.

```
gets(name);
```

where name is a string variable.

## Write Strings

To write a string, we can use *printf()* function with format specifier `%s`.

```
char name[50];
scanf("%s", name);
printf("%s", name);
```

Another and more convenient way of printing string is to use the function *puts*. This is a simple function with one-string parameter.

```
puts(name);
```

where name is a string variable.

## String Functions

"*string.h*" is a header file which includes the declarations, functions, constants of string-handling utilities. These string functions are widely used today by many programmers to deal with string operations.

Some of the standard member functions of *string.h* header files are:

| Function Name | Description |
| --- | --- |
| strlen() | Returns the length of a string. |
| strlwr() | Returns upper case letter to lower case. |
| strupr() | Returns lower case letter to upper case. |
| strcat() | Concatenates two strings. |
| strcmp() | Compares two strings. |
| strrev() | Returns reverse of a string. |
| strcpy() | Copies a string from source to destination. |

## Description

Here the function reverse (str) is called by the function main( ) by passing the value of string. Function reverse(str) processes the string array by using its local variables, so as to reverse the contents. Once completed, function reverse(str) displays the result, which is reverse of the given string.

## Algorithm

Start  
**Step 1:** Input the string  
**Step 2:** Print the string  
**Step 3:** Call function reverse ()  
Stop

Algorithm to reverse a string.

- 1. Calculate the length
  - For *i* = 0 to str1[*i*] ≠ Null in step of 1
  - end For
- 2. len = *i*
- 3. initialize *j* = 0, *i* = len-1
- 4. swap(str1[*j*], str1[*i*])
- 5. *j* = *j* + 1, *i* = *i* -1
- 6. repeat steps 4 to 5 until *i* > *j*
- 7. Print “reversed string”

## Flowchart

![](img/dad8bddd927fabdab2417ecbf1eb24eb_134_0.png)

## Program

```c
#include<stdio.h>
void main()
{
  char str1[20];
  void reverse(char str1[]);
  printf("\n Enter the string to be reversed: ");
  gets(str1);
  printf("\n\n User Entered String: ");
  printf("%s\n",str1);
  reverse(str1); // Function call
}
void reverse(char str1[])
{
  int i,j,len,temp;
  // This loop finds the length of the string.
  for(i=0;str1[i]!='\0';i++)
  {
    ;
  }
  len=i;
  //This loop reverses the string str1 in place.
  for(j=0,i=len-1; i>j; i--,j++)
  {
    temp=str1[i];
    str1[i]=str1[j];
    str1[j]=temp;
  }
  printf("\n Reversed String: ");
  puts(str1);
}
```

## Output

- 1. Enter the string to be reversed: KLECET Belgaum  
  User Entered String: KLECET Belgaum  
  Reversed String: muagleB TECELK
- 2. Enter the string to be reversed: hello  
  User Entered String: hello  
  Reversed String: olleh
- 3. Enter the string to be reversed: Good morning  
  User Entered String: Good morning  
  Reversed String: gninrom dooG

## Outcomes

- Able to optimally reverse the string without using extra variables.
- Capable of writing user-defined functions for most of the standard string library functions.

## Related Programs

### Program 1

C program to compare two strings without using strcmp.

```c
#include<stdio.h>
#include<string.h>
void main()
{
  char a[100], b[100];
  int result;
  printf("\n Enter the first string: ");
  gets(a);
  printf("\n Enter the second string: ");
  gets(b);
  result=compare(a,b);
  if(result==0)
  printf("\n Entered strings are equal....\n");
  else
  printf("\n Entered strings are not equal.....\n");
}
int compare(char a[],char b[])
{
  int c=0;
  while(a[c]==b[c])
  {
    if(a[c]=='\0'||b[c]=='\0')
    break;
    c++;
  }
  if(a[c]=='\0'&&b[c]=='\0')
  return 0;
  else
  return -1;
}
```

### Output

- 1. Enter the first string: welcome  
  Enter the second string: welcome  
  Entered strings are equal....  
  Press any key to continue . . .
- 2. Enter the first string: computer concepts  
  Enter the second string: c programming  
  Entered strings are not equal.....  
  Press any key to continue . . .
- 3. Enter the first string: good morning  
  Enter the second string: good morning  
  Entered strings are equal....  
  Press any key to continue . . .
- 4. Enter the first string: good bad  
  Enter the second string: good  
  Entered strings are not equal.....  
  Press any key to continue . . .

### Program 2

C program to check whether a given string is a palindrome or not.

```c
#include<stdio.h>
#include<string.h>
main()
{
char text[100];
int begin, middle, end, length=0;
printf("\n Enter string: ");
gets(text);
    while(text[length]!='\0')
        length++;
        end=length-1;
        middle=length/2;
        for(begin=0;begin<middle;begin++ )
        {
            if(text[begin]!=text[end])
            {
                printf("\n\n String Is Not palindrome....\n\n");
                break;
            }
            end--;
        }
        if (begin==middle)
            printf("\n\n String Is Palindrome...\n\n");
            return 0;
}
```

### Output

- 1. Enter string: madam  
  String Is Palindrome...  
  Press any key to continue . . .
- 2. Enter string: programming  
  String Is Not palindrome....  
  Press any key to continue . . .

### Program 3

C program to find the length of a string without using any built-in function.

```c
#include<stdio.h>
void main()
{
    char str1[20];
    int i,count=0;
    printf("\n Enter the string: ");
    gets(str1);
    for(i=0;str1[i]!='\0';i++)
    {
        count++;
    }
        printf("\n The length of a string is:%d\n",count);
}
```

### Output

- 1. Enter the string: welcome to ccp lab  
  The length of a string is:18  
  Press any key to continue . . .
- 2. Enter the string: work is worship  
  The length of a string is:15  
  Press any key to continue . . .

## Practice Programs

- 1. Design and develop a C program to swap two strings.
- 2. Design and develop a C program to remove spaces, blanks from a string.
- 3. Design and develop a C program to remove vowels from a string.

## Term-Work 16

Design and develop a function matchany (s1, s2) that returns the first location in the string s1 where any character from the string s2 occurs, or –1 if s1 contains no character from s2. Do not use the standard library function that does a similar job! Invoke the function matchany (s1, s2) from the main for different strings and print both the strings and the return value from the function matchany (s1, s2).

- Competency in using functions.
- To understand manipulation of strings.

Here the function matchany(s1, s2) is called by the function main( ) by passing the values of two character strings. Function matchany(s1, s2) processes the string arrays using local variables, to find any character of string s2 matching any character in string s1. If any matching character is found then the function matchany(s1, s2) will display the position of the matched character in s1, else –1 is displayed.

Start  
**Step 1:** Input string1  
**Step 2:** Input string2  
**Step 3:** Call function matchany (str1, str2)  
**Step 4:** IF j = –1 then  
  Print “No matching character found”  
  else  
  Print “Match found at position j”  
  END IF  
Stop
