```
void producer()
{
    for (int n = 0; n!=LOTS; ++n) {
        scoped_lock l {m}; // m is a mutex (§18.3)
        q.push_back(allocate_shared<Event,pmr::polymorphic_allocator<Event>>({&pool}));
        cv.notify_one();
    }
}
```