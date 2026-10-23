This syntax is required when calling a member function through a pointer, as it explicitly specifies the object on which the member function should be invoked.

On the other hand, calling a member function directly doesn’t require the use of a pointer and follows the usual syntax for calling member functions:

```
```cpp
obj.myFunction();
```
```

The output of the program will be:

```
```
Hello from myFunction!
Hello from myFunction!
```
```

Both calls to myFunction() produce the same result, but one is made through a pointer to a member function ((obj.*functionPtr)()) and the other is made directly (obj.myFunction()). The difference in syntax is due to the need to explicitly specify the object when calling a member function through a pointer.