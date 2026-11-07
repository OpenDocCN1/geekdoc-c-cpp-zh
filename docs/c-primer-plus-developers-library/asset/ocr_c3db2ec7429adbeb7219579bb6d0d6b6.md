```
```cpp
while (cin.get() != '\n')
    continue;
}

// SingingWaiter methods
void SingingWaiter::Data() const
{
    Singer::Data();
    Waiter::Data();
}

void SingingWaiter::Get()
{
    Waiter::Get();
    Singer::Get();
}

void SingingWaiter::Set()
{
    cout << "Enter singing waiter's name: ";
    Worker::Get();
    Get();
}

void SingingWaiter::Show() const
{
    cout << "Category: singing waiter\n";
    Worker::Data();
    Data();
}
```
```

Of course, curiosity demands that you test these classes, and Listing 14.12 provides code to do so. Note that the program makes use of polymorphism by assigning the addresses of various kinds of classes to base-class pointers. Also the program uses the C-style string library function `strchr()` in the following test:

```
```cpp
while (strchr("wstq", choice) == NULL)
```
```

This function returns the address of the first occurrence of the choice character value in the string "wstq"; the function returns the NULL pointer if the character isn’t found. This test is simpler to write than an if statement that compares choice to each letter individually.

Be sure to compile Listing 14.12 along with workermi.cpp.