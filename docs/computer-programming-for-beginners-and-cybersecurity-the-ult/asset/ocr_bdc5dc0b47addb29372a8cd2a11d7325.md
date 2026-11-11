destroyed when a function exits. These variables are also known as local variables.

```
```c
auto int value;
```
```

Is the same as

```
```c
int value;
```
```

# Static variables

Static is used when you want to keep the variable from being destroyed when it goes out of scope; this variable will persist until the program is complete. The static variable is created only once throughout the lifetime of the program. Below is an example of a static variable in use:

```
```c
void tick()
{
//This will run once
static int count = 0;
count++;
printf("The count is now: %d\n", count);
}
int main()
{
tick();
tick();
tick();
}
```
```

Output: