We can also initialize an array of characters at the time it's declared:

```
char letters[5] = { 'a', 'b', 'c', 'd', 'e' };

```

| 'a' | 'b' | 'c' | 'd' | 'e' |
|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] |

Note that it's not necessary to completely initialize an entire array. If less initial values are specified, then only as many elements will be initialized. The remaining elements in the array will be set to zero.

```
double sample[5] = { 10.5, 12.6, 31.2 };

```

| 10.5 | 12.6 | 31.2 | 0.0 | 0.0 |
|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] |

We can also define an array without specifying the number of elements in the array. The size of the array is automatically determined by the number of initialization elements:

```
int num[] = { 2, 3, 4, 7, 9 };

```

| 2 | 3 | 4 | 7 | 9 |
|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] |