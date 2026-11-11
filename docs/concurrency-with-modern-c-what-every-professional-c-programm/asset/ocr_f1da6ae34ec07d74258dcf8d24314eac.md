# # Erroneous Busy Waiting with Resource Hierarchy

```
```cpp
// dp_4.cpp

...

int main() {
    std::cout << "dp_4\n";
    srand(time(nullptr));

    int m1{0}, m2{0}, m3{0}, m4{0};

    std::thread t1{[&] {phil(1, m1, m2);}};
    std::thread t2{[&] {phil(2, m2, m3);}};
    std::thread t3{[&] {phil(3, m3, m4);}};
    std::thread t4{[&] {phil(4, m4, m1);}};

    t1.join();
    t2.join();
    t3.join();
    t4.join();
}

...
```
```

Program version 4 output looks fine: