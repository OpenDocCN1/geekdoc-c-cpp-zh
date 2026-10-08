Answers to Chapter 7 Labs

# Mini-Quiz 7-3

+   1. while (evenNum < )
{
    cout << evenNum << endl;
evenNum += 2; (or evenNum = evenNum + 2)
}// end while
2. a. for (int x = 10; x <= 100; x = x + 10)
3. d 110
4. for (int x = 25; x > 0; x = x - 5) (You can also use
x -= 5 as the update argument.)
5. 0
6. for (int num = 2; num < 9; num += 2) (You can also use
num = num + 2 as the update argument.)

# Answers to Chapter 7 Labs

# LAB 7-1 Stop and Analyze

+   1. The program inputs a temperature. It uses two processing
items: a counter that keeps track of the number of tempera-
tures and an accumulator that totals the temperatures. The
program displays the average temperature.
2. The number 999 was as a sentinel value because it's not a valid
outside temperature. A negative number was not chosen as a sentinel
value because the temperature outside can be below zero.
3. The selection on Lines 32 through 43 is necessary to pre-
vent the program from calculating the average temperature when the
counter variable (numberOfItems) contains the number 0. Dividing
by zero causes the program to end abruptly with.
4. Although the statement on Lines 35 and 36 don't need both type
casts, it needs at least one of them. Without at least one type cast,
t quotient obtained when dividing the contents of the totalTemp
by the variables of the numberOfItems variable would be
an integer (rather than a double). This is because both of
those variables have the int type; when you divide two integers,
t result is an integer. At least one type cast is needed to force the
computer to perform the division using double numbers, which will
result in a quotient that is also a double number.
5. The cout << fixed << setprecision(1) the statement in output in fixed-point notation with
one decimal place.

![](bbox=[0.122, 0.517, 0.178, 0.584])