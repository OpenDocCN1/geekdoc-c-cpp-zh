You can see in the above program we are not allowed to access the variables a and b directly, however one can call the function sum() to set the values in a and b and the function display() to display the values of a and b.

# Advantages of Data Abstraction:

+   - Helps the user to avoid writing the low level code.
- Avoids code duplication and increases reusability.
- Can change internal implementation of class independently without affecting more than one user.
- Helps to increase security of an application or program as only important details are provided to the user.

# Polymorphism

The word polymorphism means having many forms. In simple words, we can define polymorphism as the ability of a message to be displayed in more one form.

A person at the same time can have different characteristic. Like a man at the same time is a father, a husband, an employee. So the same person possess different behaviour in different situations. This called polymorphism.

Example: Suppose we have to write a function to add some integers, some times there are 2 integers, some times there are 3 integers. We can write the Addition Method with the same name having different parameters, the concerned method will be called according to parameters.

```
int main () {
    sum1 = sum(20,30);
    sum2 = sum(20,30,40);
}
```
```

```
int sum(int a, int b, int c) {
    return (a+b+c);
}
```

An operation may exhibit different behaviours in different instances. The behaviour depends upon the types of data used in the operation.

+   - Polymorphism is extensively used in implementing inheritance.