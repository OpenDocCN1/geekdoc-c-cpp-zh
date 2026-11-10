11.4 Examine the following code snippet and explain why `printf` prints different values in `main` and `func`:

```
int main(void)
{
    short arr[100];
    printf("Size of array = %hd\n", sizeof(arr));
    func(arr);
    return 0;
}
void func(short f_arr[])
{
    printf("Size of array = %hd\n", sizeof(f_arr));
    return;
}
```

11.5 How is passing the element `arr[5]` different from passing the name, `arr`, to a function? Explain whether the function can change the contents of `arr` defined in the caller.

11.6 Explain the circumstances that determine whether a variable is declared before `main`, inside `main` or after `main`.

11.7 Explain the concept of variable hiding using a suitable example.

# PROGRAMMING & DEBUGGING SKILLS

11.1 Identify the errors in the following program:

```
#include <stdio.h>
void func(void)
int main(void)
{
    func(void);
    return 0;
}
void func(void)
{
    printf("Elementary penguin\n");
    return;
}
```

11.2 Write a program containing a function named `volume` which returns the volume of a sphere. The function is passed the radius as a single argument.

11.3 Modify the preceding program in C11.2 so that the `volume` function handles a cube and a sphere. Incorporate `#define` statements that would enable the function to be invoked in the following two ways:

```
float radius, length, vol;
vol = volume(radius, SPHERE);
vol = volume(length, CUBE);
```