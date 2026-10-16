```
p[i] = new int[d2]; // creates space for each row
}

int main()
{
    int m, n;

    cout << "Enter size of matrix: ";
    cin  >> m >> n;
    matrix A(m,n); // matrix object A constructed

    cout << "Enter matrix elements row by row \n";
    int i, j, value;

    for(i = 0; i < m; i++)
        for(j = 0; j < n; j++)
        {
            cin >> value;
            A.get_element(i,j,value);
        }
    cout << "\n";
    cout << A.put_element(1,2);

    return 0;
};
```

The output of a sample run of Program 6.6 is as follows.

```
Enter size of matrix: 3 4
Enter matrix elements row by row
11 12 13 14
15 16 17 18
19 20 21 22

17
```

17 is the value of the element (1,2).

![](bbox=[0.35, 0.64, 0.9, 0.82])

The constructor first creates a vector pointer to an int of size d1. Then, it allocates, iteratively an int type vector of size d2 pointed at by each element p[i].

Thus, space for the elements of a d1 × d2 matrix is allocated from free store as shown above.