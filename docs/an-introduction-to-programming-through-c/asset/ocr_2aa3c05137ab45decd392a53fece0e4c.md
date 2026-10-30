main. After this the call will terminate. When the execution of main resumes, √2 and 0.785 would get printed by the last statement in main.

We next consider the swap function. It should be clear to you now what we should do: instead of using the variables as arguments, we should use their addresses. Here is the function.

```
void swap(int* pa, int* pb){
    int temp;
    temp = *pa;
    *pa = *pb;
    *pb = temp;
}
```

It may be called by a main program as follows.

```
int main{
    int x=5, y=6;
    swap(&x,&y);
    cout << x << ' ' << y << endl;
}
```

The arguments to the call are &x, &y, having type int*, because x,y are of type int. Thus they match the types of the parameters of the function. Thus our program will be compiled correctly.

So let us consider the execution. The address of x will be copied into pa, and the address of y into pb. Thus we may note that *pa in swap will really refer to the variable x of the main program, and *pb in swap will refer to the variable y of the main program. The statement temp = *pa; will cause the value of x to be copied to temp. In the next statement, the value of y is copied to x. The last statement causes the value in temp, i.e. the value in x at the beginning to be copied to y (which is what *pb denotes). The function call completes. The main program then resumes and will print the exchanged values, 6 and 5.

The changes required to the main program for mark averaging and the function read_marks_into are left as exercises.

# 9.8.5 Reference vs. Pointers

You have seen that there are two ways of writing the functions Cartesian_To_Polar, swap and read_marks_into. Which one is better?

Clearly, the functions are easier to write with call by reference. So that is clearly to be recommended in C++ programs.²

> ²You are probably wondering: when a function executes, and some parameter is a reference parameter, how does the computer know what variable the parameter refers to? A simple answer is: at the time of the call, C++ automatically sends the address of the variables referred to by the reference parameters to the function activation frame. Also, during the function execution, C++ itself dereferences the address of the reference variables, and gets to the variables as needed. So in other words, the operations of sending addresses and dereferencing them that had to be manually written out in C are performed “behind the scenes” by C++.