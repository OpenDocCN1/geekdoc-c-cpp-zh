```
private:
    int myMember;
};

int main() {
    MyClass obj(5);
    obj.doOperation();

    return 0;
}
```

In this example, we have a class called MyClass with a member variable myMember. Inside the doOperation member function, we define a lambda function called lambda. The lambda function captures the member variable myMember through the capture list [this] and captures the local variable multiplier by reference using the capture list &multiplier.

By capturing myMember through [this], the lambda function gains access to the myMember variable of the class instance it is called from. The [this] capture list captures all non-static member variables of the class by value.

By capturing multiplier by reference through &multiplier, the lambda function can access and modify the multiplier variable defined within the doOperation function.

Inside the lambda function, we multiply myMember by multiplier and output the updated value. Then, we output the value of myMember again after the lambda function has been called.

When we execute the program, the output will be:

```
Inside lambda: myMember = 10
After lambda: myMember = 10
```