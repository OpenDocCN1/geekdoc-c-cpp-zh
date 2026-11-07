```
```cpp
int number1, number2, sum;
cout << "Enter two numbers: ";
cin >> number1 >> number2;
sum = number1 + number2;
cout << sum << endl;
```
```

The program runs like this:

```
Enter two numbers: 2 3
5
```

The first number entered is stored in number1 and the second number entered is stored in number2. Obviously, you must put a space between the two input values.

String values can be entered the same way. Here is an example:

If the user enters "Mary", the program outputs:

```
Hello, Mary
```

But if the user enters "Mary Smith", the program outputs:

```
Hello, Mary
```

What happened? Remember, the space between the two input values separates the input into distinct values. Since there wasn't a variable to hold “Smith”, the program just ignored it. To read a whole line into a variable, you need to use the getline() function. Here is an example of how the function works: