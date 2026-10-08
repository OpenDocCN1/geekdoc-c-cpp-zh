The phrase “double interestRate;” means: “please make room in memory for a variable called interestRate that will store a real number”. There are two keywords you can use in C++ to store a real number. You can use float which stores a floating point number to a certain precision, or you can use double which uses twice as much memory but is much more precise. Computer memory is cheaper now than it was in 1969, so float isn’t used much any more. The strange name double lives on for backwards compatibility. If you think of double as meaning “real number” you won’t get into much trouble.

Notice the semi-colon at the end of the statement “int principal;”. Every statement in C++ ends with a semi-colon. You can think of it as the C++ equivalent of a full stop in English. However, C++ is much fussier than the English language—if you forget a single semi-colon, the program won’t work.

The line

```
cout << "How much are you investing?\n";
```

writes the text “How much are you investing?” to the screen and then starts a new line. Anything enclosed in quotation marks is interpreted as text rather than computer code by C++. The special sequence of characters \n means insert a new line.

The line

```
cin >> principal;
```

means read a number typed by the user and store it in the variable principal.

The next few lines behave much the same.

The mathematical heart of our calculation is given by the lines:

```
double finalBalance =
    pow(1.0 + interestRate * 0.01, numberOfYears)
    * principal;
double interest = finalBalance - principal;
```

These lines make room in memory for two variables called finalBalance and interest and immediately assign values to these variables.

The computation of the interest is simple. It is just the finalBalance minus the principal.

The final balance is computed using the formula $P(1+i)^T$ where $P$ is short for principal, etc. Our code just expands the variable names, replaces multiplication with *, and uses the function pow to raise a number to a given power. In general pow(a,b) = $a^{b}$.

Notice that C++ doesn’t care if your statements go over multiple lines. This is great if you want to write a long formula. The price you have to pay is that you must end all statements with a semi-colon, since C++ doesn’t look

of values that depends upon whether you have a 32 bit or a 64 bit computer, but that really isn’t important right now.