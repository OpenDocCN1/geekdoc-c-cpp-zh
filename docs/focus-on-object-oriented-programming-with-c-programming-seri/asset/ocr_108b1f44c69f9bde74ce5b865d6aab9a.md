```
```cpp
void test6() {
    cout << "5. Array declared with no integers: IntArray z;" << endl << endl;
    cis << "5. Array declared with no integers: IntArray z;" << endl << endl;
    IntArray z;
    for(int i = z.low(); i <= z.high(); i++)
        z[i] = i * 10;
    z.setName("z");
    cout << z << endl;
    cis << z << endl;
    wait();
}
```
```

```
```cpp
void test6() {
    cout << "6. Array declared with another object of type IntArray: IntArray c(6, 8);" << endl << endl;
    cout << endl;
    IntArray e(c);
    cout << "6. Array declared with another object of type IntArray: IntArray c(6, 8);" << endl << endl;
    cis << endl;
    cis << endl;
    IntArray c(6, 8);
    for(int i = c.low(); i <= c.high(); i++)
        c[i] = i * 10;
    c.setName("c");
    cout << c << endl;
    cis << c << endl;
    IntArray e(c);
    cout << e << endl;
    cis << e << endl;
    wait();
}
```
```

```
```cpp
void test7() {
    cout << "7. Array assigned to another array w/ different indices: IntArray f(1, 4);" << endl << endl;
    cout << endl;
    IntArray g(5, 8);
    f = g;
    cout << endl;
    cis << "7. Array assigned to another array w/ different indices: IntArray f(1, 4);" << endl << endl;
    cis << endl;
    IntArray g(5, 8);
    f = g;
    cis << endl;
    cis << endl;
    IntArray f(1, 4);
    for(int i = f.low(); i <= f.high(); i++)
        f[i] = i * 10;
    f.setName("f");
    cout << f << endl;
    cis << f << endl;
    IntArray g(5, 8);
    for(int i = g.low(); i <= g.high(); i++)
        g[i] = i * 10;
    g.setName("g");
    cout << g << endl;
    cis << g << endl;
    f = g;
    cout << f << endl;
    cis << f << endl;
    cis << g << endl;
    cis << g << endl;
    wait();
}
```
```