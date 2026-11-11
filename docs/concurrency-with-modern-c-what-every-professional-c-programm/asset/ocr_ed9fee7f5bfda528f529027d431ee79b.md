```
45  auto fut3 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
46  auto fut4 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
47  auto fut5 = std::async([&lockFreeStack]{ return lockFreeStack.topAndPop(); });
48
49  fut.get(), fut1.get(), fut2.get();
50
51  std::cout << fut3.get() << '\n';
52  std::cout << fut4.get() << '\n';
53  std::cout << fut5.get() << '\n';
54
55 }
```

The member function topAndPop returns the top element of the stack. It reads the head element of the stack (line 29) and make the next node the new head if oldHead is not a nullptr (line 30). oldHead is a nullptr if the stack is empty. I decided to throw an exception if the stack is empty (line 31). Returning a special non-value or returning a std::optional⁴³ is also a valid option. Copying the value has a downside. If the copy constructor of the value throws an exception such as std::bad_alloc⁴⁴, the value is lost. Finally, the member functions returns the head element (line 33).

The calls fut.get(), fut1.get(), fut2.get() (line 49) ensure that the associated promise runs. If you don't specify the launch policy, the promise may run lazily in the caller's thread. Lazily means that the promise will execute if and only if the future asks for its result with get or wait. You can also launch the promise in a separate thread:

Launching each promise in a separate thread

```
    auto fut = std::async(std::launch::async, [&conStack]{ conStack.push(2011); });
    auto fut1 = std::async(std::launch::async, [&conStack]{ conStack.push(2014); });
    auto fut2 = std::async(std::launch::async, [&conStack]{ conStack.push(2017); });
```

Finally, the output of the program:

> ⁴³https://en.cppreference.com/w/cpp/utility/optional

> ⁴⁴https://en.cppreference.com/w/cpp/memory/new/bad_alloc