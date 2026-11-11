of objects of the ArrayList object before the object goes out of scope.

```
```cpp
~ArrayList()
{
    delete [] p;
    cout<<"Array List Deleted"<<endl;
}
```
```

As discussed from the Section 12.7, the memory for the object L1, which is the object of the class ArrayList, will be allocated by the compiler as shown in Figure 12.28:

Further, the keyword new allocates a dynamic memory at the time of creating the object L1 using a dynamic constructor. The dynamic memory allocated is pointed by the pointer p, which is the member of the object L1 as shown in Figure 12.29.

![](bbox=[0.653, 0.107, 0.879, 0.291])

When the object goes out of scope, which is when the main() function completes its execution, the static memory for the object L1 will be destroyed; however it is possible that the dynamic memory allocated for the array is still present in the heap space. Note that the dynamic memory is actually allocated by the programmer at runtime of the program, and hence the system will not be able to delete it automatically even if the object L1 goes out of scope. Therefore, the dynamic array created would unnecessarily occupy the heap space as shown in the Figure 12.30.

![](bbox=[0.423, 0.344, 0.881, 0.567])

Hence, it is a good programming practice to delete all the resources held by the object before the object goes out of scope. To do this, we can write destructor as a member function in the class. Note that we need not worry about calling a destructor explicitly; this is because C++ will automatically call it before a particular object goes out of scope. Hence, when we write the statement

![](bbox=[0.599, 0.743, 0.879, 0.912])

```
```cpp
delete [] p;
```
```

inside the destructor, we are sure that the dynamic array created for a particular object will always get deleted before that object is destroyed. Therefore, this will help in optimum utilization of the available heap space.