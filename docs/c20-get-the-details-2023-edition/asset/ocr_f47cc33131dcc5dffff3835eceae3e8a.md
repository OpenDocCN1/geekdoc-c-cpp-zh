```
```cpp
    << std::this_thread::get_id() << '\n';
    return {};
}
void return_void() {}
void unhandled_exception() {}
};
};

Job performJob(std::jthread& out) {
    co_await MyAwaitable{out};
}

int main() {

    std::vector<std::jthread> threads(8);
    for (auto& thr : threads) performJob(thr);

}
```
```

The main difference with the previous program is the new awaitable MyAwaitable, used in the coroutine performJob (line 54). On the contrary, the coroutine object returned from the coroutine performJob is straightforward. Essentially, its member functions initial_suspend (line 38) and final_suspend (line 43) returns the predefined awaitable std::suspend_never. Additionally, both functions show the JobNumber of the executed job and the thread ID on which it runs. The screenshot shows which coroutine runs immediately and which one is suspended. Thanks to the thread id, you can observe that suspended coroutines are resumed on a different thread.

You can try out the program on the Wandbox^a.

^a <https://wandbox.org/permalink/kkHgWKF0SYAwp8Dm>