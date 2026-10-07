# GOLDEN SECTION

#include "funcTemp.h"
using std::cout; using std::endl;
struct Y{}

```
int func(double x){
cout << "Calling from Y func" << endl;
return ceil(x);
}
```

class Z{
public:

```
int func(double x){
cout << "Calling from Z func" << endl;
return floor(x);
}
```

```
int main() {
Y; Z;
Functor<Y> f1(&y, &Y::func);
cout << f1(2.5) << endl;
Functor<Z> f2(&z, &Z::func);
cout << f2(2.5) << endl;
return 0;
}
```

Both Y and Z objects are created in the program and Functor class objects are used to call the func method from both classes. The only trick is that the template parameters must be specified (i.e., the specific choices for T must be given) when the Functor class constructor is called. The output from the program is

Calling from Y func
3
Calling from Z func
2

The complaint could be lodged that our newest version of the Functor class is limited by the fact that it can handle only a member function with prespecified argument and return types of double and int. This restriction can also be removed using the template approach (Exercise 8.1). For now, the generality provided by the formulation in 8.5 will be sufficient.

# 8.3 Golden section

In this section we develop our first optimization method. To begin, let us deal with a simple case where a convex function f is defined on the integers $N_m = \{1, \dots, m\}$. The objective is to find the fastest algorithm in the sense that it finds the fewest evaluations $\nu_n$ of f on $N_m$ to find its minimum. Our discussion of this problem stems from developments in Kiefer (1953) and Monahan (2001).

One may check that an arbitrary choice is allowed for f, then $\nu_2 = 2$ and $\nu_3 = 3$. For $m=4$ and $N_4 = \{1, 2, 3, 4\}$, the minimizer can be found in $v_4 = 3$ evaluations if f is first