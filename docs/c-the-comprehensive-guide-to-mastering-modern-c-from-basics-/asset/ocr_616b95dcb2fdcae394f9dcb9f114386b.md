# 20.4 Heap Memory and Stack Memory

It's a great thing that in C++ you can rely on objects being cleaned up at a well-defined time and the associated resources being released. You know that an object created in a function is automatically removed upon exit:

```
int calculate(int param) {
    vector<int> data{/*...*/};
    //
    return result;
}
```

At the end of calculate(), data is automatically removed, no matter what you did with it in the function. The functionality is quite simple: The computer literally manages a stack, on which it always places the variables you define. The compiler keeps track of the positions in the stack where a range was entered—example, with an opening block brace {. Upon leaving