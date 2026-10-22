```
```cpp
void multiply(void*);        // ordinary function

template<typename T>
void multiply(T);             // function template

class Comrades {
    friend void multiply(int) { }
                         // defines a new function ::multiply(int)

    friend void ::multiply(void*);
                         // refers to the ordinary function above,
                         // not to the multiply<void*> instance

    friend void ::multiply(int);
                         // refers to an instance of the template

    friend void ::multiply<double*>(double*);
                         // qualified names can also have angle brackets,
                         // but a template must be visible

    friend void ::error() { }
                         // ERROR: a qualified friend cannot be a definition
};
```
```