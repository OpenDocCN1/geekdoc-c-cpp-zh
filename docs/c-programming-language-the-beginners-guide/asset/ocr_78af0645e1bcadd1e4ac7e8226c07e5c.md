# Strcat / Concatenation

This is only partial code. We’re going to figure out how to stick these two and to make another new string. In many programming languages, the addition operator does the trick. For example, some programming languages might write the code this way to connect the two strings together to make a new string:

```
```c
#include

int main()
{
    char first[] = "I would like to go ";
    char second[] = "from here to there\\n";
    printf("%s\\n", first+second);
    return(0);
}
```
```

However, in the C programming language, this would not work. You could display both strings back to back, but that’s not the solution we’re after. What you need to do is to stick the strings together. Now, rather than say, “stick the strings together,” C programmers say, “concatenate,” which comes from the Latin word for sticking two strings together.

But before that, fix up the code. First, create a storage location, or a buffer, for the resulting two strings.

```
```c
#include
```
```