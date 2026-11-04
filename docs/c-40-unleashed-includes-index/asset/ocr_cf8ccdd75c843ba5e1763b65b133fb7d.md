```
calc.AddOperator("F1", (a, b) => {
    Thread.Sleep(5000);
    return a + b;
});
```

When the user of the calculator now uses the F1 function through the UI, the calculator engine will issue a call to the function that was passed to AddOperator:

```
calc.Eval(1, "F1", 2); // calls into the custom delegate
```

However, the added operator is quite evil because it will hang for five seconds before returning the sum. If we blindly invoke the delegate in the calculator engine, this might cause the user interface to appear hung. Or to say it in another way: While the custom function is doing its "work" (which could be sleeping for five seconds!), no other useful work can be done because we're blocked until the call returns.

In fact, we shouldn't even look for contrived examples like sleeping for five seconds; it's quite possible the programmed function is computing-intensive and takes a while to return when faced with specific inputs. Such an example is a very naïve implementation of a Fibonacci function based on recursion:

```
uint Fibonacci(uint n) {
    return n <= 1 ? n : Fibonacci(n - 1) + Fibonacci(n - 2);
}
```

Assume for the sake of argument that our calculator supports not just binary functions but also unary ones and uses uint (or even ulong or BigInteger) rather than int. By now, it shouldn't be a hard exercise for you to extend our Calculator class to support this.

# SPEEDING UP FIBONACCI

A popular programming interview question is to ask for an implementation of an algorithm calculating Fibonacci numbers. Candidates who come up with a recursive approach tend to experience heavy sweating when the interviewer starts asking performance-related questions. Let me share a few thoughts on this subject.

The problem with the recursive algorithm is the excessive recomputation of the intermediate results. For example, take a look at the following expansion of calls:
Fibonacci(5) = Fibonacci(4) + Fibonacci(3)
          = Fibonacci(3) + Fibonacci(2) + Fibonacci(3)
          = ...

If you continue to expand those calls, you'll soon come to the conclusion that lots of wasteful recomputation is taking place. Although this makes this example ideal for the discussion about long-running delegate invocations, it's far from ideal in practice. You'll see how bad things get in a moment.