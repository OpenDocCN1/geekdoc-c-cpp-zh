```
```cpp
if (i % 2 == 0)
    pi = pi + (1 / (2 * i + 1));
else
    pi = pi - (1 / (2 * i + 1));

for (i = 0; i < n; i++)
{
    pi = 0;
    pi = 4 * pi;
}

cout << endl << "pi = " << pi << endl;

return 0;
}
```
```

+   3. Rewrite the program of Example 5-5, Telephone Digits. Replace the statements from Line 10 to Line 28 so that the program uses only a switch structure to find the digit that corresponds to an uppercase letter.

+   4. The program Telephone Digits outputs only telephone digits that correspond to uppercase letters. Rewrite the program so that it processes both uppercase and lowercase letters and outputs the corresponding telephone digit. If the input is something other than an uppercase or lowercase letter, the program must output an appropriate error message.

+   5. To make telephone numbers easier to remember, some companies use letters to show their telephone number. For example, using letters, the telephone number 438-5626 can be shown as GET LOAN. In some cases, to make a telephone number meaningful, companies might use more than seven letters. For example, 225-5466 can be displayed as CALL HOME, which uses eight letters. Write a program that prompts the user to enter a telephone number expressed in letters and outputs the corresponding telephone number in digits. If the user enters more than seven letters, then process only the first seven letters. Also output the – (hyphen) after the third digit. Allow the user to use both uppercase and lowercase letters as well as spaces between words. Moreover, your program should process as many telephone numbers as the user wants.

+   6. Write a program that reads a set of integers and then finds and prints the sum of the even and odd integers.

+   7. Write a program that prompts the user to input a positive integer. It should then output a message indicating whether the number is a prime number. (Note: An even number is prime if it is 2. An odd integer is prime if it is not divisible by any odd integer less than or equal to the square root of the number.)

+   8. Let n = d_k d_{k-1} d_{k-2} ... d_1 d_0 be an integer and t = d_0 - d_1 + d_2 - ... + (-1)^k d_k. It is known that n is divisible by 11 if and only if t is divisible by 11. For example, suppose that n = 8784204. Then, t = 4 - 0 + 2 - 4 + 8 - 7 + 8 = 11. Because 11 is divisible by 11, it follows that 8784204 is divisible by 11. If n = 54063297, then t = 7 - 9 + 2 - 3 + 6 - 0 + 4 - 5 = 2. Because 2 is not