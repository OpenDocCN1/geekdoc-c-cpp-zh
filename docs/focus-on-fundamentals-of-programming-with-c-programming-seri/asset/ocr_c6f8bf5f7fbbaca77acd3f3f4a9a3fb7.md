# Static Storage Class

Static storage class allows us to control whether the local variables retain their values between function calls. A static variable within a function is a local variable that retains its values from previous calls to that function. They are created the first time that a function is called and are not destroyed when the function is exited.

For example:

```
void foo(void) {
    static int num = 0;
    ...
}
```

The value of num will be initialized to 0 only once when program execution begins. Here's a program to illustrate static and automatic variables:

```
// storage5.c
int main(void) {
    int i;
    for (i = 0; i < 5; ++i) {
        foo();
    }
}

void foo(void) {
    int autoVar = 0;
    static int staticVar = 0;

    printf("Automatic = %d Static = %d\n", autoVar, staticVar);
    ++autoVar;
    ++staticVar;
}
```

Output:

```
Automatic = 0   Static = 0
Automatic = 0   Static = 1
Automatic = 0   Static = 2
Automatic = 0   Static = 3
Automatic = 0   Static = 4
```