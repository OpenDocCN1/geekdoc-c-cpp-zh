# C++ Maths

Programming is mathematical in nature and as you might expect, there is plenty of built-in scope for some quite intense maths. C++ has a lot to offer someone who is implementing mathematical models into their code. It can be extremely complex or relatively simple.

# C++ = MC²

The basic mathematical symbols apply in C++ as they do in most other programming languages. However, by using the C++ Math Library, you can also calculate square roots, powers, trig and more.

+   C++ mathematical operations follow the same patterns as taught in school, in that multiplication and division takes precedence over addition and subtraction. You can also alter that. For now, create a new file and enter.

```
#include <iostream>
using namespace std;
int main() {
    float numbers = 100;
    numbers = numbers + 10;  // This adds 10 to the initial
    cout << "\n";
    numbers = numbers - 10;  // This subtracts 10 from the new
    cout << "\n"
}
```

+   Multiplication and division can be applied as such:
#include <iostream>
using namespace std;
int main() {
    float numbers = 100;
    numbers = numbers * 10;  // This multiplies 100
    cout << "\n";
    numbers = numbers / 10;  // And divides 1000 by
    cout << "\n"
}

While simple, it does the old maths warmed up. We used a float for the variables. While you can use an integer, if you to use decimals, you would need to change it to a float or double, depending on the accuracy needed. Run the code and see.

Again, while not particularly interesting, the code and see the results. It's a start into C++ maths. We used a float, so you can play around with the code and multiply by decimal places, as well as divide, add and subtract.

![](bbox=[0.065, 0.775, 0.31, 0.785])

```
#include <iostream>
using namespace std;
int main() {
    float numbers = 100;
    numbers = numbers * 10;  // This multiplies 100 by 10
cout << "\n"
    numbers = numbers / 10;  // And divides 1000 by 10
cout << "\n"
}
```

```
Process returned (0x) execution time : 0.043 s
Press any key to continue.
```

```
Process returned (00) execution time : 0.050 s
Press any key to continue.
```

![](bbox=[0.515, 0.865, 0.765, 0.875])