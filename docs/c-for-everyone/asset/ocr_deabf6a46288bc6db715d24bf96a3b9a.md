```
```cpp
cout << " ";
}
cout << endl;
}
void box_string(string str)
{
    int n = str.length();
    print_line(n + 2);
    cout << "!" << endl;
    print_line(n + 2);
}
```
```

**18.** `int total_pennies = round_to_pennies(total);`
`int total_tax_pennies = round_to_pennies(total * tax_rate);`

where the function is defined as

```
```cpp
/**
 @param amount an amount in dollars and cents
 @return the amount in pennies, rounded to the nearest penny
*/
int round_to_pennies(double amount)
{
    return static_cast<int>(100 * amount + 0.5);
}
```
```

**19.** `if (is_even(page)) . . .`

where the function is defined as follows:

```
```cpp
bool is_even(int n)
{
    return n % 2 == 0;
}
```
```

**20.** Add parameter variables so you can pass the initial balance and interest rate to the function:

```
```cpp
double balance(double initial_balance, double rate, int years)
{
    return initial_balance * pow(1 + rate / 100, years);
}
```
```

**21.** `int spaces = count_spaces(input);`

where the function is defined as follows:

```
```cpp
/**
 @param str any string
 @return the number spaces in str
*/
int count_spaces(string str)
{
    int count = 0;
    for (int i = 0; i < str.length(); i++)
    {
        if (str.substr(i, 1) == " ")
        {
            count++;
        }
    }
    return count;
}
```
```