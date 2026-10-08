# Appendix C

```
5. a. majorsum = 0;
for(k = 0; k < 5; k++)
majorsum += x[k][k];
```

```
b. minorsum = 0;
for(k = 0; k < 5; k++)
minorsum += x[k][4 - k];
```

```
c. uppersum = 0;
for(i = 0; i < 5; i++)
for(j = i + 1; j < 5; j++)
uppersum += x[i][j];
```

```
d. lowersum = 0;
for(i = 0; i < 5; i++)
for(j = 0; j < i; j++)
lowersum += x[i][j];
```

Section 8.5.3

+   1. a. true
b. false
c. true
d. true
e. true

```
2. a. func(int a, n, m);
.. .
void func(int a[][JMAX], n, m) /* this should run correctly */
{
  int i, j;
  for(i = 0; i < n; i++)
    for(j = 0; j < m; j++)
      printf("%d", a[i][j]);
  return;
}
```

```
b. arr[0][0] = 3;
func(arr);
printf("%d", arr[0][0]); /* this should print original value */
/* if it is passed by value */
```