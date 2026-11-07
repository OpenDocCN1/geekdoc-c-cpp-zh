This example can be found at

https://godbolt.org/z/jn4MK3o9T

As you type code into the Compiler Explorer editor or when you load an existing example, Compiler Explorer automatically compiles and runs it or displays any compilation errors.

```
```cpp
// fig12_08.cpp
// quotient function with a contract precondition.
#include <iostream>

double quotient(double numerator, double denominator)
  [[pre: denominator != 0.0]];

int main() {
  std::cout << "quotient(100, 7): " << quotient(100, 7)
            << "\nquotient(100, 0): " << quotient(100, 0) << '\n';
}

// perform division
double quotient(double numerator, double denominator) {
  return numerator / denominator;
}
```
```

**Fig. 12.8**  quotient function with a contract precondition.

We preset the compiler options for this example to

`-std=c++20 -fcontracts`

which compiles the code with C++20 and experimental contracts support. Compiler Explorer generally shows at least two tabs—a code editor and a compiler. Our examples also show the output tab so you can see the executed program’s results—this is also where compilation errors would be displayed. The compiler tab has two drop-down lists at the top. One lets you select the compiler. The other lets you view and edit the compiler options, or you can click the down arrow to select common compiler options.

The quotient call at line 9 satisfies the precondition and executes successfully, producing:

```
```text
quotient(100, 7): 14.2857
```
```

The quotient call at line 10, however, causes a **contract violation**. So, the **default violation handler (handle_contract_violation)** is implicitly called, displays the following error message, then terminates the program:

```
```text
default std::handle_contract_violation called:
./example.cpp 6 quotient denominator != 0.0 default default 0
```
```