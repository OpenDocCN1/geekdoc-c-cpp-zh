# ### Multi threaded summation with an atomic

```
```cpp
...
void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val,
           unsigned long long beg, unsigned long long end){
    for (auto it = beg; it < end; ++it){
        sum.fetch_add(val[it]);
    }
}
...
```
```

And I got my performance improvement by calculating the partial sums locally.

# ### Multi threaded summation with local variables

```
```cpp
...
void sumUp(unsigned long long& sum, const std::vector<int>& val,
           unsigned long long beg, unsigned long long end){
    unsigned long long tmpSum{};
    for (auto i = beg; i < end; ++i){
        tmpSum += val[i];
    }
    std::lock_guard<std::mutex> lockGuard(myMutex);
    sum += tmpSum;
}
...
```
```

The performance numbers are quite impressive and give a clear indication. The less you share state, the more you get out of your cores.

Performance of the various summations on Linux

| Single threaded | std::lock_guard | Atomics | Local summation |
| --- | --- | --- | --- |
| 0.07 sec | 3.34 sec | 1.34 sec | 0.03 sec |