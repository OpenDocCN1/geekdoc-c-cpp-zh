```
vector<future<bool>> > futures;
for (long i = 0; i < num_threads; ++i) {
    ptask<bool, long> pt{is_prime};
    futures.push_back(pt.get_future());
    thread t{move(pt), vi[i]};
    t.detach();
}
```