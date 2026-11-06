```
```cpp
int main()
{
    vector<int> MyVector;
    MyVector.push_back(1);
    MyVector.push_back(2);
    MyVector.push_back(3);
    MyVector.push_back(4);

    ProcessVector(MyVector);
}
```
```

![](bbox=[0.121, 0.279, 0.205, 0.349])

The essential code, application flow, and output are the same as ReturnType01. However, notice that this example changes the lambda expression to include a return type. Whenever you want to define a return type for a lambda expression, add the arrow operator and the return type, which is bool in this case.

![](bbox=[0.121, 0.378, 0.207, 0.45])

There are other reasons to use a specific return type. In some cases, providing a specific return type allows the compiler to better optimize your code so that you obtain better performance from your application. Using this approach can be quite helpful when you suspect your lambda expression is going to be processing a considerable amount of data. In this case, you won’t see any difference in application speed between ReturnType01 and ReturnType02 because the data set is so small.

# Using the auto keyword

The auto keyword is a new feature, added since C++ 11. What this keyword does is provide a shortcut method for defining the type of a variable, no matter what the variable may ultimately contain. Essentially, you use the auto keyword to save typing time — rather than type the full text of a lambda expression each time you need it, you simply type the name of the variable that contains the lambda expression.

![](bbox=[0.121, 0.66, 0.207, 0.732])

When you use the auto keyword, you’re asking the compiler to determine the type of a variable based on how that variable is used. This means that it must be possible to determine the type of the variable by examining the context in which it is used. When you use the auto keyword, these outcomes are possible:

+   - The compiler will determine the type automatically and assign it to the variable.
+   - The variable will receive a correct type, but not the type that you had originally envisioned (such as assigning a long where an int might serve better).