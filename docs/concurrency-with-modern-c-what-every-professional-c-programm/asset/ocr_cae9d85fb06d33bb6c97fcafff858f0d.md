I know from personal experience that both definitions might not be easy to digest. Here is a graphic to visualize them.

```
```cpp
std::atomic<std::string*> ptr;
int data;
std::atomic<int> atoData;

void producer() {
  std::string* p = new std::string("C++");
  data = 2011;
  atoData.store(2014,std::memory_order_relaxed);
  ptr.store(p, std::memory_order_release);
}

void consumer() {
  std::string* p2;
  while (!(p2 = ptr.load(std::memory_order_consume)));
  std::cout << "*p2: " << *p2 << std::endl;
  std::cout << "data: " << data << std::endl;
  std::cout << "atoData: " << atoData.load(std::memory_order_relaxed) << std::endl;
}
```
```

![](bbox=[0.39, 0.18, 0.92, 0.31])

Data dependencies of std::memory_order_consume

The expression ptr.store(p, std::memory_order_release) is dependency-ordered-before the expression while (!(p2 = ptr.load(std::memory_order_consume))), because the following line std::cout << "*p2: " << *p2 << '\n' is be read as the result of the load operation. Furthermore it holds that: while (!(p2 = ptr.load(std::memory_order_consume)) carries-a-dependency-to std::cout << "*p2: " << *p2 << '\n', because the output of *p2 uses the result of the ptr.load operation.

We have no guarantee regarding the output of data and atoData. That's because neither has a carries-a-dependency relation to the ptr.load operation. It gets even worse: since data is a non-atomic variable, there is a data race on the variable data. The reason is that both threads can access data at the same time, and thread t1 wants to modify data. Therefore the program has undefined behavior.

Finally, we have reached the relaxed semantic.

# 2.4.5 Relaxed Semantic

The relaxed semantic is the other end of the spectrum. The relaxed semantic is the weakest of all memory models and only guarantees the modification order of atomics. This means all modifications on an atomic happen in some particular total order.

# 2.4.5.1 No synchronization and ordering constraints

It is relatively easy. If there are no rules, we cannot violate them. However, that is too easy; the program should have well-defined behavior. Well-defined behavior means that you typically use synchronization and ordering constraints of stronger memory models to control operations with relaxed semantic. How does this work? A thread can see the effects of another thread in arbitrary order, so you have to make sure there are points in your program where all operations on all threads get synchronized.