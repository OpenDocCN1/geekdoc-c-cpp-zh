```
```cpp
21    auto val = myStack.top();
22    myStack.pop();
23    return val;
24  }
25  ConcurrentStack() = default;
26  ConcurrentStack(const ConcurrentStack&) = delete;
27  ConcurrentStack& operator = (const ConcurrentStack&) = delete;
28 private:
29    mutable std::mutex mutexStack;
30    std::stack<T, Cont<T, std::allocator<T>>> myStack;
31  };
32
33  int main() {
34
35    ConcurrentStack<int> conStack;
36
37    auto fut = std::async([&conStack] { conStack.push(2011); });
38    auto fut1 = std::async([&conStack] { conStack.push(2014); });
39    auto fut2 = std::async([&conStack] { conStack.push(2017); });
40
41    auto fut3 = std::async([&conStack] { return conStack.topAndPop(); });
42    auto fut4 = std::async([&conStack] { return conStack.topAndPop(); });
43    auto fut5 = std::async([&conStack] { return conStack.topAndPop(); });
44
45    fut.get(), fut1.get(), fut2.get();
46
47    std::cout << fut3.get() << '\n';
48    std::cout << fut4.get() << '\n';
49    std::cout << fut5.get() << '\n';
50
51  }
```
```

The member function topAndPop (lines 18 - 24) returns a copy instead of a reference such as the member function top before. Calling pop on an empty container is undefined behavior. I prefer to throw a std::out_of_range exception (line 20) if the stack is empty. Returning a special non-value or returning a std::optional¹ is also a valid option. Copying the value has a downside. If the copy constructor of the value type throws an exception such as std::bad_alloc², the value is lost.

The calls fut.get(), fut1.get(), fut2.get() (line 45) ensure that the associated promise runs. If you don't specify the launch policy, the promise may run lazily in the caller's thread. Lazily means that the promise will execute if and only if the future asks for its result with get or wait. Launching the promises in a separate thread is also a valid option:

¹https://en.cppreference.com/w/cpp/utility/optional
²https://en.cppreference.com/w/cpp/memory/new/bad_alloc