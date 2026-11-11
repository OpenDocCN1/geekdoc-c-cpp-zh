```
```cpp
39 herb.join();
40 andrei.join();
41 scott.join();
42 bjarne.join();
43 bart.join();
44 jenna.join();
45 
46 std::cout << "\n" << "Boss: Let's go home." << '\n';
47 
48 std::cout << '\n';
49 
50 }
```
```

The only change to the previous program coutUnsynchronized.cpp is that std::cout is wrapped in a std::osyncstream (line 16). To use the std::osyncstream, I add the header <syncstream>. When the std::osyncstream goes out of scope in line 17, the characters are transferred, and std::cout is flushed. It is worth mentioning that the std::cout calls in the main program do not introduce a data race and have, therefore, not be synchronized.

Because I use the syncStream declared on line 17 only once, a temporary object may be more appropriate. The following code snippet presents the modified call operator.

```
```cpp
void operator()() {
    for (int i= 1; i <= 3; ++i) {
        // begin work
        std::this_thread::sleep_for(std::chrono::milliseconds(200));
        // end work
        std::osyncstream(std::cout) << name << ": " << "Work " << i << " done !!!" 
                                    << '\n';
    }
}
```
```

std::basic_osyncstream syncStream offers two interesting member functions.

+   - syncStream.emit() emits all buffered output and executes all pending flushes.
+   - syncStream.get_wrapped() returns a pointer to the wrapped buffer.

cppreference.com²⁰ shows how you can sequence the output of different output streams with the get_wrapped member function.

²⁰https://en.cppreference.com/w/cpp/io/basic_osyncstream/get_wrapped