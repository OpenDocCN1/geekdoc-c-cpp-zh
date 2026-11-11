```
scanf("%d", &number);
```

When this statement is encountered by the computer, the execution stops and waits for the value of the variable **number** to be typed in. Since the control string “%d” specifies that an integer value is to be read from the terminal, we have to type in the value in integer form. Once the number is typed in and the ‘Return’ Key is pressed, the computer then proceeds to the next statement. Thus, the use of **scanf** provides an interactive feature and makes the program ‘user friendly’. The value is assigned to the variable **number**.

# # WORKED-OUT PROBLEM 4.4

Sample program 3 discussed in Chapter 3 can be converted into a more flexible interactive program using **scanf** as shown in Fig. 4.10.

In this case, computer requests the user to input the values of the amount to be invested, interest rate and period of investment by printing a prompt message

Input amount, interest rate, and period

and then waits for input values. As soon as we finish entering the three values corresponding to the three variables amount, inrate, and period, the computer begins to calculate the amount at the end of each year, up to ‘period’ and produces output as shown in Fig. 4.10.

```
~~~c
Program

main()
{
    int year, period ;
    float amount, inrate, value ;

    printf("Input amount, interest rate, and period\n\n") ;
    scanf ("%f %f %d", &amount, &inrate, &period) ;
    printf("\n") ;
    year = 1 ;

    while( year <= period )
    {
        value = amount + inrate * amount ;
        printf("%2d Rs %8.2f\n", year, value) ;
        amount = value ;
        year = year + 1 ;
    }
}

Output

Input amount, interest rate, and period

10000 0.14 5
~~~
```