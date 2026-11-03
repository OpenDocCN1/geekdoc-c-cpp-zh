What happens if we enter a floating point number instead of an integer? The fractional part may be stripped away! Also, scanf may skip reading further input.

When the scanf reads a particular value, reading of the value will terminate as soon as the number of characters specified by the field width is reached (if specified) or until a character that is not valid for the value being read is encountered. In the case of integers, valid characters are an optionally signed sequence of digits.

An input field may be skipped by specifying * in the place of field width. For example, the statement

```
scanf("%d %*d %d", &a, &b)
```

will assign the data

123 456 789

as follows:

+   123 to a
+   456 skipped (because of *)
+   789 to b

The data type character d may be preceded by 'l' (letter ell) to read long integers.

# Example 5.4

Various input formatting options for reading integers are experimented with in the program shown in Fig. 5.4.

The first scanf requests input data for three integer values a, b, and c, and accordingly three values 1, 2, and 3 are keyed in. Because of the specification %*d the value 2 has been skipped and 3 is assigned to the variable b. Notice that since no data is available for c, it contains garbage.

The second scanf specifies the format %2d and %4d for the variables x and y respectively. Whenever we specify field width for reading integer numbers, the input numbers should not contain more digits than the specified size. Otherwise, the extra digits on the right-hand side will be truncated and assigned to the next variable in the list. Thus, the second scanf has truncated the four digit number 6789 and assigned 67 to x and 89 to y. The value 4321 has assigned to the first variable in the immediately following scanf statement.

```
Program
/******************************************************/
/*                                                    */
/*              READING INTEGER NUMBERS              */
/*                                                    */
/******************************************************/
/*
main()
{
    int a,b,c,x,y,z;
    int p,q,r;

    printf("Enter three integer numbers\n");
    scanf("%d %*d %d",&a,&b,&c);
    printf("%d %d\n\n",a,b,c);

    printf("Enter two 4-digit numbers\n");
    scanf("%2d %4d",&x,&y);
    printf("%d %d\n\n",x,y);

    printf("Enter a two digit integers\n");
```