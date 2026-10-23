from i and changing these k digits one by one in some order, until i coincides with j. In this process, i is successively incremented or decremented by powers of 2 until j is reached.

How many such paths exist? Well, it depends on the number of different possible ways to order these k digits. Let’s count: there are k possibilities for choosing the first digit to be changed. For each choice, there are k − 1 possibilities for choosing the second digit to be changed, and so on. By continuing this process, one gets a total of k! possible orderings for these k digits. Since each ordering defines a different path, the total number of paths leading from i to j is also k!.

In the well-ordered path leading from i to j, the above k digits are changed one by one in a natural order from the least significant digit to the most significant digit. The following function prints this path to the screen. If i > j, then it is called recursively, with i and j interchanged:

```
void path(int i, int j){
    if(i <= j){
        int go = i;
        int power = 1;
        int increment = 0;
        printf("%d\n",i);
        while(j){
            if(increment = (j%2 - i%2) * power)
                printf("%d\n", go += increment);
            i /= 2;
            j /= 2;
            power *= 2;
        }
    }
    else
        path(j,i);
} /* well-ordered path from i to j */
```

# 1.19 Example: Pascal’s Triangle

A good example of an application that uses a two-dimensional array and a nested loop is Pascal’s triangle. This triangle can be embedded in the lower-left part of a square mesh (see Figure 1.4). In every cell of the mesh, there is room for a single integer number. In what follows, we describe the rules to fill the cells in Pascal’s triangle.

Let i = 0,1,2,… be the row index (numbered bottom to top) and j = 0,1,2,… be the column index (numbered left to right) in the mesh. Assume that a particle initially lies in the origin cell (0,0). Now, it starts to move. In every move, the particle can advance one cell either to the right or upward.

Consider a cell (k,l) for some fixed nonnegative integers k and l. Along how many different paths can the particle reach (k,l)?

This problem is solved recursively. The particle can approach (k,l) either from (k,l − 1) on the left or (k − 1,l) just below it. Hence, the particle must reach one of these cells before it can reach (k,l). Hence, the number of different paths leading to (k,l) is the number of different paths leading to (k,l − 1) plus the number of different paths leading to (k − 1,l).