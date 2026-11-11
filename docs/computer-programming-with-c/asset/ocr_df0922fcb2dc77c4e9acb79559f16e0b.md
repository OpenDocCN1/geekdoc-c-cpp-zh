# SCRATCH PAD

We traverse the complete sentence using a for loop and increment the value of the variable count each time the character ch is found in the sentence. Note that we have used a function `toupper()` while performing matching of `a[i]` and `ch`. This means that we forcefully convert the characters to be compared in upper case so as to ensure that the matching process is case insensitive and the case in which user inputs the data does not make any difference in comparisons. The loop used for comparison is as shown below:

```
```cpp
for(i=0;a[i]!='\0';i++)
{
    if(toupper(a[i])==toupper(ch))
    {
        count++;
    }
}
```
```

Hence, the variable count will represent the frequency of the character in the input sentence.

# NOTES

The function `toupper()` converts a character in uppercase if its currently not in uppercase. It does not affect the character if it is already in uppercase. Also the function does not affect digits and special symbols. As we have applied `toupper()` on both the sides in the comparison, it just ensures that the match is performed ignoring the case, which is the requirement given in the question. We could have also used `tolower()` function instead of `toupper()`, keep in mind the only requirement here is to forcefully get both the sides in an uniform case so that case differences between them(if any) do not hamper the results of comparisons. Both the functions are defined in the header file `ctype.h`, which has to be included in the program.

# Solved Example 6.11

Write a program to take a sentence as input from the user and to reverse the occurrence of words in the sentence. Note that the program should not reverse the characters inside the word. For example, if the user enters the string as "I like computer programming" the output must be:

`programming computer like I`

```
```c
#include<stdio.h>
void main()
{
    char a[100];
```
```