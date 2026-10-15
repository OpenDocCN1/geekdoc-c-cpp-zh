```
public int AddTwoNumbers(int a, int b)
{
    b += 10;
    int sum = a + b;
    return sum;
}
```

As the name gives away, we aren't passing a copy; instead, we're passing a reference to the original value, so the value that lives from where the method is invoked. No copy is made in this case. That has a big influence on the behavior. If we now make a change on the parameter value in the called method, the original will also be changed as well, since, indeed, we have passed a reference to it. For this to happen, we need to include the ref keyword, saying to C# that you want to pass by reference. So passing by reference is definitely intentional. You'll want to do this when the method actually should work on the original values. Notice I have now added the ref keyword, and I've added it in two places. In the method declaration I've now added the ref keyword before the int b. Our method can only still be called by passing in b by reference. When doing this, so when we call the method, we now also need to specify the ref keyword here. Executing the method, which does add 10 to the current value of b, will now have an effect on the value in the caller. Normally, a method can just return a single value. Using ref, it's also possible to let a method work on different values and change the original values of the parameters. One more thing, before the method is called, all ref parameters must be initialized. In the next demonstration, I'm going to show you the difference between calling by value and by ref. First we'll see that our default way of working