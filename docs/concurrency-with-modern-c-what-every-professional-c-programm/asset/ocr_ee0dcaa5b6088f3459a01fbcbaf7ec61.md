![](bbox=[0.263, 0.112, 0.737, 0.247])

In the following two variations using a local variable, only the function sumUp changes; therefore, I display the function. For the entire program, please refer to the source files.

# 6.1.3.1.2 Using an Atomic Variable with Sequential Consistency

Let’s replace the non-atomic global summation variable sum with an atomic.

# Summation of a vector with minimal synchronization and an atomic

```
```cpp
// LocalVariableAtomic.cpp

...

void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val,
           unsigned long long beg, unsigned long long end){
    unsigned int long long tmpSum=0;
    for (auto i = beg; i < end; ++i){
        tmpSum += val[i];
    }
    sum += tmpSum;
}

...
```
```

Here are the performance numbers.

![](bbox=[0.263, 0.716, 0.737, 0.865])