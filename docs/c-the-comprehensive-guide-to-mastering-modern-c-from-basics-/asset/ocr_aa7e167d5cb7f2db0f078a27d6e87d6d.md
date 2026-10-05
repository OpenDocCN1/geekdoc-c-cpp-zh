are of different types, it will try b !== a and ! (b ==na). If you do not want this, then define the
corresponding overloads yourself.

+   * Use constexpr, noexcept or const
If you can, mark your operators with constexpr and
noexcept. Member functions should at least be marked
with const.

+   * Preincrement and decrement
operator++() and operator--() modify the object
immediately and return it as a reference. This
allows, for example, ++a. If you use a++ instead
(postincrement), then a copy of the old value needs to
 created and returned; you should avoid this and
prefer the pre variants. If you still want to provide the
post variants, you need to define operator++(int) and
operator--(int). The int parameter is just a dummy
and is not used; it only serves to distinguish the
overload. The implementation would look like this:

```
//The Less efficient a++ and --
Num::operator++(int) { Num res{this}; val++; return res; }
Num::operator--(int) { Num res{this}; val--; return res; }
```

+   * Dereference operator
The unary operator* is typically used to access the
“real value” of a class. Good examples of this are
uniqueunique_ptr, all iterators, and raw pointers. So if you
write Num a{7}; you can now write *a to access val.
Because I also return a reference with int&, you can
deven *a = 99; to change the value.