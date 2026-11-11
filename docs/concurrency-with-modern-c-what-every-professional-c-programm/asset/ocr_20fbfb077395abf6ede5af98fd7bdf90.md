```
```cpp

auto ex = pool.executor();

// One way, single.
ex.execute([] { std::cout << "We made it!" << '\n'; });

std::cout << '\n';

// Two way, single.
future<int> f1 = ex.two_way_execute([] { return 42; });
f1.wait();
std::cout << "The result is: " << f1.get() << '\n';

std::cout << '\n';

// One way, bulk.
ex.bulk_execute([](int n, int& sha){
    std::cout << "part " << n << ": " << "shared: " << sha << "\n";
}, 8,
   [] { return 0; }
);

std::cout << '\n';

// Two way, bulk, void result.
future<void> f2 = ex.bulk_twoway_execute(
    [](int n, std::atomic<short>& m){
        std::cout << "async part " << n;
        std::cout << " atom: " << m++ << '\n';
    }, 8,
    [] {},
    [] {
        std::atomic<short> atom(0);
        return std::ref(atom);
    }
);
f2.wait();
std::cout << "bulk result available" << '\n';

std::cout << '\n';

// Two way, bulk, non-void result.
future<double> f3 = ex.bulk_twoway_execute(
    [](int n, double, int &){
        std::cout << "async part " << n << '\n';
        std::cout << std::this_thread::get_id() << '\n';
```
```