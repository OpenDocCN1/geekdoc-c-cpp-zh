

```cpp
void test9() {
    cout << "9. 重载相等运算符（相同元素）：IntArray m(3, 7);\n";
    cout << endl;
    IntArray n(1, 5);
    cout << "m";
    cout << endl;
    cout << "n";
    cout << endl;
    cout << endl << endl;\n";
    cout << endl;
    cout << "9. 重载相等运算符（相同元素）：IntArray m(3, 7);
    cout << endl << endl;\n";
    IntArray n(1, 5);
    cout << "n";
    cout << endl;
    cout << endl << endl;\n";
    cout << endl;
    IntArray m(3, 7);
    for(int i = m.low(); i <= m.high(); i++)
        m[i] = i * 10;
    m.setName("m");
    cout << "m" << endl;
    cout << "m" << endl;
    IntArray n(1, 5);
    for(int i = n.low(); i <= n.high(); i++)
        n[i] = i * 10;
    n.setName("n");
    cout << "n" << endl;
    cout << "n" << endl;
    wait();
    cout << "Returns " << (m == n ? "True." : "False.") << endl << endl;
    cout << endl << endl;
    cout << "n" << endl;
    cout << "Returns " << (m == n ? "True." : "False.") << endl << endl;
    wait();
}
```

```cpp
void test10() {
    cout << "10. 重载相等运算符（不同元素）：IntArray o(3, 7);\n";
    cout << endl;
    IntArray p(1, 5);
    cout << "o";
    cout << endl;
    cout << "p";
    cout << endl << endl;
    cout << "10. 重载相等运算符（不同元素）：IntArray o(3, 7);
    cout << endl << endl;\n";
    IntArray p(1, 5);
    cout << "o";
    cout << endl;
    cout << endl
    cout << "p";
    cout << endl;
    cout << endl << endl;\n";
    IntArray o(3, 7);
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
    cout << endl << endl;
    cout << "Returns " << (o == p ? "True." : "False.") << endl << endl;
    wait();
}
```

# 关注 C++ 面向对象编程

```cpp
void test11() {
    cout << "11. 重载相等运算符（不同大小的数组）：" << IntArray q(1, 3);
    cout << endl;
    cout << " << IntArray r(1, 4);
    cout << endl;
    cout << q << r << endl;
    cout << endl << endl << endl;
    cout << "11. 重载相等运算符（不同大小的数组）：" << IntArray q(1, 3);
    cout << endl;
    cout << " << IntArray r(1, 4);
    cout << endl;
    cout << " << q << r << endl;
    cout << endl << endl;
    
 << endl << endl endl endl;;
    IntArray q(1, 3);
    for(int i = q.low(); i <= q.high(); i++) {
        cout << i << " * 10";
    }
    q.setName("q");
    cout << << << endl;
    cout << endl << endl

    IntArray(11  4);
    for(int i = r.low(); i <= r.high(); i++) {
        cout << i << " * 10";
    }
    r.setName("r");
    cout << r << endl;
    cout << "Returns " << (q == r ? "True." : "False.") << endl << endl;
    cout << r << endl;
    cout << "Returns " << (q == r ? "True." : "False.") << endl << endl;
    wait();
}
```

```cpp
void test12() {
    cout << "12. 重载不等相等运算符（相同元素）：IntArray s(3, 7);
    cout << endl;
    cout << " << IntArray t(1, 5);
    cout << endl;
    cout << s << t << endl;
    cout << endl << endl endl;
    cout << "12. 重载不等相等运算符（相同元素）：IntArray s(3, 7);
    cout << endl;
    cout << " << IntArray t(1, 5);
    cout << endl;
    cout << s << t << endl;
    cout << endl << endl endl;
    IntArray s(3, 7);
    for(int i = s.low(); i <= s.high(); i++) {
        cout << i << " * 10";
    }
    s.setName("s");
    cout << s << endl;
    cout << s << endl;
    IntArray t(1, 5);
    for(int i = t.low(); i <= t.high(); i++) {
        cout << i << " * 10";
    }
    t.setName("t");
    cout << t << endl;
    cout << t << endl;
    wait();
    s = t;
    cout << s << endl;
    cout << t << endl;
    cout << "Returns " << (s != t ? "True." : "False.") << endl << endl;
    cout << s << endl;
    cout << t << endl;
    cout << "Returns " << (s != t ? "True." : "False.") << endl << endl;
    wait();
}
```

# 关注 C++ 面向对象编程

```cpp
void test1() {
    cout << "1. 边界不法的数组声明：IntArray f(5, 2);";
    cout << endl << endl;
    cout << "1. 边界不法的数组声明：IntArray f(5, 2);";
    cout << endl << endl;
    IntArray f(b, 2);
    for(int i=0; i<=f.low(); i<= f.high(); i++) {
        f.setName("*");
        cout << f << endl;
        cout << f << endl;
    }
    wait();
}
```

```cpp
void test2() {
    cout << "18. 索引越界的数组：IntArray q(10);" << endl;
    cout << endl
    q[10] = 1 << endl;
    cout << "18. 索引越界的数组：IntArray q(10);" << endl;
    q[10] = 1 << endl;
    cout << endl
    IntArray q(10);
    for(int i=q.low(); i<= q.high(); i++) {
        q[i] = i * 10;
        q.setName("q");
        cout << q << endl;
        cout << q << endl;
    }
    wait();
}
```

```cpp
void test3() {
    cout << "19. 长度不匹配的数组：IntArray m(1, 4);" << endl;
    cout << endl
    IntArray n(1, 5);
    cout << "19. 长度不匹配的数组：IntArray m(1, 4);" << endl;
    cout << endl
    IntArray n(1, 5) << endl;
    cout << endl
    cout << endl
    IntArray m(1, 4);
    for(int i = m.low(); i <= m.high(); i++) {
        m[i] = i * 10;
        m.setName("m");
        cout << m << endl;
        cout << m << endl;
    }
    IntArray n(1, 5);
    for(int i = n.low(); i <= n.high(); i++) {
        n[i] = i * 10;
        n.setName("n");
        cout << n << endl;
        cout << n << endl;
    }
    wait();
    cout << "Returns " << (m == n ? "True." : "False.") << endl << endl;
    cout << endl << endl;
    cout << "n" << endl;
    cout << "Returns " << (m == n ? "True." : "False.") << endl << endl;
    wait();
}
```

