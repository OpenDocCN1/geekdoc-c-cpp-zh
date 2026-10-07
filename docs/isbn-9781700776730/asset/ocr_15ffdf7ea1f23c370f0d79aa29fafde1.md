```
void test1() {
    cout << "1. Array declared with illegal array bounds: IntArray f(5, 2);";
    cout << endl << endl;
    csis << "1. Array declared with illegal array bounds: IntArray f(5, 2);";
    cout << endl << endl;
    IntArray f(b, 2);
    for(int i=0; i<=f.low(); i<= f.high(); i++) {
        f.setName("*");
        cout << f << endl;
        csis << f << endl;
    }
    wait();
}
```

```
void test2() {
    cout << "18. Array with index out of range: IntArray q(10);" << endl;
    cout << ""
    q[10] = 1 << endl;
    csis << "18. Array with index out of range: IntArray q(10);" << endl;
    q[10] = 1 << endl;
    csis << ""
    IntArray q(10);
    for(int i=q.low(); i<= q.high(); i++) {
        q[i] = i * 10;
        q.setName("q");
        cout << q << endl;
        csis << q << endl;
    }
    wait();
}
```

```
void test3() {
    cout << "19. Arrays with length mismatch: IntArray m(1, 4);" << endl;
    cout << ""
    IntArray n(2, 4);
    csis << "19. Arrays with length mismatch: IntArray m(1, 4);" << endl;
    cout << ""
    IntArray n(2, 4) << endl;
    csis << ""
    csis << ""
    IntArray m(1, 4);
    for(int i=m.low(); i<= m.high(); i++) {
        m[i] = i * 10;
        m.setName("m");
        cout << m << endl;
        csis << m << endl;
    }
    IntArray n(2, 4);
    for(int i=n.low(); i<= n.high(); i++) {
        n[i] = i * 10;
        n.setName("n");
        cout << n << endl;
        csis << n << endl;
    }
    wait();
    m
    cout << m << endl;
    cout << n << endl;
    csis << m << endl;
    csis << n << endl;
    wait();
}
```

# Focus on Object-Oriented Programming with C++