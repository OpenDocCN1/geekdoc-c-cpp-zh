```
```cpp
cout<<"It is a vowel"<<endl;
else if(alphabet=='u')
cout<<"It is a vowel"<<endl;
else
cout<<"It is not a vowel"<<endl;
return 0;
}
```
```

Output:

```
```
Enter an alphabet
e
It is a vowel
```
```

In Listing 15, you can see that the character supplied at run-time is tested successively across the multiple `if-else` statements until a match is found.

The program created by using `if-else` ladders is difficult to read and maintain as program becomes more complex to understand. C++ provides switch statements to overcome these difficulties and complexities in understanding a program, which is discussed next.

# Using the switch Statement

A `switch` statement is a conditional statement that tests a value against different values. If the value is matched, the corresponding group of statements is executed. A switch statement begins with the `switch` keyword that is followed by a value expression in the parenthesis (). It is a combination of multiple case labels that must be separated by the `break` statement. Every case label contains a constant value that is matched against the value, which is specified in the `switch` expression. If the value is matched, the statements of that case label are executed. In addition, you can specify the `default` label, which is executed when the value, which is specified in the `switch` expression, does not match with the given case labels. The syntax to use switch statement is:

```
```cpp
switch(expression)
{
    case value1: statement1;
    break;
    case value2: statement2;
    break;
    case value3: statement3;
    break;
    .
    .
    .
    default: default_statement;
}
```
```