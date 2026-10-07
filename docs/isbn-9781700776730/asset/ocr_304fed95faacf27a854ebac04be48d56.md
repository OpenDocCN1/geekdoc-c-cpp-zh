```
void test1() {
    cout << " 11. Overloaded inequality operator (different elements):" << IntArray(3
```

```
void test2() {
    cout << " 14. Overloaded inequality operator (different size arrays):" << IntArray(w, 3) << " " << endl;
    cout << IntArray(1, 4) << " " << endl;
    cout << endl;
    cout << endl;
    cout << " 14. Overloaded inequality operator (different size arrays):" << IntArray(w, 3) << " " << endl;
    cout << IntArray(1, 4) << " " << endl;
    cout << endl;
    cout << w << " x" << endl;
IntArray w(1, 3);
    for (int i = 0; i < w.high(); i++) {
        for (int j = 0; j < 10; j++) {
            w.setName("w");
            cout << endl;
        }
    }
IntArray x(1, 4);
    for (int i = 0; i < x.high(); i++) {
        for (int j = 0; j < 10; j++) {
            x.setName("x");
            cout << endl;
        }
    }
    cout << w << " x" << endl;
    cout << " Returns: " << (w == x ? "True" : "False") << endl << endl;
    cout << " Returns: " << (w == x ? "True" : "False") << endl << endl;
    wait(10);
}
```