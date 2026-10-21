In Kotlin, closures can write the captured data, as they do in Scala:

```
fun <A, B> single(f: (A) -> B): (A) -> B {
    var called = false
    return { x ->
        if (called) throw IllegalStateException()
        called = true
        f(x)
    }
}
```

This example creates a variant of a function f that can be invoked only once before it throws an exception—for instance, for the purpose of testing. This requires writing the Boolean variable called from the closure. By contrast, Java does not allow closures to reassign variables. This code is rejected by the compiler:

```
<A, B> Function<A, B> single(Function<A, B> f) {
    var called = false;
    return x -> {
        if (called) throw new IllegalStateException();
        called = true; // rejected at compile time
        return f.apply(x);
    };
}
```

Instead, you can replace the lambda expression with an anonymous class that defines a reassignable Boolean field:

```
<A, B> Function<A, B> single(Function<A, B> f) {
    return new Function<>() {
        private boolean called = false;

        public B apply(A x) {
            if (called) throw new IllegalStateException();
            called = true;
            return f.apply(x);
        }
    };
}
```

The argument f is still captured in a closure, but it is only read and not reassigned.