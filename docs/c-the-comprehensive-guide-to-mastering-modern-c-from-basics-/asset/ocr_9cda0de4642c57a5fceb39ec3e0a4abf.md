```
std::thread f41{ runFib, 41 };
std::thread f42{ runFib, 42 };

f40.join(); f41.join(); f42.join();

std::thread a1{ runAck, 4, 0 };
std::thread a2{ runAck, 4, 1 };
std::thread a3{ runAck, 2, 700 };
std::thread a4{ runAck, 3, 10 };
```

# **Listing 29.3** Add parameters to the thread function in the constructor.

You can simply pass one or more parameters additionally to the constructor of jthread.

> Ackermann and Fibonacci

The fib(log n) function for the n-th Fibonacci number I have used often in different variants in this book as an example for a calculation. The n-th Fibonacci number is the sum of the n-1-th and n-2-th Fibonacci numbers. The first ones are 1, 1, 2, 3, 5, 8, 13, 21—and the sequence continues.

I like to use it because first, you can write the function in one line, and second, it keeps the computer busy for a while. For fib(40), the computer already needs a few seconds to compute; fib(45) becomes a test of patience. However, this is only the case if you write it —as I do here—naively recursively. With a little more effort, you can also get an efficient function, as shown in Listing 29.3. But I don't want to do that for the thread examples.