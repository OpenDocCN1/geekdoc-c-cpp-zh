calls the function `add()` and hence the control of execution will be transferred to the function definition of `add()` as shown in Figure 7.12. Remember, making a call to `add()` from `main()` is possible because we have already prototyped it before `main()`. The function definition of `add()` will now be executed which takes two numbers a and b as input from the user and prints the result of addition on the computer screen.

After execution of the function `add()` completes, the control will be returned back to `main()` at the next statement after the function call.

![](bbox=[0.163, 0.263, 0.84, 0.468])

**Figure 7.12:** Call to function `add()`

Hence, the statement

```
printf("Back from add\n");
```

will get executed thereby printing a message, “Back from add” on the computer screen.

Obviously, there is no need to prototype a function if it is defined before `main()`. This is because there is no forward referencing whatsoever as the full definition of the function itself appears before making the function call. In this case, compilers are smart enough to extract the prototype function from the function definition and hence the code in Figure 7.13 works absolutely fine without prototyping `add()`.

![](bbox=[0.18, 0.695, 0.824, 0.892])

```
#include<stdio.h>
void add()
{
    int a,b;
    printf("Enter the two numbers\n");
    scanf("%d%d",&a,&b);
    printf("Addition is %d\n", a+b);
}
void main()
{
    printf("Going to add\n");
    add();
    printf("Back from add\n");
}
```

**Figure 7.13:** Defining the function before `main()`