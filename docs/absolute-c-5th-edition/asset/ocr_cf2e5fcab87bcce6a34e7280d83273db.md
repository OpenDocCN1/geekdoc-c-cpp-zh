# 314 CHAPTER 7 Constructors and Other Tools

3. The definition is easier to give if you also add a private helping function named BankAccount::digitToInt, as shown, to the class BankAccount.

```
//Uses iostream
void BankAccount::input( )
{
    int dollars,
    char point, digit1, digit2;
    cout << "Enter account balance (include cents even if .00)\$";
    cin >> dollars;
    cin >> digit1 >> digit2;
    accountDollars = dollars;
    accountCenters = digitToInt(digit1)*10 + digitToInt(digit2);
    if (accountCenters < 0)
        accountCenters = -accountCenters;
    cout << "Enter interest rate (NO percent sign); }";
    cin >> rate;
    setRate(rate);
}
```

```
int BankAccount::digitToInt(char digit)
{
    return (static_cast<int>(digit) - static_cast<int>('0'));
}
```

+   4. The member function input changes the value of its calling object, and so the compiler will issue an error message if you add the const. Each parameter method protects the caller's argument from change. If the type is a large structure or object, a value by makes a copy of the caller's argument and uses more memory than a call by constant reference.

+   5. In const int x = 17;, the const keyword promises the compiler that code written by the author will not change the value of x.
In the int const() declaration, the const keyword is a promise to the compiler that code written by the author to implement function will not change anything in the class.

+   In int g(const A& x); the const keyword is a promise to the compiler that code written by the class author will not change the argument plugged in x.

+   6. class DayOfYear
{
public:
    DayOfYear(int monthValue, int dayValue);
    DayOfYear(int monthValue);
    DayOfYear();
}