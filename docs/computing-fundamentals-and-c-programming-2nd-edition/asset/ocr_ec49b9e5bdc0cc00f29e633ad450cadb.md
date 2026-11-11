```
```c
main()
{ /*----- DECLARATION STATEMENTS -----*/
    int year;
    float amount, value, inrate;
/*----- ASSIGNMENT STATEMENTS -----*/
    amount = PRINCIPAL;
    inrate = 0.11;
    year = 0;
/*----- COMPUTATION STATEMENTS -----*/
/*----- COMPUTATION USING While LOOP -----*/
    while(year <= PERIOD)
    { printf("%2d   %8.2f\n",year, amount);
      value = amount + inrate * amount;
      year = year + 1;
      amount = value;
    }
/*----- while LOOP ENDS -----*/
}
/*----- PROGRAM ENDS -----*/
```
```

**Fig. 3.5** *Program for investment problem*

Let us consider the **new features** introduced in this program. The second and third lines begin with **#define** instructions. A **#define** instruction defines value to a *symbolic constant* for use in the program. Whenever a symbolic name is encountered, the compiler substitutes the value associated with the name automatically. To change the value, we have to simply change the definition. In this example, we have defined two symbolic constants **PERIOD** and **PRINCIPAL** and assigned values **10** and **5000.00** respectively. These values remain constant throughout the execution of the program.

| | |
|---|---|
| 0 | 5000.00 |
| 1 | 5550.00 |
| 2 | 6160.50 |
| 3 | 6838.15 |
| 4 | 7590.35 |
| 5 | 8425.29 |
| 6 | 9352.07 |
| 7 | 10380.00 |
| 8 | 11522.69 |
| 9 | 12790.00 |
| 10 | 14197.11 |

**Fig. 3.6** *Output of the investment program*