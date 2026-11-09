# Exercise

Retrieve the fourth element. (Hint the index is not 4)

# Looding through elements in an array

If we want to retrieve all the elements in an array, we can use loops to do that.
We will use *for* loop since it is the simplest way to go about it.

# Example

```
```cpp
#include<iostream>
using namespace std;

int main(){
    int size[4] = { 1,2,3,4};

    for(int i = 0 ; i < 4; i++){
        cout << size[i] ;
    }
    return 0;
}
```
```