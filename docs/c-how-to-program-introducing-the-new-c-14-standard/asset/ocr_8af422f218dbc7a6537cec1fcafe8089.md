+   5. **6.5** Give the function prototype (without parameter names) for each of the following:
+      A. The function described in **Exercise 6.4(a)**.
+      B. The function described in **Exercise 6.4(b)**.
+      C. The function described in **Exercise 6.4(c)**.
+      D. The function described in **Exercise 6.4(d)**.

6. **6.6** Write a declaration for double-precision, floating-point variable `lastVal` that should retain its value between calls to the function in which it’s defined.

7. **6.7** Find the error(s) in each of the following program segments, and explain how the error(s) can be corrected (see also **Exercise 6.46**):

A.

```
```cpp
{
    void g() {
        cout << "Inside function g" << endl;
        void h() {
            cout << "Inside function h" << endl;
        }
    }
}
```
```

B.

```
```cpp
{
    int sum(int x, int y) {
        int result(0);
```
```