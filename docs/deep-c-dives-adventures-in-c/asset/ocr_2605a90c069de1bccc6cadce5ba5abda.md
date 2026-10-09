The methods are declared as standard functions:

```
```c
void Sort(struct MyClass *self)
{
    printf("sort called\n");
}
void Display(struct MyClass *self)
{
    for (int i = 0; i < 10; i++)
    {
        printf("%d\n", self->data[i]);
    }
}
```
```

To make use of this we need to create an instance of the class:

```
```c
int main(int argc, char **argv)
{
    struct MyClass myObject = {0,1,2,3,4,5,6,7,8,9},
                          &Sort, &Display};
    myObject.sort(&myObject);
    myObject.display(&myObject);;
}
```
```

This sets up an instance of the struct and initializes it so that it has an array to sort and two functions to do the jobs. The functions can be called in the usual way, but notice that they are functions as we have to pass a pointer to the instance of the struct as the first parameter. There is no way that the functions can “work out” which instance of the struct to sort or in the jargon the functions are not automatically bound to the instance they operate on.

In C functions cannot be “attached” to a struct in such a way that the function “knows” which struct it was called by. To do so we would need to generate a new “bound” function, i.e. a method by partial application that eliminated self from the function call but provided it automatically, see Dive 13 and partial application.

It can be done, as C is so low-level anything can be done, but only by knowing how the function call and return is implemented and this is highly machine-dependent.