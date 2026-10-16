don’t want to change the argument variable? Is there a way to take advantage of the efficiency of passing by reference while protecting an argument variable’s integrity? Yes, there is. The answer is to pass a constant reference.

# Hint

> In general, you should avoid changing an argument variable. Try to write functions that send back new information to the calling code through a return value.

# Declaring Parameters as Constant References

The function display() shows the contents of the hero’s inventory. In the function’s header I specify one parameter—a constant reference to a vector of string objects named vec.

```
void display(const vector<string>& vec)
```

A constant reference is a restricted reference. It acts like any other reference, except you can’t use it to change the value to which it refers. To create a constant reference, simply put the keyword const before the type in the reference declaration.

What does this all mean for the function display()? Because the parameter vec is a constant reference, it means display() can’t change vec. In turn, this means that inventory is safe; it can’t be changed by display(). In general, you can efficiently pass an argument to a function as a constant reference so it’s accessible, but not changeable. It’s like providing the function read-only access to the argument. Although constant references are very useful for specifying function parameters, you can use them anywhere in your program.

# Hint

> A constant reference comes in handy in another way. If you need to assign a constant value to a reference, you have to assign it to a constant reference. (A non-constant reference won’t do.)

# Passing a Constant Reference

Back in main(), I create inventory and then call display() with the following line, which passes the vector as a constant reference.

```
display(inventory);
```