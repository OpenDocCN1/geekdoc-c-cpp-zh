# 10. Consider the following C program:

```
void fun(void) {
    int a, b, c; /* definition 1 */
    ...
    while (...) {
        int b, c, d; /*definition 2 */
        ... <-- ---------- 1
        while (...) {
        int c, d, e; /* definition 3 */
        ... <-- ---------- 2
        }
        ... <-- ---------- 3
    }
    ... <-- ---------- 4
}
```

For each of the four marked points in this function, list each visible variable, along with the number of the definition statement that defines it.

# 11. Consider the following skeletal C program:

```
void fun1(void);  /* prototype */
void fun2(void);  /* prototype */
void fun3(void);  /* prototype */
void main() {
    int a, b, c;
    ...
}
void fun1(void) {
    int b, c, d;
    ...
}
void fun2(void) {
    int c, d, e;
    ...
}
void fun3(void) {
    int d, e, f;
    ...
}
```