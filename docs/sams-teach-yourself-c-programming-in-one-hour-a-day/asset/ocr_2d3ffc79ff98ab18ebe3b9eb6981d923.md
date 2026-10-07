void print_msg(void)
{
    puts("This is a message to print ");
}

5. There should not be a semicolon at the end of the function header.

6. Only the larger_of() function needs to be changed:

```
21: int larger_of( int a, int b)
22: {
23:     int save;
24:
25:     if (a > b)
26:     save = a;
27:     else
28:     save = b;
29:
30:     return save;
31: }
```

7. The following assumes that two values are integers and an integer is returned:

```
int product( int x, int y)
{
    return (x * y);
}
```

8. The following listing checks the second value passed to verify that it is not 0. Division by zero causes an error. You should never assume that the values passed are correct. However, this only prevents a division-by-zero error at the function level. It will return 0 to the calling program, because the program needs to always return an integer variable type. To avoid division by error, your program should check the value of b before you call the divide_em function.

```
int divide_em( int a, int b)
{
    int answer = 0;

    if(b == 0)
        answer = 0;
    else
        answer = a/b;

    return answer;
}
```

9. Although the following code uses main(), it could use any function. Lines 9, 10, and 11 show the calls to the two functions. Lines 13 through 16 print the values. To run this listing, you need to include the code from exercises 7 and 8 after line 19.