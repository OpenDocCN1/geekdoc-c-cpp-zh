# 10.11. EXERCISES

(a) What is printed if main is written as follows?

```
int main() {
    input = 5;
    cout << sum1(input) << endl;
    cout << sum2(input) << endl;
    cout << sum3(input) << endl;
}
```

(b) What is printed if main is written as follows?

```
int main() {
    input = 5;
    cout << sum1(input) << endl;
    cout << sum3(input) << endl;
    cout << sum2() << endl;
}
```

(c) What is printed if main is written as follows?

```
int main() {
    input = 5;
    cout << sum2(input) << endl;
    cout << sum1(input) << endl;
    cout << sum3(input) << endl;
}
```

(d) Which of the functions sum1, sum2, and sum3 produce a side effect? What is the side effect?
(e) Which function may not use the input variable?
(f) What is the scope of the variable i? What is its lifetime?
(g) What is the scope of the variable I?
(h) Which of the functions sum1, sum2, and sum3 manifest good functional independence? Why?

2. Consider the following C++ code:

```
#include <iostream>

using namespace std;

int next_int1() {
    static int cnt = 0;
    cnt++;
    return cnt;
}

int next_int2() {
    int cnt = 0;
    cnt++;
    return cnt;
}

int global_count = 0;
```