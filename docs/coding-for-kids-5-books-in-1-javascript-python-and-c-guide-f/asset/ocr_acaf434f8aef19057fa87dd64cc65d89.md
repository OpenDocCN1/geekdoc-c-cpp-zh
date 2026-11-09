# # Accessing struct member values

To access a structure's member variables value, you use the dot operator as shown below

# ## Example code

```
```cpp
#include<iostream>
using namespace std;

struct PersonInfo{

    int age;
    int Weight;
    int Height;
};

int main(){

    // initializing the structure
    PersonInfo kevin = {20,50,1};
    PersonInfo jessica = {15,29,1};

    cout << kevin.age << endl;
    cout << jessica.age << endl;

    return 0;
}
```
```