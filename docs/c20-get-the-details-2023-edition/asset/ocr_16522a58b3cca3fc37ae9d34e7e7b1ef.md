```
```cpp
void return_void() { }
void unhandled_exception() { }

};
};

Job prepareJob() {
    co_await MySuspendNever();
}

int main() {

    std::cout << "Before job" << '\n';

    auto job = prepareJob();
    job.start();

    std::cout << "After job" << '\n';
}
```
```

First of all, I replaced the predefined awaitables `std::suspend_always` and `std::suspend_never` with awaitables MySuspendAlways (line 6) and MySuspendNever (line 20). I use them in lines 51, 55, and 66. The awaitables mimic the behavior of the predefined awaitables but additionally write a comment. Due to the use of `std::cout`, the member functions await_ready, await_suspend, and await_resume cannot be declared as constexpr.

The screenshot of the program execution shows the control flow nicely, which you can directly observe on the [Compiler Explorer].

⁷https://godbolt.org/z/T5rcE4