In order to appreciate the various nuances of dynamic polymorphism, let us first look at a function (shown in Listing 6.5) that returns the sum of factorials of the numbers that belong to a range whose limits are passed to it. The function may have the following definition.

# Listing 6.5 Function to compute sum of factorials

```
long int factorialSum(unsigned int a, unsigned int b)
{
    int i;
    long int sum;
    for(sum=0,i=a;i<b;i++)
        sum+=factorial(i);
    return sum;
}
```

In, factorial() is a function that returns the factorial of the parameter passed to it. Similarly, the function in Listing 6.6 returns the sum of cubes of the numbers that belong to the range whose limits are passed to it.

# Listing 6.6 Function to compute sum of cubes

```
long int cubeSum(unsigned int a, unsigned int b)
{
    int i;
    long int sum;
    for(sum=0,i=a;i<b;i++)
        sum+=cube(i);
    return sum;
}
```

The cube() function returns the cube of the number passed as a parameter to it. Again, the function of Listing 6.7 returns the sum of logarithms of the numbers that belong to the range whose limits are passed to it.

# Listing 6.7 Function to compute sum of logarithms

```
long int logSum(unsigned int a, unsigned int b)
{
    int i;
    long int sum;
    for(sum=0,i=a;i<b;i++)
        sum+=log(i);
    return sum;
}
```

The log() function returns the logarithm of the number passed as a parameter to it. A close look at the definitions of these functions reveals that the definitions of the functions are exactly the same for the name of the inner function they call all. Nevertheless, the similarity in their definitions is striking. It is not entirely unreasonable on our part to expect that there be some means of replacing these functions by a single function. We want to make a generic function that will replace all the above functions. For this, we have to specify a function pointer as an additional formal argument in the function. See Listing 6.8.