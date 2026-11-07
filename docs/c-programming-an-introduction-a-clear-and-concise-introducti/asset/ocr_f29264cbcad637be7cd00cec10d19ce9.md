way to do that is to use a for loop for the computation.

Now we can start writing the function definition by writing the function heading:

```
```cpp
int power(int base, int exp)
```
```

That’s the easy part. The body is more difficult but we’ve already made the decision to use a for loop to multiple the base by itself the number of times specified by the exp parameter. We have to start off with the value 1 since any number raised to the first power is that number. Here’s the code:

```
```cpp
int power(int base, int exp)
{
    int number = 1;
    for(int i = 1; i <= exp; ++i) {
        number *= base;
    }
    return base;
}
```
```

All we have to do now is use it in a program and test it with a few values to see if it works. First we’ll test it by calling power(2,3):

```
```cpp
int main(array<System::String ^> ^args)
{
    cout << power(2,3) << endl;
    Console::ReadKey();
    return 0;
}
```
```