non-const operation. If find were not a const function, it could change any member data at all. Because it is const, the only value it can change is the mutex, which has been marked mutable. Simply reading the class declaration tells you this. Indeed, the only context where a mutex member datum does not need to be mutable is if there are no const member functions. Even then, it is a good habit to make mutexes mutable.

Function parameters are also, by default, mutable. They behave like local variables. It is unusual for a function to mutate its arguments: they are used to inform its operation. Of course, the functions in `<algorithm>` which take input iterators are a notable exception to this. However, given that function parameters are also rarely declared const anyway, you may consider avoiding the const qualification of func-tion parameters. For example:

Click here to view code image

```
void f(char const* const p);
void g(int const i);
```

might seem pedantic rather than correct. This is a matter of style and taste. There is another related matter of style and taste regarding const, and that is where to put it.

+   - References cannot be const-qualified.
+   - Pointers are const-qualified to the right.
+   - Member functions are const-qualified to the right.
+   - Types can be const-qualified to the right or to the left of the type. This is known as East const and const West.

References cannot be const-qualified, because a reference cannot be reseated; that is, its referent cannot be changed. Qualifying a reference with const would add no further information.

Pointers sit to the right of a type name. If pointers could be const-qualified to the left, then there would be potential for ambiguity:

Click here to view code image