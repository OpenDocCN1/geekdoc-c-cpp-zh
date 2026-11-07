received, and the percentage of the total votes received by the candidate. Your program should also output the winner of the election. A sample output is:

```
Candidate                 Votes Received        % of Total Votes
Johnson                         5000                    25.91
Miller                          4000                    20.73
Duffy                           6000                    31.09
Robinson                        2500                    12.95
Ashtony                         1800                     9.33
Total                          19300

The Winner of the Election is Duffy.
```

+   8. Consider the following function main:

```
int main()
{
    int inStock[10][4];
    int alpha[20];
    int beta[20];
    int gamma[4] = {11, 13, 15, 17};
    int delta[10] = {3, 5, 2, 6, 10, 9, 7, 11, 1, 8};

    .
    .
    .
}
```

+   a. Write the definition of the function setZero that initializes any one-dimensional array of type `int` to 0.

+   b. Write the definition of the function inputArray that prompts the user to input 20 numbers and stores the numbers into alpha.

+   c. Write the definition of the function doubleArray that initializes the elements of beta to two times the corresponding elements in alpha. Make sure that you prevent the function from modifying the elements of alpha.

+   d. Write the definition of the function copyGamma that sets the elements of the first row of inStock to gamma and the remaining rows of inStock to three times the previous row of inStock. Make sure that you prevent the function from modifying the elements of gamma.

+   e. Write the definition of the function copyAlphaBeta that stores alpha into the first five rows of inStock and beta into the last five rows of inStock. Make sure that you prevent the function from modifying the elements of alpha and beta.

+   f. Write the definition of the function printArray that prints any one-dimensional array of type `int`. Print 15 elements per line.