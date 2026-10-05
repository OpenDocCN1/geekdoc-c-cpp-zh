```
// https://godbolt.org/z/Y3dnsMYCs
#include <chrono>
#include <iostream>
int main() {
    using namespace std::chrono;
    milliseconds myMs = 4000ms;
    std::cout << myMs.count()/1000 << "\n"; // Where here lose thousands
    std::cout << myMs.count()/1000 << "\n"; // Where here lose thousands
    std::cout << duration_seconds(myMs).count() << "\n"; // explicit
    std::cout << microseconds(myMs).count() << "\n"; // like implicit
}
```

**Listing 28.25** Do not make your calculations using "count()".

It is much less error-prone to use <chrono> to do the work in one place. The performance is also not worse than if you programmed yourself by hand.

If the compiler tells you somewhere that it cannot convert something, believe it. Do not bypass its warning by using count() and your own calculation. The probability is high that you have made a logical error somewhere.

You can also mix conversions and arithmetic. An expression can contain different units. So long as no information is lost during the conversions, it works seamlessly.

```
// https://godbolt.org/z/vTx4cdqza
#include <chrono>
#include <iostream>
void showDuration(std::chrono::milliseconds dur) {
    std::cout << dur.count() << "ms\n";
}
int main() {
    using namespace std::chrono;
    auto x = 2s;
    auto y = 3ms;
    showDuration(x + y); // Output: 2003ms
    showDuration(x - y); // Output: 1997ms
}
```

**Listing 28.26** You can mix units.

Here, x is automatically converted to milliseconds before + or - is performed.