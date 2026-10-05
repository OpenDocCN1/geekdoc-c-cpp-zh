# 592 CHAPTER 13 Recursion

Display 13.5 Mutual Recursion to Determine a String Has an Even Number of 1s

```
// uses istream and string
// If the recursive calls ends in this function with an empty string
// then we had an even number of 1s.
bool evenNumberOfOnes(string s)
{
    if (s.length() == 0)
        return true; // Is even
    else if (s[0]=='1')
        return oddNumberOfOnes(s.substr(1));
    else
        return evenNumberOfOnes(s.substr(1));
}
```

```
// If the recursive calls ends in this function with an even string
// then we had an odd number of 1s.
bool oddNumberOfOnes(string s)
{
    if (s.length() == 0)
        return false; // Not even
    else if (s[0]=='1')
        return evenNumberOfOnes(s.substr(1));
    else
        return oddNumberOfOnes(s.substr(1));
}
```

```
int main ()
{
    string s = "10011";
    if (evenNumberOfOnes(s))
        cout << "Even number of ones." << endl;
    else
        cout << "Odd number of ones." << endl;
    return 0;
}
```

Sample Dialogue

Odd number of ones.