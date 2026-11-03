will be executed with n = 3. That is,

```
fact = 3 * factorial(2);
```

will be evaluated. The expression on the right-hand side includes a call to factorial with n = 2. This call will return the following value:

```
2 * factorial(1)
```

Once again, factorial is called with n = 1. This time, the function returns 1. The sequence of operations can be summarized as follows:

```
fact = 3 * factorial(2)
= 3 * 2 * factorial(1)
= 3 * 2 * 1
= 6
```

Recursive functions can be effectively used to solve problems where the solution is expressed in terms of successively applying the same solution to subsets of the problem. When we write recursive functions, we must have an if statement somewhere to force the function to return without the recursive call being executed. Otherwise, the function will never return.

# 10.14 FUNCTIONS WITH ARRAYS

Like the values of simple variables, it is also possible to pass the values of an array to a function. To pass an array to a called function, it is sufficient to list the name of the array, without any subscripts, and the size of the array as arguments. For example, the call

```
largest(a,n);
```

will pass all the elements contained in the array a of size n. The called function expecting this call must be appropriately defined. The largest function header might look like:

```
float largest(array, size)
float array[];
int size;
```

The function largest is defined to take two arguments, the array name and the size of the array to specify the number of elements in the array. The declaration of the formal argument array is made as follows:

```
float array[];
```

The pair of brackets informs the compiler that the argument array is an array of numbers. It is not necessary to specify the size of the array here.

Let us consider a problem of finding the largest value in an array of elements. The program is as follows:

```
main()
{
    float largest();
    static float value[4] = {2.5, -4.75, 1.2, 3.67};
```