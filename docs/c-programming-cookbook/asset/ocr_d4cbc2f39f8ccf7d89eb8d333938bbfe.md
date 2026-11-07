# # Implementing Derived Classes

To use our abstract class, we derive concrete classes from it and implement the pure virtual functions. This allows different types of git operations to be executed polymorphically.

```
```cpp
class PushOperation : public GitOperation {

public:

void execute() const override {

std::cout << "Performing a 'push' operation." << std::endl;

}

};

class PullOperation : public GitOperation {

public:

void execute() const override {
```
```