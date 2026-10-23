# 14.4.3 Non-tail recursion

In the non-tail recursion, one or more statements exist after the recursive call. Consequently, all the statements after the recursive call will execute depending upon the calls made by the recursive function. For instance, if the recursive call has been executed four times then the statement following the recursive function will be executed four times. Example of non-tail function has been depicted below:

```
//program of non-tail recursion
void nontail1 (int x)  // value of x passed is 5
{
if(x!=0)
nontail1(x-1);
cout<<"x="<<x<<"\t";
}
Output for x=5:  0      1      2      3      4      5
```

From the above function, it is apparent that the recursive call is stored in the stack. Consequently, they are popped one by one till stack is not empty. Consider the other example of non-tail recursive function with the return type available at the end.

```
//Non-tail recursion with return statement
int nontail (int x)
{
if(x!=0)  // if x is not zero
nontail(x-1);     // continue to call non-tail function
return x;  // Eventually, return x
}
Output: 5 will be returned to the caller
```

It is extremely important to understand that we can use the return statement for returning the value. For instance, in the above program all the values from '0' to '5' will be returned to the caller. However, the one that is returned last will be available for access. Since, other values are overlapped. Similarly, the above function will return 7, if the argument is passed as 7.

# 14.4.4 Mutual recursion

In the mutual recursion, two different functions are calling each other to ensure that recursion takes place. Here one function func1 () calls to another function func2 (). Whereas, function func2 () will call the function func1 (). This calling will continue till the base condition of the calling function is not reached. To display the number from 'n' to 1, mutual function has been depicted in the following example.