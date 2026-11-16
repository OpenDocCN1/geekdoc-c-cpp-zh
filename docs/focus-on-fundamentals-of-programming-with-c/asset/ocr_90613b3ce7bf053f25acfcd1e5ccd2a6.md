```
void mergeTwoArrays(int a[], int b[], int c[], int maxA, int maxB) {
    int i, j, k;
    i = j = k = 0;
    while (i < maxA && j < maxB) {
        if (a[i] <= b[j]) {
            c[k++] = a[i++];
        }
        else {
            c[k++] = b[j++];
        }
    }
    while (i < maxA) {
        c[k++] = a[i++];
    }
    while (j < maxB) {
        c[k++] = b[j++];
    }
}
```

Here's the output produced after the merge:

| 1 | 2 | 4 | 5 | 6 | 8 | 9 | 11 | 17 | 20 |
|---|---|---|---|---|---|---|---|---|---|