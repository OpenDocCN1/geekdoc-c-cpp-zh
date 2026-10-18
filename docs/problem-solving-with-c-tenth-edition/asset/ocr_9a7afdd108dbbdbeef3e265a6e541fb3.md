For example, suppose the following cout statement appears somewhere after this magic formula and suppose the value of price is 78.5:

```
cout << "The price is $" << price << endl;
```

The output will then be as follows:

```
The price is $78.50
```

You may use any other nonnegative whole number in place of 2 to specify a different number of digits after the decimal point. You can even use a variable of type int in place of the 2. We will explain this magic formula in detail in Chapter 6. For now you should think of this magic formula as one long instruction that tells the computer how you want it to output numbers that contain a decimal point.

If you wish to change the number of digits after the decimal point so that different values in your program are output with different numbers of digits, you can repeat the magic formula with some other number in place of 2. However, when you repeat the magic formula, you only need to repeat the last line of the formula. If the magic formula has already occurred once in your program, then the following line will change the number of digits after the decimal point to 5 for all subsequent values of type double that are output:

```
cout.precision(5);
```

# Input Using cin

You use cin for input more or less the same way you use cout for output. The syntax is similar, except that cin is used in place of cout and the arrows point in the opposite direction. For example, in the program in Display 2.1, the variables numberOfBars and oneWeight were filled by the following cin statements (shown along with the cout statements that tell the user what to do):

# Outputting Values of Type double

If you insert the following “magic formula” in your program, then all numbers of type double (or any other type that allows for digits after the decimal point) will be output in ordinary, everyday notation with two digits after the decimal point:

```
cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout.precision(2);
```

You can use any other nonnegative whole number in place of the 2 to specify a different number of digits after the decimal point. You can even use a variable of type int in place of the 2.