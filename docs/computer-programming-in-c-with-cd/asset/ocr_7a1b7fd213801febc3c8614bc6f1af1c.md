In Listing 14, the value of `num1` and `num2` variables, after execution of the `swap()` function, remains unchanged because when the `swap()` function is called, the copy of `num1` and `num2` are passed to the variables, `a` and `b`. The changes that are made to the values of `a` and `b` variables inside the `swap()` function are actually made to the copy of `num1` and `num2` variables. No changes have been made to the actual `num1` and `num2` variables. Therefore, after calling the `swap()` function, the value of `num1` and `num2` remains unchanged.

The second technique of passing argument to a function is call by reference. In this technique, you can pass arguments to a function in two ways: using pointers and using references. In both ways, the actual original object is passed into the function, and not a copy is created within the scope of the function. When you pass arguments to a function using pointer, you use the `*` operator; while using a reference, you use the `&` operator. Using the `&` operator, the address of variable is passed to a function. For example, the following code snippet shows passing of arguments to the `swap()` function by reference:

```
```cpp
int main()
{
    void swap(int & , int &);
    int num1=40, num2 = 60;
    cout<<"Main: Before Swap num1 = "<<num1<<" and num2 = "<<num2<<endl;
    swap(num1, num2);
    cout<<"Main: After Swap num1 = "<<num1<<" and num2 = "<<num2<<endl;
    return 0;
}
void swap(int &a, int &b)
{
    cout<<"Swap: Before Swap a = "<<a<<" and b = "<<b<<endl;
    int c;
    c = a;
    a = b;
    b = c;
    cout<<"Swap: After Swap a = "<<a<<" and b = "<<b<<endl;
}
```
```

In the preceding code snippet, the `swap()` function is called by reference. When the `swap()` function is called, it does not create new variables called `a` and `b`, instead the variable `a` and `b` refers to the memory location of variables `num1` and `num2`. Now, any changes made by the `swap()` function are actually made to the memory address of the `num1` and `num2` variables. Therefore, these changes are made to the actual `num1` and `num2` variables.

As we have said, another way to pass arguments to a function is using the `*` operator. The function definition of the `swap()` function is:

```
```cpp
void swap(int *a, int *b)
```
```