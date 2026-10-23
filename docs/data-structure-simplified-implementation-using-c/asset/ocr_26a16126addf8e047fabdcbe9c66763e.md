+   - Base condition
+   - Increment/decrement of call

# 14.2.1 Base condition

Base condition governs the number of times the function would call to itself, by specifying the condition where the loop terminates. It helps in preventing the infinite loop. Recursive functions are terminated by specifying the base condition. Syntax for the base condition appears as follows:

```
If(x==0)
return x;
```

The above condition is known as the base condition and permits to return from the function upon meeting the specified condition. In the given case, it is 0.

# 14.2.2 Incrementing/decrementing of function call

Since, recursive function, call itself and can be terminated once the base condition is reached. Consequently, there must be a statement that should leads towards the base condition. This base condition can be reached with the help of incrementing/decrementing the statement in the function call. For instance

```
print(x-1)
```

If the value of x is 8, and this value will be decremented by one in each call. Eventually, it will fulfill the condition given in the base condition. This type of statement that leads towards the base condition by decrementing the variable value are termed as decrementing function call. Consider the other call as

```
print(x+1)
```

In the above call, base condition can be reached by incrementing the value from the calling function.

Complete program using the base condition as well as incrementing/decrementing function call has been depicted as follows:

```
Program to print the number from 10 to 1
void print (int x)// value of x passed is 1
{
if(x! =10)  //base condition
{
cout<<"x="<<x;
print(x+1); // incrementing call
}
}
```