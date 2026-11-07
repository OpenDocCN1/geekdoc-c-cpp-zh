```
```cpp
};

};

// Type-erased container for callable objects

class AnyCallable {

std::unique_ptr callable;

public:

template<Func>

AnyCallable(Func f) : callable(new Callable(f)) {}

void call() const {

callable->call();

}

};
```
```