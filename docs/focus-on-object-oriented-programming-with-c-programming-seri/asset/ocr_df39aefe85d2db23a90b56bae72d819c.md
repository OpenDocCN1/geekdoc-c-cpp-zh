Note that the explicit call to the functions `Base::operator=()` was written using functional notation. If you want to use infix notation, you may use either of the following two methods:

+   - `(base)this = d;`
+   - `((base&)*this) = d;`

The first statement casts the `Derived` pointer into a `Base` pointer, and then dereferences the result to produce the `Base` class portion of the invoking instance. Therefore, the `Base` class `operator=()` will be called.

The second statement achieved the same result, but in a more direct fashion, with the invoking instance itself now cast into a reference to the `Base` class.