# 9.1 Dealing with Sharing

If you don’t share, no data races can happen. Not sharing means that your thread works on local variables. This can be achieved by copying the value, by using thread-specific storage, or by transferring the result of a thread to its associated future via a protected data channel. The patterns in this section are quite obvious, but for completeness, I will present them with a short explanation.

# 9.1.1 Copied Value

If a thread gets its arguments by copy and not by reference, there is no need to synchronize access to any data. No data races and no lifetime issues are possible.

# 9.1.1.1 Data Races with References

The following program creates three threads. One thread gets its argument by copy, the other by reference, and the last by constant reference.

```
Data races with references

```cpp
// copiedValueDataRace.cpp

#include <functional>
#include <iostream>
#include <string>
#include <thread>

using namespace std::chrono_literals;

void byCopy(bool& b){
    std::this_thread::sleep_for(1ms);
    std::cout << "byCopy: " << b << '\n';
}

void byReference(bool& b){
    std::this_thread::sleep_for(1ms);
    std::cout << "byReference: " << b << '\n';
}

void byConstReference(const bool& b){
    std::this_thread::sleep_for(1ms);
    std::cout << "byConstReference: " << b << '\n';
}

int main(){
```

```