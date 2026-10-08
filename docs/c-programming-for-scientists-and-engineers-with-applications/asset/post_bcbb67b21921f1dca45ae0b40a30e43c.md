
## Section 7.3.3

- 1. a. true
  b. true
  c. true
  d. true

- 2. a. 0 23
   1 43
   2 65
   3 67
   4 87
  b. 4 87
   3 67
   2 65
   1 43
   0 23

- 3. a. 0 23 86
   1 43 67
   2 65 43
   3 67 65
   4 87 59

| b. 173 154 130 152 146 |
| 153 134 110 132 126 |
| 151 132 108 130 102 |
| 129 110 86 108 102 |
| 109 90 66 88 82 |

```c
4. printf("element");
for(i = 0; i < 5; i++)
  printf("%d", i);
  printf("\na");
  for(i = 0; i < 5; i++)
    printf("%d,%d", a[i]);
  printf("\nb");
  for(i = 0; i < 5; i++)
    printf("%3f", b[i]);
```

- 5. printf("element array b\n");
  for(i = 0; i < 5; i++)
    printf("%d %3f\n", a[i], b[i]);

## Section 7.4.3

- 1. a. false
  b. false
  c. true
  d. true

- 2. a. a
| a | b |
|---|---|
| 0 | 45 |
| 10 | 55 |
| 21 | 66 |
| 42 | 87 |

- b. a
| a | b |
|---|---|
| 7 | 35 |
| 8 | 40 |
| 12 | 60 |
| 14 | 70 |

- 3. a
| a | b |
|---|---|
| 0 | 18 |
| 6 | 36 |
| 7 | 42 |
| 8 | 33 |
| 34 | 48 |

- 3. a is 1 2 1 16
b. b is 6.25 3.0.75
c. a is 18 15 8 26
d. a is -6 2 1 23

## Section 7.5.3

- 1. a. false
  b. false
  c. true
  d. true
  e. false
  f. true

```c
2. void mult(int a[], int b[], int c[], int n)
{
    int k;
    for(k = 0; k < n; k++)
    c[k] = a[k] * b[k];
}
```

```c
3. float funcsum(float x[], int n)
{
    int k;
    float sum = 0;
    for(k = 0; k < n; k++)
    sum += x[k];
    return sum;
}
```

```c
4. int main ()
{
    const int ARRAYSIZE = 5;
    int x[ARRAYSIZE], y[ARRAYSIZE];
    for(k = 0; k < ARRAYSIZE; k++)
        if(unequal(x[k], y[k]))
            printf("%d and %d are equal\n", x[k], y[k]);
    return 0;
}
```

## Chapter 8

### Section 8.1.4

- 1. a. false
  b. true
  c. false
  d. true

- 2. a. float x[10][20];
  b. int x[20][40];
  c. double w[50][200];
  d. double w[100][200], q[100][200];

- 3. c[0][0]
  c[0][1]
  c[0][2]
  c[1][0]
  c[1][1]
  c[1][2]

```c
4. for(i = 0; i < 10; i++)
   for(j = 0; j < 20; j++)
   {
       ...
       x[i][j]
       ...
   }
```

```c
5. for(j = 0; j < 400; j++)
   for(i = 0; i < 300; i++)
   {
       ...
       q[i][j]
       ...
   }
```

- 6. a.
| a | b |
|---|---|
| 0 | 1 |
| 1 | 1 |
| 2 | 1 |
| 0 | 0 |
| 1 | 0 |
| 2 | 0 |

- b.
| a | b |
|---|---|
| 0 | 1 |
| 1 | 0 |
| 2 | 0 |
| 0 | 1 |
| 1 | 0 |
| 2 | 0 |

## Section 8.2.3

- 1. #define ROWS 3
  #define COLS 4
```c
   int arr[ROWS][COLS], i, j;
   for(j = 0; j < COLS; j++)
     for(i = 0; i < ROWS; i++)
       scanf("%d", &arr[i][j]);
```

| a[0][0] | 5 |
|---|---|
| a[0][1] | 16 |
| a[0][2] | 14 |
| a[0][3] | 35 |
| a[1][0] | 8 |
| a[1][1] | 19 |
| a[1][2] | 18 |
| a[1][3] | 10 |
| a[2][0] | 12 |
| a[2][1] | 16 |
| a[2][2] | 20 |

## Section 8.3.3

```c
for(i = 0; i < 3; i++)
  for(j = 0; j < 4; j++)
    printf("%1f ", arr[i][j]);
```
```c
printf(" ");
for(j = 0; j < 6; j++)
  printf("%d", j + 1);
```
```c
printf("\n");
for(i = 0; i < 4; i++) {
    printf("%d", i);
    for(j = 0; j < 6; j++) {
        printf("%5f", arr[i][j]);
    }
}
```

```c
#define IMAX 40
#define JMAX 60
```c
fprintf("%d %d\n", IMAX, JMAX);
for(i = 0; i < IMAX; i++) {
    for(j = 0; j < JMAX; j++) {
        fprintf("%d", arr[i][j]);
    }
}
```

## Section 8.4.4

- 1. a. false
  b. true
  c. false
  d. false

- 2. int a[2][3] = {1, 2, 3, 4, 5, 6}, b[2][3] = {10, 20, 30, 40, 50, 60};
  a = b; /* this statement should cause an error */
  for(i = 0; i < 2; i++) {
    printf("%d %d\n", a[i][0], a[i][1], a[i][2]);
  }

- 3. int a[2][3] = {1, 2, 3, 4, 5, 6}, b[2][3] = {10, 20, 30, 40, 50, 60};
  for(j = 0; j < 3; j++) { /* this should run correctly */
    a[0][j] = b[0][j]; // corrected index logic
  }
  for(i = 0; i < 2; i++) {
    printf("%d %d\n", a[i][0], a[i][1], a[i][2]);
  }

- 4. int a[2][3] = {1, 2, 3, 4, 5, 6}, b[2][3] = {10, 20, 30, 40, 50, 60};
  int sum, i, j, k;
  for(i = 0; i < 3; i++) {
    for(j = 0; j < 3; j++) {
      sum = 0;
      for(k = 0; k < 3; k++)
        sum += a[i][k] * b[k][j]; /* index will go out of bounds */
      c[i][j] = sum;
    }
  }
  for(i = 0; i < 3; i++) {
    for(j = 0; j < 3; j++)
      printf("%d %d %d\n", a[i][0], a[i][1], a[i][2]);
    printf("\n");
  }

- 3. a. array x
  2.5 4.2 5.2 6.4
  4.2 2.6 1.2 7.8
  5.8 2.4 6.7 9.1
  1.3 2.1 3.2 4.8

- b. array x
  2.5 4.2 5.2 7.3
  4.2 2.6 1.2 6.9
  3.5 8.5 5.9 10.1
  1.3 2.1 3.2 16.9

- c. array x
  2.5 4.2 5.2 9.4
  4.2 2.6 1.2 11.5
  3.5 8.5 5.9 14.5
  1.3 2.1 3.2 16.0

- d. array x
  for(i = 0; i < 4; i++) {
    temp = 0;
    for(j = 0; j < 5; j++)
      temp += x[i][j];
    rowsum[i] = temp;
  }
  for(j = 0; j < 5; j++) {
    temp = 0;
    for(i = 0; i < 4; i++)
      temp += x[i][j];
    colsum[j] = temp;
  }

## Appendix C

- 5. a. majorsum = 0;
  for(k = 0; k < 5; k++)
  majorsum += x[k][k];

- b. minorsum = 0;
  for(k = 0; k < 5; k++)
  minorsum += x[k][k];

- c. uppersum = 0;
  for(i = 0; i < 5; i++)
  for(j = i + 1; j < 5; j++)
  uppersum += x[i][j];

- d. lowersum = 0;
  for(i = 0; i < 5; i++)
  for(j = 0; j < i; j++)
  lowersum += x[i][j];

## Section 8.5.3

- 1. a. true
  b. false
  c. true
  d. true
  e. true

- 2. a. func(int a, n, m);
  void func(int a[][JMAX], int m) /* this should run correctly */
  {
    int i, j;
    for(i = 0; i < n; i++)
    for(j = 0; j < m; j++)
      printf("%d", a[i][j]);
  return;
  }

- b. arr[0][0] = 3;
  func(arr);
  printf("%d", arr[0][0]); /* this should print original value */
  /* it is passed by value */

```c
void func(int arr[][JMAX])
{
    arr[0][0] = 25;
    return;
}
```

- c. func(int [][JMAX]); /* this should cause an error */

- d. void func(int arr[][JMAX], int n, int m) /* this should run correctly */
{
    int rowsum = 0, colsum = 0, i , j;
    for(j = 0; j < m; j++)
        rowsum += arr[0][j];
    for(i = 0; i < n; i++)
        colsum += arr[i][0];
    return;
}

- e. printf("%d", arr[2][3]);
  func(arr[2][3], &arr[2][3]);
  printf("%d", arr[2][3]);

  void func(int a, *b) /* * this should cause an error */
  {
    printf("%d %d \n", a, *b);
    a = 10;
    *b = 20;
    printf("%d %d \n", a, *b);
    return;
  }

- 3. void funcmax(float pressure[][JMAX], int n, int m)
{
    float rowmax[IMAX] = 0.0, max;
    for(i = 0; i < m; i++)
    {
        max = 0.0;
        for(j = 0;j < n; j++)
            if(max < pressure[i][j])
                max = pressure[i][j];
        rowmax[i] = max;
    }

```c
}
for(i = 0; i < n; i++)
{
  for(j = 0; j < m; j++)
    printf("%f ", pressure[i][j]);
  printf("%f\n", rowmax[i]);
}
```

- 4. define IMAX 10
  #define JMAX 5

- a. int main() {
  float temperature[IMAX][JMAX];
  float rowavg[IMAX], colavg[JMAX];
  funcin(temperature);
  funcavg(temperature, rowavg, colavg);
  functout(temperature, rowavg, colavg);
  return 0;
}

```c
   void funcin(float temp[][JMAX]) {
  int i, j;
  for(i = 0; i < IMAX, i++)
    for(j = 0; j < JMAX; j++)
      scanf("%f", &temp[i][j]);
  return;
  }
```

```c
   b. void funcavg(float temp[][JMAX], float rowavg[], float colavg[]) {
  int i, j;
  for(i = 0; i < IMAX; i++)
  {
    rowavg[i] = 0.0;
    for(j = 0; j < JMAX; j++)
      rowavg[i] += temp[i][j];
  }
  rowavg[i] = rowavg[i]/JMAX;
  for(j = 0; j < JMAX; j++)

```
{
colavg[j] = 0.0;
for(i = 0; i < IMAX; i++)
colavg[j] += temp[i][j];
}
colavg[j] = colavg[j]/IMAX;
```
```
