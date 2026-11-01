Here you can see how tie has been eliminated and replaced with some syntactic sugar in the form of auto and brackets.

Structured binding was my favorite C++17 feature. You can even use it to bind to an array or a struct:

Click here to view code image

```
int a[2] = {1, 2};
auto [b, c] = a; // b and c are ints, where b = 1
and c = 2

struct S {
    int a;
    int b;
};
S make_s();

auto [d, e] = make_s(); // d = the first member of
the returned struct
                        // e = the second member.
```

The use cases for out parameters are few. While returning tuples is a neat trick, do not overlook returning a struct. If your return values are related in some way, you may be in the process of unearthing an abstraction. The same tricks used to return a tuple are used to return a struct. Copy elision means the values are created where they will be needed by the caller.

Always check that you are not discarding an abstraction when you merely return a tuple. A pair of BigObj and an error code doesn’t sensibly lend itself to being com-posed into a new abstraction, but a tuple consisting of several related objects most likely needs names for the individual parts. Consider the string and the character count: there is a small abstraction with a name like modified_string waiting to be manifested.

> Always check that you are not discarding an abstraction when you merely return a tuple.