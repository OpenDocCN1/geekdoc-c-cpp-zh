# Solved Example 15.3

Write a program to open a file in read mode and to count

+   1. Number of upper case characters in the file
+   2. Number of lower case characters in the file
+   3. Number of digits in the file
+   4. Number of special characters in the file

```
```
#include<iostream.h>
#include<fstream.h>
void main()
{
    /*Open the source file in input mode*/
    ifstream fin;
    fin.open("source.txt");
    char ch;
    /*set all counts to zero before starting the counting loop*/
    int countUpper=0,countLower=0,countDigit=0,countSpecial=0;
    /*The below loop reads and examines one character at a time
    from input file*/
    while(!fin.eof())
    {
        /*Read a character*/
        fin.get(ch);
        /*Check if the character is upper case based on ASCII
        value ranges*/
        if(ch>=65 && ch<=90)
        {
            countUpper++;
        }
        /*Check if the character is lower case based on ASCII
        value ranges*/
        else if(ch>=97 && ch<=122)
        {
            countLower++;
        }
        /*Check if the character is digit based on ASCII value
        ranges*/
        else if(ch>=48 && ch<=57)
        {
            countDigit++;
        }
    }
```
```