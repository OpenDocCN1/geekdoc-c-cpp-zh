```
```cpp
void HandleStuff( CORP_DATA & inputRec, int crntQtr, EMP_DATA empRec,
    double & estimRevenue, double ytdRevenue, int screenX, int screenY,
    COLOR_TYPE & newColor, COLOR_TYPE & prevColor, StatusType & status,
    int expenseType )
{
int i;
for ( i = 0; i < 100; i++ ) {
    inputRec.revenue[i] = 0;
    inputRec.expense[i] = corpExpense[ crntQtr ][ i ];
}
UpdateCorpDatabase( empRec );
estimRevenue = ytdRevenue * 4.0 / (double) crntQtr;
newColor = prevColor;
status = SUCCESS;
if ( expenseType == 1 ) {
    for ( i = 0; i < 12; i++ )
        profit[i] = revenue[i] - expense.type1[i];
}
else if ( expenseType == 2 ) {
    profit[i] = revenue[i] - expense.type2[i];
}
else if ( expenseType == 3 ) {
    profit[i] = revenue[i] - expense.type3[i];
}
```
```
```

What’s wrong with this routine? Here’s a hint: you should be able to find at least 10 different problems with it. Once you’ve come up with your own list, look at the following list:

+   - The routine has a bad name. *HandleStuff()* tells you nothing about what the routine does.
+   - The routine isn’t documented. (The subject of documentation extends beyond the boundaries of individual routines and is discussed in Chapter 32, “Self-Documenting Code.”)
+   - The routine has a bad layout. The physical organization of the code on the page gives few hints about its logical organization. Layout strategies are used haphazardly, with different styles in different parts of the routine. Compare the styles where *expenseType == 2* and *expenseType == 3*. (Layout is discussed in Chapter 31, “Layout and Style.”)
+   - The routine’s input variable, *inputRec*, is changed. If it’s an input variable, its value should not be modified (and in C++ it should be declared *const*). If the value of the variable is supposed to be modified, the variable should not be called *inputRec*.
+   - The routine reads and writes global variables—it reads from *corpExpense* and writes to *profit*. It should communicate with other routines more directly than by reading and writing global variables.