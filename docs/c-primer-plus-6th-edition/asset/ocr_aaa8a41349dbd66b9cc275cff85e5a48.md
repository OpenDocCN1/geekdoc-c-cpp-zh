# Wrappers 1193

```
int main() {
{
    using std::cout;
    using std::endl;

    double y = 1.21;
    cout << "Function pointer dub:\n";
    cout << " " << use_f(y, dub) << endl;
    cout << "Function pointer square:\n";
    cout << " " << use_f(y, square) << endl;
    cout << "Function object Fp:\n";
    cout << " " << use_f(y, Fp(5.0)) << endl;
    cout << "Function object Fq:\n";
    cout << " " << use_f(y, Fq(5.0)) << endl;
    cout << "Lambda expression 1:\n";
    cout << " " << use_f(y, [](double u) {return u*u;}) << endl;
    cout << "Lambda expression 2:\n";
    cout << " " << use_f(y, [](double u) {return u+u/2.0;}) << endl;
    return 0;
}
```

The template parameter T is set to double for each call. What about template argument F? Each time the actual argument is something that a double argument and returns a type double value, so it might seem that F would be the same type for all six calls to use_f() and that the template would be instantiated just once. But as the following sample output shows, that belief is naive:

Function pointer dub:
use_f count = 1, &count = 0x0402028
2.42

Function pointer square:
use_f count = 2, &count = 0x0402028
1.1

Function object Fp:
use_f count = 1, &count = 0x0402020
6.05

Function object Fq:
use_f count = 1, &count = 0x0402024
6.21

Lambda expression 1:
use_f count = 1, &count = 0x0405020
1.4641

Lambda expression 2:
use_f count = 1, &count = 0x040501c
1.815