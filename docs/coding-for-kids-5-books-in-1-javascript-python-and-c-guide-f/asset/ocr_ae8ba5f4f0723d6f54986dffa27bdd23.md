# Infinite loops

Infinite loops occur when the condition that *for* loop or *while* loop checks in order to decide whether to run their associated block of code, is always **true**.
**So, it basically runs forever.**

# Example

```
```cpp
#include<iostream>
using namespace std;

int main(){

    while( true ){
        cout << "Hi from the infinite while loop"<< endl;
    }

    return 0;
}
```
```