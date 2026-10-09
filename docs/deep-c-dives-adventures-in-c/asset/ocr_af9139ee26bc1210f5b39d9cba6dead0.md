The “export it” approach leaves the function to create the data structure and return a pointer to it:

```
int *myFunction(void){
   int *myArray = (int*) malloc(sizeof(int)*10);
   for(int i=0;i<10;i++){
      myArray[i]=i;
   }
   return myArray;
}
int *myArray = myFunction();
```

The advantage is that the function can decide how big a data structure is needed, but it has to pass this back to the calling function. The disadvantage is that the user of the function may not have any idea that it is responsible for freeing the data structure. It might even be that the function returns the same data structure on each call leaving multiple callees jointly responsible for the lifetime of the structure. In most cases the best alternative is to provide a management function to complement myFunction which will dispose of the structure and that can be called multiple times without causing an error.

# Returning More Than One Result

A C function can only return a single value and this can be a problem. If you need to return multiple values, a single value return may not seem up to the task – it is but it isn’t obvious.

A very common approach to the problem is to use parameters to return results. We have already seen that passing a pointer is effectively pass by reference and as such the function can change values in the calling program. Consider a function that needs to return a max and a min value. We could implement this as a function with two pointer parameters:

```
void maxmin(int *max, int *min){
   *max = 100;
   *min = 0;
}
int mymax;
int mymin;
maxmin(&mymax,&mymin);
```

As always, the problem is to remember to pass in the address of the variables being used for the results. Usually such functions are organized so that the “in” parameters are listed before any “out” parameters.