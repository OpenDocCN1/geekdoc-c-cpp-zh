```
Stack<std::string> stringStack;   // stack of strings
Stack<float>      floatStack;   // stack of floats
...
floatStack = stringStack;        // ERROR: std::string doesn't convert to float
```