*Bad call of member on nullptr.*

```
~~~cpp
Type *obj = nullptr;
obj->do_thing(); // never do this
~~~
```

Even in the (technically OK, but never do this) scenario of calling `delete this`.

*Bad example of delete this.*

```
~~~cpp
struct S {
  std::string data;

  void delete_yourself() {
    // do things
    delete this; // technically OK

    if (this) {
      // this block will always be executed, nothing changed
      // our view of `this`
    }

    // never do this
    data.size(); // UB, data's lifetime has ended
  }
};
~~~
```

There is no scenario in which a check for if (this) will return false on a modern compiler.

![](bbox=[0.119, 0.538, 0.19, 0.58])

# ## Exercise: Do you check for this to be nullptr?

A check for nullptr can hide a check for NULL or a check against 0. A check for this to be NULL is likely to only exist in very old code bases. Make sure you have your warnings enabled, then look for these cases.