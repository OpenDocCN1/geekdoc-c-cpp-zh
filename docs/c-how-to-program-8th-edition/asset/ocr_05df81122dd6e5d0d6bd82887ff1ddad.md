# F.12 Given the union

```
```c
union A
{
    double y;
    char *zPtr;
};
```
```

which of the following are correct statements for initializing the union?

+   a) `A p = b;`  // b is of type A  
+   b) `A q = x;`  // x is a double  
+   c) `A r = 3.14159;`  
+   d) `A s = { 75.63 };`  
+   e) `A t = { "Hi There!" };`  
+   f) `A u = { 3.14159, "Hi" };`  
+   g) `A v = { y = -7.843, zPtr = &x };`