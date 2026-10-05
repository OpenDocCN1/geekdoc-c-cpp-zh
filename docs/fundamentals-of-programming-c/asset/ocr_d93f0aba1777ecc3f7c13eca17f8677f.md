# 13.4 Complex Numbers

C++ supports mathematical numbers via the complex class. Recall from mathematics that a complex number has a real component and an imaginary component. Often written as a+bi, a is the real part, ordinary real number, and bi is the imaginary part where b is a real number and i^2 = -1.

The complex class in C++ is a complex vector. In the angle you specify the precision of the number's components:

```
complex<float> fc;
complex<double> dc;
complex<long> ldc;
```

Here, the real and imaginary coefficient of fc are single-precision floating-point values. dc and ldc have the indicated precisions. Listing 13.7 (complex.cpp) is small example that computes the product of complex conjugates (which should be real numbers).

```
Listing 13.7: complex.cpp
// File complex.cpp
#include <iostream>
#include <complex>

using namespace std;

int main() {
    // c1 = 2 + 3i, c2 = 2 - 3i; c1 and c2 are complex conjugates
    complex<double> c1(2.0, 3.0), c2(2.0, -3.0);

    // Compute product "by hand"
    double real = c1.real();
    double imag1 = c1.imag();
    double real2 = c2.real();
    double imag2 = c2.imag();

    cout << c1 << " * " << c2 << " = " << endl;
    cout << real*real2 + imag1*real2 + real*imag2 - imag1*imag2 << endl;

    // Use complex arithmetic
    cout << c1 << " + " << c2 << " = " << c1+c2 << endl;
}
```

Listing 13.7 (complex.cpp) prints

| (2,3) * (2,-3) = 13 |
| (2,-3) * (2,3) = (13,0) |

Observe that the program displays the complex number 2-3i as the ordered pair (2,-3). The first element of the pair is the real part, and the second element is the imaginary coefficient. If the imaginary part is zero, the number is a real (or, in this case, a double).

Imaginary numbers have scientific and engineering applications that extend the scope of this book, so this concludes our brief into C++s complex class. If you need to solve problems that involve complex numbers, more information can be found at http://www.cplus.com/reference/std/complex/.