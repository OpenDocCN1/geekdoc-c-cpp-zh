```
void test9() {
    cout << "9, Overloaded equality operator (identical elements): IntArray m(3, 7);\n    cout << endl;
    IntArray n(1, 5);
    cout << "m";
    cout << endl;
    cout << "n";
    cout << endl;
    csis << endl << endl;\n    cout << endl;
    csis << "9. Overloaded equality operator (identical elements): IntArray m(3, 7);
    csis << endl << endl;\n    IntArray n(1, 5);
    csis << "n";
    cout << endl;
    csis << endl << endl;\n    cout << endl;
    IntArray m(3, 7);
    for(int i = m.low(); i <= m.high(); i++)
        m[i] = i * 10;
    m.setName("m");
    cout << "m" << endl;
    csis << "m" << endl;
    IntArray n(1, 5);
    for(int i = n.low(); i <= n.high(); i++)
        n[i] = i * 10;
    n.setName("n");
    cout << "n" << endl;
    csis << "n" << endl;
    wait();
    cout << "Returns" << (m == n ? "True." : "False.") << endl << endl;
    csis << endl << endl;
    csis << "n" << endl;
    csis << "Returns " << (m == n ? "True." : "False.") << endl << endl;
    wait();
}
```

```
void test10() {
    cout << "10. Overloaded equality operator (different elements): IntArray o(3, 7);\n    cout << endl;
    IntArray p(1, 5);
    cout << "o";
    cout << endl;
    cout << "p";
    cout << endl << endl;
    csis << "10. Overloaded equality operator (different elements): IntArray o(3, 7);
    csis << endl << endl;\n    IntArray p(1, 5);
    csis << "o";
    cout << endl;
    cout << endl;
    csis << "p";
    cout << endl;
    csis << endl << endl;\n    IntArray o(3, 7);
    for(int i = o.low(); i <= o.high(); i++)
        o[i] = i * 10;
    o.setName("o");
    cout << "o" << endl;
    IntArray p(1, 5);
    for(int i = p.low(); i <= p.high(); i++)
        p[i] = i * 10;
    p.setName("p");
    cout << "p" << endl;
    cout << "Returns " << (o == p ? "True." : "False.") << endl << endl;
    csis << endl << endl;
    csis << "Returns " << (o == p ? "True." : "False.") << endl << endl;
    wait();
}
```

# Focus on Object-Oriented Programming with C++