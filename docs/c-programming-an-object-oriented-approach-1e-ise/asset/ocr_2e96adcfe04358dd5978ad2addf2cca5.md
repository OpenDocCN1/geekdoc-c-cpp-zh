# Program 13.11  File fraction.cpp (Continued)

```
```cpp
// Greater-than or equal operator (friend)
bool operator>= (const Fraction& left, const Fraction& right)
{
    return (left.numer * right.denom >= right.numer * left.denom);
}
// Extraction operator (friend)
istream& operator >> (istream& left, Fraction& right)
{
    cout << "Enter the value of numerator: ";
    left >> right.numer;
    cout << "Enter the value of denominator: ";
    left >> right.denom;
    right.normalize();
    return left;
}
// Insertion operator (friend)
ostream& operator << (ostream& left, const Fraction& right)
{
    left << right.numer << "/" << right.denom;
    return left;
}
// Helper function (greatest common divisor)
int Fraction::gcd (int n, int m)
{
    int gcd = 1;
    for (int k = 1; k <= n && k <= m; k++)
    {
        if (n % k == 0 && m % k == 0)
        {
            gcd = k;
        }
    }
    return gcd;
}
// Helper function (normalizing a fraction)
void Fraction::normalize ()
{
    if (denom == 0)
    {
        cout << "Invalid denominator in fraction. Need to quit." << endl;
        assert (false);
    }
    if (denom < 0)
    {
```
```