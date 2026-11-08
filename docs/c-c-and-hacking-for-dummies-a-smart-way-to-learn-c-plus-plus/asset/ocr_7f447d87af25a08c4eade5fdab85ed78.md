To look at Conditions, to give our program choice we will use a syntax like the following:

```
```text
if (and then we include our condition here)
{
    insert our program here for the program to work out
}
```
```

This is basically saying, “If this happens, then do this”. You should be familiar with the basic terms of IF, THEN, AND, OR which is basic mathematics and problem solving skills. However, it is within the brackets where we put our condition, where the program can choose whether or whether not it is going to execute that condition. For example, if we have the three variables of x,y and z, we will first need to declare their values to the program. However, to start including some operators into the equation, lets say that the variable “x” is greater than the variable “y”.

Our code would look like this:

```
```cpp
int x,y,z;

cin>>x;

cin>>y;

    if(x>y)
    {
            z = x+y;
            cout<<z;
    {
```
```

Once we declare the values of the variables of x and y, the program will determine if “x” is indeed greater than “y”. If the program finds this to be true, then the undeclared variable “z” will be declared as the sum of x and y and then give us the answer. However, if the program finds that x is not greater than our new variable of z, nothing will happen.

This is where we give our program choice of what it can do when faced with