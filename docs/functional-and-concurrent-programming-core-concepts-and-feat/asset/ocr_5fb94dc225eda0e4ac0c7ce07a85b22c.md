```
Computation<Boolean> isOdd(int n) {
    if (n == 0) return done(false);
    else return call(() -> isEven(n - 1));
}

isEven(1_000_000).result() // true
```

Listing 14.5: Optimized tail-calls, using a trampoline, Java variant.

The main differences from the Scala variant are that you need to invoke function done explicitly (instead of relying on an implicit conversion in Scala), and you must use a lambda expression as the argument for function call (instead of a by-name argument in Scala).

# 14.4 Dealing with Non-Tail-Calls

The trampolines implemented in Listings 14.2 and 14.4 can only deal with tail-calls. Can anything be done to handle non-tail-calls, and thus tackle general recursion with no need to grow the execution stack? If a call is not in tail position, you need a way to use the value produced by the call in the continuing code. The key idea is to use map (and flatMap) as a mechanism to transform the result of a function call according to some additional computation. This section extends the Computation type with map and flatMap methods to handle non-tail-calls.

Consider first a non-tail recursive factorial function as an illustration:

```
def factorial(n: Int): BigInt = if n == 0 then BigInt(1) else factorial(n - 1) * n

factorial(1_000_000) // throws StackOverflowError
```

This function is not tail recursive because a computation—a multiplication by n—needs to take place after the recursive call. For this, you need to keep n on the execution stack while computing factorial(n - 1), and the stack grows. For large enough inputs, the function fails with a StackOverflowError.

If the Computation type from Listing 14.2 is used, the recursive call factorial(n - 1) produces a value of type Computation[BigInt]. What you need then is to multiply the (yet to be computed) BigInt inside this computation by n to produce another Computation[BigInt]. This suggests regarding a computation as one