For instance, if n = 10 and the missing number is 6 = 0110₂, A may look like:

![](bbox=[0.271, 0.113, 0.754, 0.227])

Printing this array in spiral form would give

1 2 3 4 8 12 16 15 14 13 9 5 6 7 11 10

The only constant time access to it is of the form A[j][i], which can be labeled as fetch the jᵗʰ bit of A[i], assuming the first bit is the most significant, etc.

# C++ Implementation

Consider the following program:

```
int m = floor(logb(n)) + 1;
int A[m][n];

int main()
{
    int i, j, t, numrow, n0, n1, ntemp = n;
    int B[n], res[m];

    for(i = 0; i < m; i++)
    {
        B[i] = i;
    }

    for(i = m - 1; i >= 0; i--)
    {
        n0 = n1 = 0;

        for(j = 0; j < ntemp; j++)
        {
            if (A[i][B[j]] == 0) n0++;
            else n1++;
        }

        if(n0 - n1 == 2 || n0 - n1 == 1) res[i] = 1;
        if(n0 - n1 == 0 || n0 - n1 == -1) res[i] = 0;

        for(j = 0, t = 0; j < ntemp; j++)
        {
            if((res[i] == A[i][B[j]]))
```