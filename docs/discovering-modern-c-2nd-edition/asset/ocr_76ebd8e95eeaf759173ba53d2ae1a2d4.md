```
}
break;
... more left preconditioners
}
case 1:
... more solvers
}
```

For each new solver and preconditioner, we have to expand this gigantic block in multiple places for each call.

# A.9 More about Meta-Programming

# A.9.1 First Meta-Program in History

Meta-Programming was actually discovered by accident. Erwin Unruh wrote in the early ’90s a program that printed prime numbers as error messages and thus demonstrated that C++ compilers are able to compute. Because the language has changed since Erwin Unruh wrote the example, here is a version adapted to today’s standard C++:

Click here to view code image

```
1 // Prime number computation by Erwin Unruh
2
3 template <int i> struct D { D(void*); operator int(); };
4
5 template <int p, int i> struct is_prime {
6 enum { prim = (p==2) || (p%i) && is_prime<(i>2?p:0), i-1>
7 :: prim };
8 };
9
10 template <int i> struct Prime_print {
11 Prime_print <i-1> a;
12 enum { prim = is_prime <i, i-1>::prim };
13 void f() { D<i> d = prim ? 1 : 0; a.f();}
14 };
15
15 template<> struct is_prime<0,0> { enum {prim=1}; };
16 template<> struct is_prime<0,1> { enum {prim=1}; };
17
18 template<> struct Prime_print<1> {
19 enum {prim=0};
```