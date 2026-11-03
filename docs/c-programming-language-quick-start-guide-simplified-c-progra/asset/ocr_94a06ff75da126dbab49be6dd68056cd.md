body of invoked function. This means that each argument is evaluated, and its value is

used locally in its own environment. Thus, if a variable is passed to a function, the stored

value of that variable in the calling environment will not be changed because the calling

environment and called environment have their own copy of arguments.

Following is an example, demonstrating the concept of “call by value”:

```
```c
void changeValue(int a)
{

a = a + 10;

printf("Inside changeValue function: Value of a = %d\n", a);
}

void main(void)
{

int a = 10;

printf("Inside main function, before changeValue is called: Value of a = %d\n", a);

changeValue(a);

printf ("Inside main function, before after changeValue is called:
Value of a = %d\n", a);
```
```