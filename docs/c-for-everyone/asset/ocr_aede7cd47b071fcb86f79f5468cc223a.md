**R4.11** Rewrite the following for loop into a while loop.

```
int s = 0;
for (int i = 1; i <= 10; i++)
{
    s = s + i;
}
```

**R4.12** Rewrite the following do/while loop into a while loop.

```
int n;
cin >> n;
double x = 0;
double s;
do
{
    s = 1.0 / (1 + n * n);
    n++;
    x = x + s;
}
while (s > 0.01);
```

**R4.13** Provide trace tables of the following loops.

+   a.

```
int s = 1;
int n = 1;
while (s < 10) { s = s + n; }
n++;
```

+   b.

```
int s = 1;
for (int n = 1; n < 5; n++) { s = s + n; }
```

+   c.

```
int s = 1;
int n = 1;
do
{
    s = s + n;
    n++;
}
while (s < 10 * n);
```

**R4.14** What do the following loops print? Work out the answer by tracing the code, not by using the computer.

+   a.

```
int s = 1;
for (int n = 1; n <= 5; n++)
{
    s = s + n;
    cout << s << " ";
}
```

+   b.

```
int s = 1;
for (int n = 1; s <= 10; cout << s << " ")
{
    n = n + 2;
    s = s + n;
}
```

+   c.

```
int s = 1;
int n;
for (n = 1; n <= 5; n++)
{
    s = s + n;
    n++;
```