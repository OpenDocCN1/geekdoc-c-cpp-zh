# DISPLAY 3.12 A for Statement

```
1  //Illustrates a for loop.
2 #include <iostream>
3 using namespace std;
4 
5 int main( )
6 {
7     int sum = 0;
8 
9     for (int n = 1; n <= 10; n++) //Note that the variable n is a local
10        sum = sum + n;           //variable of the body of the for loop!
11 
12     cout << "The sum of the numbers 1 to 10 is "
13         << sum << endl;
14     return 0;
15 }
```

Initializing action

Repeat the loop as long as this is true.

Done after each loop body iteration

# Output

```
The sum of the numbers 1 to 10 is 55
```

# DISPLAY 3.13 for Loop with a Multistatement Body

# SYNTAX

```
for (Initialization_Action; Boolean_Expression; Update_Action)
{
    Statement_1
    Statement_2
    .
    .
    .
    Statement_Last
}
```

Body

# EXAMPLE

```
for (int number = 100; number >= 0; number--)
{
    cout << number
        << " bottles of beer on the shelf.\n";
    if (number > 0)
        cout << "Take one down and pass it around.\n";
}
```