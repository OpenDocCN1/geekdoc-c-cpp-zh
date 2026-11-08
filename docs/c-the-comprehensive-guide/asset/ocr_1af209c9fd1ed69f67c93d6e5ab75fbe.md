container. But that would not have worked in the example. Because as practical and safe as a reference, it cannot do two things that a pointer can:

+   - **You cannot reassign a reference**
+   
+     When you write `int value = 42; int &ref = value;`, `ref` will always refer to `value` from now on. So with `ref = 99;`, you are always assigning something new to `value`. However, if you have an `int *ptr = &value;` pointer, you can achieve the same thing with `*ptr = 66;` as with the reference, but you can also point to a completely new variable.
+   
+     The following would work with references:

```
int value = 42;
int &ref = value;
ref = 99;        // value is now 99
int *ptr = &value;
*ptr = 66;       // value is now 66
int new_value = 73;
ptr = &new_value; // ptr no longer points to value
*ptr = -1;       // value remains 66, new_value is now -1
```

+   - **You cannot store references in a container**
+   
+     There can be no `vector<int&>` or similar. A reference is something abstract that only exists for the compiler. In the compiled program and at runtime, you no longer see any trace of it. However, every container needs a physically present piece of memory for its elements. So here you need some form of pointer—be it a smart pointer, raw pointer, or even iterator, as you will see later.

Here, raw pointers certainly have a field of application. If the objects in the container are not owned by the pointers, then unique_ptrs are out of the question anyway. shared_ptrs would be possible, but why should you manage shared ownership when it does not exist? Raw pointers are just the right thing for that.

```
// https://godbolt.org/z/W4W6lh14kV
#include <vector>
#include <numeric>      // iota
#include <iostream>
using std::vector; using std::cout;
struct Number {          // representative of a large, expensive object
    unsigned long val_;
    Number(unsigned long val) : val_{val} {}
    Number() : val_{0} {}
};

/* determines whether z is a prime number based on previous prime numbers */
bool isPrime(const Number& z, const vector<Number*> primes) {
    for(Number* p : primes) {
```