14. Write the program for computing the maximum of numbers as suggested initially in Section 3.4.1, i.e. the one in which maximum was to be initialized to the value (-numeric_limits<float>::max()). Does this program behave identically (i.e. give the same result for the same inputs) to the program given at the end of the Section 3.4.1? If you think the programs behave differently, state the inputs for which the programs will behave differently.

15. What does the following program compute?

```
```cpp
double x;
int n;
cin >> x >> n;
repeat(n){
    x = x * x;
}
```
```

16. Draw a smooth spiral. The spiral should wind around itself in a parallel manner, i.e. there should be a certain point called “center” such that if you draw a line going out from it, the spiral should intersect it at equal distances as it winds around.