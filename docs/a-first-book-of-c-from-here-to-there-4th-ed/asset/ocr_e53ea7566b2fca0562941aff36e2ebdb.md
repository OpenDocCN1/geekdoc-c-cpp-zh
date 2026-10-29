```
const int MAXCOUNT = 5;
int count;
double num, total, average;

total = 0.0;

for (count = 0; count < MAXCOUNT; count++)
{
    cout << "Enter a number: ";
    cin >> num;
    total = total + num;
}

average = total / count;
cout << "The average of the data entered is " << average
    << endl;

return 0;
}
```

The for statement in Program 5.11 creates a loop that’s executed five times. The user is prompted to enter a number each time through the loop. After each number is entered, it’s added to the total immediately. Although total was initialized to 0 before the for statement, this initialization could have been included with the initialization of count, as follows:

```
for (total = 0.0, count = 0; count < MAXCOUNT; count++)
```

Additionally, the declarations for both total and count could have been included with their initializations inside the initializing list, as follows:

```
for (double total = 0.0, int count = 0; count < MAXCOUNT; count++)
```

Any of these for constructs is considered a good programming practice. Which one you choose is simply a matter of your own programming style.

# Nested Loops

In many situations, using a loop within another loop, called a nested loop, is convenient. Here’s a simple example of a nested loop:

```
for(i = 1; i <= 5; i++) // start of outer loop <----+
{
    cout << "\n i is now " << i << endl; //
    //
    for(j = 1; j <= 4; j++) // start of inner loop |
    cout << "  j = " << j; // end of inner loop |
} // end of outer loop <----+

```