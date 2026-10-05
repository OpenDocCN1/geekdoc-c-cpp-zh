```
// Compute
// for partial result
long sum1 = 0;
std::jthread th1(sumIt, std::ref(sum1));
long sum2 = 0; // for partial result
std::thread th2(sumIt, std::ref(sum2));
th1.join(); th2.join();
long Sum = sum1 + sum2; // Total result
// Result
std::cout << "Expected result: "
  << (1'0000'001L*1'0000'001)/2 << '\n'; // Output: 500000500000
std::cout << "Actual: "
  // Output: 500000500000
  << sum << '\n';
```

# Listing 29.21 A very simple thread-safe stack.

Regarding concurrency, the following can be said:

+   * Both push and pop are each protected with a lock_guard on the same mutex, so they do not interfere with each other.
* isEmpty does not need to be protected.
* pop can throw an exception if the container is empty.
* pop attempts to move the element out of the internal vector. For this, T should support moving. If not, then it will be copied.
* It is important that copying or moving T does not throw an exception. If you do this during pop(), the value is not successfully written but already removed from the stack. This is called not exception-safe.
* To make the pop method exception-safe, you could take other measures, but that goes beyond the scope of this chapter.

Outside the influence of MxStack, I had to consider one thing for parallelism. I let th1 and th2 add their