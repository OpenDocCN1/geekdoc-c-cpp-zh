```
```cpp
cout << "Enter Values of a and b \n";
cin >> a;
cin >> b;
int x = a-b;
try
{
    if(x != 0)
    {
        cout << "Result(a/x) = " << a/x <<
        "\n";
    }
    else // There is an exception
    {
        throw(x); // Throws int object
    }
}
catch(int i) // Catches the exception
{
    cout<<"Exception caught: DIVIDE BY
    ZERO\n";
}
cout << "END";

return 0;
}
```
```

The output of Program 13.1 would be:

# First Run

```
Enter Values of a and b
20 15
Result(a/x) = 4
END
```

# Second Run

```
Enter Values of a and b
10 10
```