```
char f(double);
char c1 = g(N::A()); char c2 = g(2);
char c3 = g(2.1);
// causes N::f(N::A) to be called
// causes f(int) to be called
// causes f(int) to be called; f(double) not considered
```

Here, f(t) is clearly dependent, so we can’t bind f at the point of definition. To generate a specialization for g<N::A>(N::A), the implementation looks in namespace N for functions called f() and finds N::f(N::A).

The f(int) is found because it is in scope at the point of definition of the template. The f(double) is not found because it is not in scope at the point of definition of the template (§iso.14.6.4.1), and argument-dependent lookup (§14.2.4) does not find a global function that takes only arguments of built-in types. I find it easy to forget that.

# 26.3.6 Overaggressive ADL

Argument-dependent lookup (often referred to as ADL) is very useful to avoid verbosity (§14.2.4). For example:

```
#include <iostream>
int main()
{
std::cout << “Hello, world” << endl;// OK because of ADL
}
```

Without argument-dependent lookup, the endl manipulator would not be found. As it is, the compiler notices that the first argument to << is an ostream defined in std. Therefore, it looks for endl in std and finds it (in <iostream>).

However, ADL can be “too aggressive” when combined with unconstrained templates. Consider:

```
#include<vector>
#include<algorithm>
// ...
namespace User {
class Customer { /*...*/ };
using Index = std::vector<Customer*>;
void copy(const Index&, Index&, int deep); // deep or shallow copy depending on the value of deep
void algo(Index& x, Index& y) {
// ...
copy(x,y,false); // error
}
}
```