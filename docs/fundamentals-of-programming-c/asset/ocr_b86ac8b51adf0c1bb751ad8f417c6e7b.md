# 9.8. EXERCISES

```
result += n;
--;
}
return result;

void fun2(int stars) {
  for (int i = 0; i < stars; i++)
    std::cout << "*";
    std::cout << std::endl;
}
ndouble fun3(double x, double y) {
  return 2*x*x + 3*y;
}
bool fun4(char ch) {
  return ch >=='A' && ch <= 'Z';
}
bool fun5(int a, int b, int c) {
  return (a <= b) ? (b <= c) : false;
}
int fun6() {
  return rand() % 2;
```

Examine each of the following print statements. If the statement is illegal, explain why it is illegal; otherwise indicate what the statement will print.

+   (a) cout << fun1(5) << endl;
(b) cout << fun1() << endl;
(c) cout << fun1(5, 2) << endl;
(d) cout << fun2(5) << endl;
(e) fun2(5);
(f) cout << fun3(5, 2) << endl;
(g) cout << fun3(5.0, 2.0) << endl;
(h) cout << fun3('A', 'B') << endl;
(i) cout << fun3(5.0) << endl;
(j) cout << fun3(5.0, 0.5, 1.2) << endl;
(k) cout << fun4('T') << endl;
(l) cout << fun4('t') << endl;
(m) cout << fun4(5000) << endl;
(n) fun4(5000);
(o) cout << fun5(2, 4, 6) << endl;