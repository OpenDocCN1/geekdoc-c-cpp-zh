For example (sample from the spec draft):

# Aggregate Initialisation

```
struct base1 { int b1, b2 = 32 };

struct base2 {
  base2() { b3 = 64 }
  int b3;
};

struct derived : base1, base2 {
  int d;
};

derived d1{{1, 2 }, {}, 4 };
nderived d2{{{}, {}, 4 }};
```

The code initializes d1.b1 with 1, d1.b2 with 2, d1.b3 with 64, d1.d with 4 . And for the second object we have: d2.b1 with 0, d2.b2 with 32, d2.b3 with 64, d2.d with 4

In our case, it has a more significant impact. Because for the overload class, without the aggregate initialisation, we'd had to implement the following constructor:

```
struct overloaded : Fs {
  template < class ... Ts>
  overloaded(Ts&& && ...ts) : Fs(std::forward<Ts>(ts)...)
}

// ...
```

It's a lot of code to write, and probably it doesn't cover all of the cases noexcept.

With aggregate initialisation, we “directly” call the constructor of lambda from the base class list, so there's no need to write it and forward arguments to it explicitly.

OK, we covered a lot, but is there any useful example of the overloaded pattern?

It appears might be convenient for std::variant visitation.

# Example with std::variant and std::visit