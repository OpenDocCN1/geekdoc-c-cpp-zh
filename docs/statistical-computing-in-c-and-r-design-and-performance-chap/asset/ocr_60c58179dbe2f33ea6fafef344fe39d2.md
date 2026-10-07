# NUMERICAL LINEAR ALGEBRA

248

![](bbox=[0.095, 0.133, 0.858, 0.503])

Figure 7.2 GCV criterion over log 10($\lambda$) $\in [-2,0]$

+   a) constructors,
b) destructors,
c) the = = or assignment operator and
d) friends.

The reason for a)-c is that a derived class may have additional members that must be created, destroyed or assigned values. Friend status indicates a relationship between classes and, such, there is no priori reason to expect it to be inherited in very much the same sense as with people where friends of a child need not be friends of a parent and conversely.\ Listing 7.6 provides a simple example of most of the inheritance syntax and features that we will use in the remainder of this section.

Listing 7.6 inheritEx.cpp

```
// inheritEx.cpp
#include <iostream>

using std::cout;  using std::endl;

struct A{
int iA;
A(int ia){iA = ia;}
void output()(){f();}
```