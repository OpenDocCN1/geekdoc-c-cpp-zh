# Solving the factorial with the while loop:

```
```cpp
int factorial(int n)
{
   int nFact = 1;
   while (n > 0)
   {
      nFact *= n--;
   }
   return(nFact);
}
```
```

# Solving the factorial using a recursive function:

```
```cpp
int factorial(int n)
{
   int nFact = 1;
   if(n > 1)
   {
      nFact = n * factorial(n - 1);
   }
   return(nFact);
}
```
```

Trace the execution of the recursive solution when the value 4 is passed to the factorial function. List the value of the variables in each call. Note the progression of the control of the program as the recursive function calls are made.

```
```cpp
int factorial(int n)
{
   int nFact = 1;
   if(n > 1)
   {
      nFact = n * factorial(n - 1);
   }
   return(nFact);
}
```
```

```
```cpp
int factorial(int n)
{
   int nFact = 1;
   if(n > 1)
   {
      nFact = n * factorial(n - 1);
   }
   return(nFact);
}
```
```

```
```cpp
int factorial(int n)
{
   int nFact = 1;
   if(n > 1)
   {
      nFact = n * factorial(n - 1);
   }
   return(nFact);
}
```
```

```
```cpp
int factorial(int n)
{
   int nFact = 1;
   if(n > 1)
   {
      nFact = n * factorial(n - 1);
   }
   return(nFact);
}
```
```