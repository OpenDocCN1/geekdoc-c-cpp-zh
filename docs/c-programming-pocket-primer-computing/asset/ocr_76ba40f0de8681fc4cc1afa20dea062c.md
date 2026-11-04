```
```c
int main()
{
    char str1[] = "123.456";
    checkDigits(str1);
    char str2[] = "-51.203";
    checkDigits(str2);

    return (0);
}
```
```

Listing 4.9 defines the function `checkDigits()` that takes a character string and has a return type of `void`. This function iterates through the character string and uses conditional logic, with the built-in C function `isdigit()`, to determine whether each character is a digit, and print a suitable message.

The `main()` function defines two character strings `str1` and `str2` and invokes the `checkDigits()` function with each of these strings. The output from Listing 4.9 is here:

```
```
Number: 123.456
Digit: 1
Digit: 2
Digit: 3
Not Digit: .
Digit: 4
Digit: 5
Digit: 6

Number: -51.203
Not Digit: -
Digit: 5
Digit: 1
Not Digit: .
Digit: 2
Digit: 0
Digit: 3
```
```