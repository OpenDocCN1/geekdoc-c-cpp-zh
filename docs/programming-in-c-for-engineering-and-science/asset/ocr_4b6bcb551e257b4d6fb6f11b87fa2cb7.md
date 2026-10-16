We see that in this version of C++ (GNU C++), the capacity of intVector increased to 1 when the first value was added to it and then doubled each time more space was needed. (In some other versions, the capacity may increase by a factor other than 2.)

When the declaration of intVector was changed to

```
vector<int> intVector(3, 0);
```

execution of the statements produced

```
Capacity  Size
3         3
6         4
6         5
6         6
12        7
12        8
12        9
12        10
12        11
12        12
24        13
.         .
.         .
.         .
24        24
48        25
48        26
.         .
.         .
.         .
48        48
96        49
96        50
.         .
.         .
.         .
96        67
96        68
```