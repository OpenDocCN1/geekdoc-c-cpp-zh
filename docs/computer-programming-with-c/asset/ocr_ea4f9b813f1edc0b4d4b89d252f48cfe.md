```
```cpp
/*Accept each element of matrix as input from the user*/
}
}
```
```

Let us assume that the user enters the number of rows as 3 and number of columns also as 3. Also, let us also assume that the user enters the values for each of the matrix elements a and b as shown in Figure 6.32.

![](bbox=[0.296, 0.243, 0.657, 0.379])

After the values of matrices a and b are taken as input from the user, we can now start performing addition to obtain the resultant matrix Res. The element at i<sup>th</sup> row and j<sup>th</sup> column of matrix Res will be evaluated as the addition of element at i<sup>th</sup> row and j<sup>th</sup> column in matrix a with the element at i<sup>th</sup> row and j<sup>th</sup> column in matrix b. For example, the element Res[0][0] is to be evaluated as shown below:

```
```cpp
Res[0][0]=a[0][0]+b[0][0];
```
```

Similarly, for each value of row number i and column number j we evaluate Res[i][j] inside a for loop as follows:

```
```cpp
Res[i][j]=a[i][j]+b[i][j];
```
```

The last set of for loops print each element stored in the resultant matrix Res which is shown in Figure 6.33:

![](bbox=[0.356, 0.667, 0.561, 0.802])

Given below is the source code to perform addition of matrices:

```
```cpp
#include<stdio.h>
void main()
{
```
```