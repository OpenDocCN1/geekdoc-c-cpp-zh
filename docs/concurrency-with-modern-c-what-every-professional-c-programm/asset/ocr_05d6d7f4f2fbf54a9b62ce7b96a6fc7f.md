CppMem: atomics(acquire-release semantic

```
```cpp
int main(){
  atomic_int x = 0;
  atomic_int y = 0;
  {{{
    x.store(2000, memory_order_relaxed);
    y.store(11, memory_order_release);
  }
  ||| {
    y.load(memory_order_acquire);
    x.load(memory_order_relaxed);
  }
  }}}
}
```
```

We already know that all results are possible except for (y = 11, x = 0).

# ### 6.4.4.1.1 Possible executions

I only refer to the three graphs with consistent execution. The graphs show an acquire-release semantic between the store-release of y and the load-acquire operation of y. It makes no difference if the reading of y (*rf*) takes place in the main thread or a separate thread. The graphs also show the *synchronizes-with* relation using a *sw* annotated arrow.

# ### 6.4.4.1.2 Execution for (y = 0, x = 0)

![](bbox=[0.27, 0.65, 0.72, 0.89])