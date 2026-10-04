# Appendix O: Solutions to Odd Numbered Review Questions

+   15. value

+   17. local

+   19. global

+   21. local

+   23. return

+   25. last

+   27. reference

+   29. reference

+   31. parameter lists

```
33. double half(double num)
{
    return num / 2;
}
```

```
35. void timesTen(int num)
{
    cout << (num * 10) << endl;
}
37. void getNumber(int &num)
{
    cout << "Enter a number in the range 1 - 100 : ";
    cin >> num;
    while (num < 1 || num > 100)
    {
        cout << "That number is out of range.\n";
        cout << "Enter a number in the range 1 - 100 : ";
        cin >> num;
    }
}
```

+   39. False

+   41. True

+   43. True

+   45. False

+   47. True

+   49. True

+   51. True

+   53. False

+   55. True

57. The assignment statement should read:

```
average = (value1 + value2 + value3) / 3.0;
```

The function is defined as a double but returns no value.