
```
move(temp, 0, lst - fst, data, fst);
}

void mergesort(int left, int right) {
    int m;
    m = (left + right) / 2;
    if (left < right)
        mergesort(left, m);
    mergesort(m + 1, right);
    merge(left, m, right);
}

int main() {
    int data[5] = 999;
    data[1] = 1;
    data[2] = 23;
    data[3] = 55;
    data[4] = 44;
    mergesort(0, 4);
    for (int i = 0; i < 5; i++)
        printf("%d\n", data[i]);
    printf("\n");
    return 0;
}
```
