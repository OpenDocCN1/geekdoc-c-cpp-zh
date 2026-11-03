# 1. /* Write a program to test the given string is palindrome or not. implement the program by using _Bool datatype */

```
#include<stdio.h>
#include<string.h>
enum _Bool{false,true}; // _Bool DataType which is capable of storing the vales 0 and 1
enum _Bool IsPalindrome(char string[]) // _Bool datatype
{
    int left,right,len=strlen(string);
    enum _Bool matched=true; // _Bool datatype
    if(len==0)
        return 0;
    left=0;
    right=len-1;
    /* Compare the first and last letter,second & second last & so on */
    while(left<right&&matched)
    {
        if(string[left]!=string[right])
            matched=false;
        else
        {
            left++;
            right--;
        }
    }
    return matched;
}

int main()
{
    char string[40];
    clrscr();
    printf("****Program to test if the given string is a palindrome****\n");
    printf("Enter a string:");
    scanf("%s",string);
    if(IsPalindrome(string))
        printf("The given string %s is a palindrome\n",string);
    else
        printf("The given string %s is not a palindrome\n",string);
    getch();
    return 0;
}
```