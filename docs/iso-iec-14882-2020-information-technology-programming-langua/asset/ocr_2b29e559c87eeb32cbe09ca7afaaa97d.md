```
template<class R, class... ArgTypes>
class packaged_task<R(ArgTypes...)> {
public:
    // construction and destruction
    packaged_task() noexcept;
    template<class F>
        explicit packaged_task(F&& f);
    ~packaged_task();

    // no copy
    packaged_task(const packaged_task&) = delete;
    packaged_task& operator=(const packaged_task&) = delete;

    // move support
    packaged_task(packaged_task&& rhs) noexcept;
    packaged_task& operator=(packaged_task&& rhs) noexcept;
    void swap(packaged_task& other) noexcept;

    bool valid() const noexcept;

    // result retrieval
    future<R> get_future();

    // execution
    void operator()(ArgTypes...);
    void make_ready_at_thread_exit(ArgTypes...);

    void reset();
};

template<class R, class... ArgTypes>
    void swap(packaged_task<R(ArgTypes...)>& x, packaged_task<R(ArgTypes...)>& y) noexcept;
```

# 32.9.10.2 Member functions [futures.task.members]

```
packaged_task() noexcept;
```

Effects: The object has no shared state and no stored task.

```
template<class F>
    packaged_task(F&& f);
```

Constraints: remove_cvref_t<F> is not the same type as packaged_task<R(ArgTypes...)>.

Mandates: is_invocable_r_v<R, F&, ArgTypes...> is true.

Preconditions: Invoking a copy of f behaves the same as invoking f.

Effects: Constructs a new packaged_task object with a shared state and initializes the object’s stored task with std::forward<F>(f).

Throws: Any exceptions thrown by the copy or move constructor of f, or bad_alloc if memory for the internal data structures cannot be allocated.

```
packaged_task(packaged_task&& rhs) noexcept;
```

Effects: Transfers ownership of rhs’s shared state to *this, leaving rhs with no shared state. Moves the stored task from rhs to *this.

Postconditions: rhs has no shared state.

```
packaged_task& operator=(packaged_task&& rhs) noexcept;
```

Effects:

+   - Releases any shared state (32.9.5);
+   - calls packaged_task(std::move(rhs)).swap(*this).