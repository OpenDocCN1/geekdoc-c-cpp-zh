```
ptr = arr;
tmp = &ptr;
for(i = 0; i < 3; i++)
{
    test(tmp, i);
    printf("%d ", arr[i]);
}
return 0;
}
```

```
void test(int **tmp, int i)
{
    *(*(tmp + i)) += 50;
}
```

Answer: tmp is declared as a pointer to a pointer to an integer. The statement tmp = &ptr; makes tmp point to the address of ptr; which points to the address of the first element of the array arr. Since *tmp is equal to ptr, we have *(tmp+i) = *(ptr+i) = *(arr+i) = arr[i]. Therefore, each call to test() increases the respective element of the array arr by 50, and the program displays: 60 70 80.

# C.20.3 Write a program that reads the order of preference that 100 tourists answered in the question: “What did you enjoy the most in Greece?”

+   1. The natural diversity
+   2. The climate
+   3. The islands
+   4. The night life
+   5. The monuments
+   6. The people
+   7. The food

Each answer takes 1–7 points according to its rank order. The first answer takes 7 points, the second one takes 6 points, and the last one takes 1 point. For example, if two tourists answered the following:

| First Tourist | Second Tourist |
|---|---|
| 5 (7p.) | 3 (7p.) |
| 4 (6p.) | 7 (6p.) |
| 6 (5p.) | 2 (5p.) |
| 3 (4p.) | 1 (4p.) |
| 2 (3p.) | 5 (3p.) |
| 1 (2p.) | 4 (2p.) |
| 7 (1p.) | 6 (1p.) |

the program should display:

First answer gets 6 points
Second answer gets 8 points