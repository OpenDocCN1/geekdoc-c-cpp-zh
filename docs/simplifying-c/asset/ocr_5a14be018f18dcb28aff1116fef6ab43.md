```
```c
/* Beginning of main function */
main()
{
    /* Declare variables */
    int i_first;
    double d_second;
    char c_choice, c_temp;

    printf("Enter the value of i_first: ");
    scanf("%d", &i_first);
    printf("Enter the value of d_second: ");
    scanf("%lf", &d_second);

    /* Use temporary variable to clear the stream */
    c_temp=getchar();

    printf("\nEnter the value of c_choice: ");
    scanf("%c", &c_choice);
    printf("\nValues of the variables are %d %lf %c\n",
           i_first, d_second, c_choice);
    return;
}
/* End of function main */
```
```

**Output 1:**
Enter the value of i_first: 45
Enter the value of d_second: 78.25
Enter the value of c_choice: h
Values of the variables are 45 78.250000 h

**Output 2:**
Enter the value of i_first: r
Enter the value of d_second:
Enter the value of c_choice:
Values of the variables are -28851 0.000000

**Output 3:**
Enter the value of i_first: 56
Enter the value of d_second: h
Enter the value of c_choice:
Values of the variables are 56 0.000000

In Program 3, the use of statement c_temp = getchar(); solves our problem and we are able to get the desired output, as seen in Output 1. One more interesting thing to note here is that the compiler terminates the reading of a value if any invalid character is encountered. Observe that in Output 2, after the message *Enter the value of i_first*, the compiler expected an integer value, but received a character. In this case, the compiler terminated the input and directly gave the output. The output here is considered to be garbage as it is of no use. Similar case happened in Output 3.

C allows us to build derived data type from the existing primitive data types. One such data type is array. Character array in C is represented as strings. Let us now learn how to enter data in strings. The format code %s allows the user to read a string from the keyboard. Program 4 illustrates how to read and display strings in C: