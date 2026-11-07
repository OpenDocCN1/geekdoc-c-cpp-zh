```
```cpp
try {
    std::string ret{"vote"};
    ...
    // store result:
    p.set_value_at_thread_exit(std::move(ret));
}
catch(...) {
    // store exception:
    p.set_exception_at_thread_exit(std::current_exception());
}
}

int main()
{
    std::vector<std::future<std::string>> results;

    // create promise and future to deal with outcome of the thread started:
    std::promise<std::string> p;
    std::future<std::string> f{p.get_future()};
    results.push_back(std::move(f));

    // start thread and move the promise to it:
    std::thread t{getValue, move(p)};
    t.detach();  // would not be necessary for std::jthread
    ...

    // wait for all threads to end:
    for (auto& fut : results) {
        std::cout << fut.get() << '\n';
    }
}
```
```

Here, in `main()`, we first create a promise to be able to send an outcome (value or exception) to the associated future that can read it:

```
```cpp
std::promise<std::string> p;
std::future<std::string> f{p.get_future()};
```
```

The future is moved into a collection of handles for futures:

```
```cpp
results.push_back(std::move(f));
```
```

We could also pass the result of `p.get_future()` directly to `push_back()`:

```
```cpp
results.push_back(p.get_future());
```
```

The promise is moved to the thread started:

```
```cpp
std::thread t{getValue, move(p)};
```
```