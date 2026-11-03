```
(d) for (x = 1, x > 10; x = x + 1)
{
    ___
    ___
}
(e) m = 1;
n = 0;
for ( ; m<n +10; ++n);
printf("Hello\n");
m = m+10
(f) for (p = 10; p > 0;)
p = p - 1;
printf("%sf", p);
```

4.28 Write a for statement to print each of the following sequences of integers:
(a) 1, 2, 4, 8, 16, 32
(b) 1, 3, 9, 27, 81, 243
(c) -4, -2, 0, 2, 4
(d) -10, -12, -14, -18, -26, -42

4.29 Change the following for loops to while loops:
(a) for (m = 1; m < 10; m = m + 1)
printf(m);
(b) for ( ; scanf("%d", &m) != -1;)
printf(m);

4.30 Change the for loops in Exercise 4.14 to do loops.

# Programming Exercises

4.1 Write a program, which reads your name from the keyboard and outputs a list of ASCII codes, which represent your name.

4.2 Write a program to do the following:
(a) To output the question "Who is the inventor of C ?"
(b) To accept an answer.
(c) To print out "Good" and then stop, if the answer is correct.
(d) To output the message 'try again', if the answer is wrong.
(e) To display the correct answer when the answer is wrong even at the third attempt and stop.

4.3 Write a program to extract a portion of a character string and print the

4.31 What is the output of following code?
```
int m = 100, n = 0;
while ( n != 0 )
{
    if ( m < 10 )
        break;
    m = m-10;
}
```

4.32 What is the output of the following code?
```
int m = 0 ;
do
{
    if (m > 10 )
        continue ;
    m = m + 10 ;
} while ( m < 50 ) ;
printf("%d", m);
```

4.33 What is the output of the following code?
```
int n = 0, m = 1 ;
do
{
    printf(m) ;
    m++ ;
}
while (m <= n ) ;
```

4.34 What is the output of the following code?
```
int n = 0, m ;
for (m = 1; m <= n + 1 ; m++ )
printf(m);
```

4.35 When do we use the following statement?
for ( ; ; )

extracted string. Assume that m characters are extracted, starting with the nth character.

4.4 Write a program which will read a text and count all occurrences of a particular word.

4.5 Write a program which will read a string and rewrite it in the alphabetical order. For example, the word STRING should be written as GINRST.

4.6 Write a program to replace a particular word by another word in a given string. For example, the word "PASCAL" should be replaced by "C" in the text "It is good to program in PASCAL language."