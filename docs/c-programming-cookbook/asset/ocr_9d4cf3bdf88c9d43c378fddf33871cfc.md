```
~~~cpp
int main() {

    PushOperation push;

    PullOperation pull;

    performOperation(push); // Outputs: Performing a 'push' operation.

    performOperation(pull); // Outputs: Performing a 'pull' operation.

    return 0;

}
~~~
```

In this setup, performOperation can accept any object of a class derived from GitOperation and call its execute method, demonstrating polymorphism in action. This design allows for new git operations to be added with minimal changes to the existing code, showcasing the power of abstract classes (interfaces) in creating flexible and maintainable software architectures.

# ## Key Takeaway