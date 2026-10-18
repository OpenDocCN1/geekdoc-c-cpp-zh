```
```cpp
}
else                 // There is a problem
{
    throw(x-y);   // Throw point
}
}
int main()
{
    try
    {
        cout << “We are inside the try block\n”;
        divide(10,20,30);          // Invoke
        divide()
        divide(10,10,20);          // Invoke
        divide()
    }
    catch(int  i)                  // Catches the
    exception
    {
        cout << “Caught the exception \n”;
    }
    return 0;
}
```
```

The output of the Program 13.2 would be:

```
```
We are inside the try block

We are inside the function
Result = -3

We are inside the function
Caught the exception
```
```