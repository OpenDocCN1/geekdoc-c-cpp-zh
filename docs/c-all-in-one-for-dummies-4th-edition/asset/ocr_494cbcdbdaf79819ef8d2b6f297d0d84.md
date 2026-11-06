# Seeing a simple example of function input

At times, a single number represents a base value, but you must manipulate it in various ways to achieve a result. For example, you might need to find the correct process to use to optimize a particular set of values using a base value as a starting point. The FunctionFunction example, shown in Listing 1–8, demonstrates how to use this technique.

# **LISTING 1-8:** Passing a Function to a Function

```
```cpp
#include <iostream>
#include <vector>

using namespace std;

int AddSome(int Value) {
    return Value + 10;
}

int DelSome(int Value) {
    return Value - 10;
}

int MulSome(int Value) {
    return Value * 10;
}

int DivSome(int Value) {
    return Value / 10;
}

typedef int(*FuncPtr)(int);

void ModIt(int Value, vector<FuncPtr> FuncArray) {
    int NumFunc = FuncArray.size();
    cout << "Processing " << NumFunc << " functions."
      << endl;

    for(int i = 0; i < NumFunc; i++)
        cout << FuncArray[i](Value) << endl;
}
```
```

*(continued)*