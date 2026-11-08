```
```cpp
bool await_ready() const noexcept {
    std::cout << " MySuspendNever::await_ready " << '\\n';
    std::this_thread::sleep_for(sleepDuration);
    return true;
}
void await_suspend(std::coroutine_handle<>) const noexcept {
    std::cout << " MySuspendNever::await_suspend " << '\\n';
}
void await_resume() const noexcept {
    std::cout << " MySuspendNever::await_resume " << '\\n';
}
};

struct Job {
    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;
    handle_type coro;
    Job(handle_type h): coro(h){}
    ~Job() {
        if (coro) coro.destroy();
    }
    void start() {
        coro.resume();
    }
};

struct promise_type {
    auto get_return_object() {
        return Job{handle_type::from_promise(*this)};
    }
    std::suspend_always initial_suspend() {
        std::cout << " Job prepared" << '\\n';
        return {};
    }
    std::suspend_always final_suspend() noexcept {
        std::cout << " Job finished" << '\\n';
        return {};
    }
    void return_void() {}
    void unhandled_exception() {}

};

Job prepareJob() {
```
```