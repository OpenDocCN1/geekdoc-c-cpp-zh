```
void f();                                // function
struct F {                             // function object
    void operator()();                     // F's call operator (§7.3.2)
};

void user()
{
    thread t1 {f};                        // f() executes in separate thread
    thread t2 {F()};                      // F()() executes in separate thread

    t1.join();                             // wait for t1
    t2.join();                             // wait for t2
}
```