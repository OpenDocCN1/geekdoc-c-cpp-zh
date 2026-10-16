```
9. i = 0;
    j = 10;
    for (;;)
    {
        k = 2 * i + j;
        if (k > 20) break;
        cout << i << j << k << endl;
        if (i + j < 10) break;
        i++;
        j--;
    }
    cout << i << j << k << endl;
```

```
10. i = 5;
    for (;;)
    {
        cout << i;
        i -= 2;
        if (i < 1) break;
        j = 0;
        for (;;)
        {
            j++;
            cout << j;
            if (j >= i) break;
        }
        cout << "###\n"
    }
    cout << "***\n";
```

```
11. k = 5;
    i = 32;
    while (i > 0)
    {
        cout << "base-2 log of " << i << " = " << k << endl;
        i /= 2;
        k--;
    }
```

```
12. i = 1;
    while (i*i < 10)
    {
        j = i;
```