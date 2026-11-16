# Figure 11.11 Correct array copy

```
int a[] = { 2, 4, 6, 8 }, b;

b = new int[4];

for ( int i = 0; i < 4; i++ )
    b[i] = a[i];
```