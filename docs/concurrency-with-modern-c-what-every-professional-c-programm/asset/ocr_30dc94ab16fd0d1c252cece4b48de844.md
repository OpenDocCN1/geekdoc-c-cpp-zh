```
~~~cpp
18  private
19      MySingleton() = default;
20      ~MySingleton() = default;
21      MySingleton(const MySingleton&) = delete;
22      MySingleton& operator=(const MySingleton&) = delete;
23
24      static MySingleton* instance;
25      static std::once_flag initInstanceFlag;
26
27      static void initSingleton() {
28          instance= new MySingleton;
29      }
30  };
31
32  MySingleton* MySingleton::instance = nullptr;
33  std::once_flag MySingleton::initInstanceFlag;
34
35  ...
~~~
```

Here are the performance numbers.

![](bbox=[0.23, 0.5, 0.77, 0.61])

![](bbox=[0.26, 0.62, 0.74, 0.73])

Let's continue our thread-safe singleton implementation using atomics.

# ### 6.3.6 Atomics

With atomic variables, my implementation becomes a lot more challenging. I can even specify the *memory-ordering* for my atomic operations. The following two implementations of the thread-safe singletons are based on the previously mentioned **double-checked locking pattern**.