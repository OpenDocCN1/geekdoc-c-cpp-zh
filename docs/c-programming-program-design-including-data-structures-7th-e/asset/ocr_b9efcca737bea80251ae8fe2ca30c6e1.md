```
```cpp
case 1:
case -1:
    oddCount++;
} //end switch
} //end classifyNumber

void printResults(int zeroCount, int oddCount, int evenCount)
{
    cout << "There are " << evenCount << " evens, "
         << "which includes " << zeroCount << " zeros"
         << endl;

    cout << "The number of odd numbers is: " << oddCount
         << endl;
} //end printResults
```
```

**Sample Run:** In this sample run, the user input is shaded.

```
Please enter 20 integers.
The numbers you entered are:
0 0 12 23 45 7 -2 -8 -3 -9 4 0 1 0 -7 23 -24 0 0 12
0 0 12 23 45 7 -2 -8 -3 -9 4 0 1 0 -7 23 -24 0 0 12
There are 12 evens, which includes 6 zeros
The number of odd numbers is: 8
```

![](bbox=[0.215, 0.526, 0.276, 0.575])

> In the previous program, because the data is assumed to be input from the standard input device (the keyboard) and the function getNumber returns only one value, you can also write the function getNumber as a value-returning function. If written as a value-returning function, the definition of the function getNumber is:

```
```cpp
int getNumber()
{
    int num;

    cin >> num;

    return num;
}
```
```

In this case, the statement (function call):

```
```cpp
getNumber(number);
```
```

in the function main should be replaced by the statement:

```
```cpp
number = getNumber();
```
```

Of course, you also need to change the function prototype.