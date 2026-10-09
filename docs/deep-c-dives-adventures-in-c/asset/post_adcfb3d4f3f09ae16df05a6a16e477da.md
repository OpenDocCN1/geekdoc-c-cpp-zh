
Most modern languages use the stack and the stack frame to store the return address, all the local variables and the functions' parameters. That is, when you call a function, the arguments you supply are usually pushed onto the stack to be retrieved and used by the function you call. In the same way, it is usual for any of the function's results to be pushed onto the stack as the function comes to an end so that the calling function can retrieve it.

Function call and return really fit neatly into the way a stack operates.

## Dead Data

The operation of the stack during function calls and returns is fairly clear now, but there is a potential problem. For example, if function A calls function B then there are two stack frames on the stack. If function B then calls function C another frame is pushed onto the stack. If function C returns, using the return address stored in its stack frame then the stack pointer is set to the start of the stack frame for function B.

![](img/5f2ea21c2077d473344a0fdf144677b9_99_0.png)

If you follow this idea you can see that it results in a perfectly natural way to implement functions, including their return addresses and automatic local variables.

Notice that in the diagram the data that function C used is still stored on the stack because it isn't accessible using standard stack operations. What this means is that it is possible to arrange to access a function's local data after it has returned!

For example:

```c
#include <stdio.h>
#include <stdlib.h>

int *funA(void)
{
    int c = 42;
    return &c;
}

int main(int argc, char **argv)
{
    int *result = funA();
    printf("%d\n", *result);
    return (EXIT_SUCCESS);
}
```

In this program funA creates a local variable c and stores 42 in it. It then returns the address of c and the main program uses this to print the value stored in c. In most cases this program will cause the compiler or the IDE to flag the potential error:

![](img/5f2ea21c2077d473344a0fdf144677b9_100_0.png)

The warning message is perfectly correct in that c is a local variable and hence only “lives” while the function is executing, and as such you should not return its address. However, if you run the program there is a good chance you will see 42 printed because the stack where the value of c was stored hasn’t changed. On some systems you will see a runtime error because the stack has changed enough to cause a memory fault. If another function is called after funA and before the value of c is printed then the chances are that you will not see 42, but some other value as stored on the stack by the other function.

This may seem like a contrived example, it is, but it is a far more common error than you might imagine as we will discover in Dive 13: First Class Functions.

The important point is that once a function returns you have to regard all of its local variables and everything it stored on the stack as being destroyed, even though they may hang around for a while simply because some other function hasn’t made use of the memory as yet.

## Blocks

So far we have focused on functions, but C is a block-structured language and functions are just one example of a block. The basic idea is that a block is a collection of instructions contained by curly brackets.

{statement1;statement2; …}.

This is often called a compound instruction to emphasize that it behaves as if the list of instructions it contains acts like a single big instruction. For example, the C flow of control statements like if are only defined for a single instruction:

if(condition) statement;

and the statement is obeyed only if the condition is true. If you want to execute multiple statements then you need to use a block:

if(condition) {statement1;statement2; ...}

This much all C programmers know, but a block is more than just a compound statement. A block acts like a function in the way it deals with the stack. That is, when you enter a block, any new local variables are added to the stack frame and when you leave the block they are lost. Another way to think of this is that a block is like a function, but without parameters and a return. Or you could say it the other way round - a function is a block with parameters and a return.

For example:

```c
int main(int argc, char **argv)
{
    int a = 42;
    {
        int c = 43;
        printf("%d    %d\n", a, c);
    }
    printf("%d\n", a);
    return (EXIT_SUCCESS);
}
```

In this case the block introduces the new variable c and this is only accessible within the block. If you try to use c outside of the block then the compiler will signal an error that you are trying to use an undefined variable. Before C99 all of the declarations in a block had to be at the start of the block, but now they can be anywhere. Notice that a is accessible inside the block this is usually called lexical or static scope.

If you know JavaScript, also notice that C does not implement hoisting for variable declarations. In JavaScript all declarations are moved to the start of a block, but in C the variable only exists after it has been declared.

Things are a little more subtle than this. If the variable is already defined outside of a block then any redefinition inside the block “shadows” the original variable, which is unavailable until the block is exited.

For example:

```c
int main(int argc, char **argv)
{
    int c = 42;
    {
        int c = 43;
        printf("%d\n", c);
    }
    printf("%d\n", c);
    return (EXIT_SUCCESS);
}
```

You will see 43 printed then 42 as the two different incarnations of c come into scope. As C variables of the same name but different type are regarded as the same variable it doesn't matter if you declare the inner variable to be of a different type:

```c
int main(int argc, char **argv)
{
    int c = 42;
    {
        float c = 43;
        printf("%f\n", c);
    }
    printf("%d\n", c);
    return (EXIT_SUCCESS);
}
```

In this case the inner block's c still shadows the containing block's c even though they are different types.

Notice that you can nest one block inside another. When you do, the variables declared in an inner block are local to that inner block, which can still access variables declared in any containing block. Any variables that you declare within the block that have the same name as variables in the containing block shadow the containing block variables even if they differ in type.

Why might blocks be useful? In fact you make use of them all of the time, perhaps without realizing. For example, as already mentioned, all of the C control statements make use of compound instructions and as such each is a block:

```c
for(int i = 0; i < 10; i++){
    int c = 0;
    c = c+i;
    printf("%d\n", c);
}
```

In this case c is local to the block and cannot be accessed outside of the for loop. In addition if there is a c already defined before the for loop then it is unchanged after the for loop ends. Notice the i is also local to the block as C99 now allows declarations within code and the for is regarded as being within the block.

The same behavior is the case for all of the control statements if, switch, while, for and do-while. Any variables declared between curly brackets are local to the block and go out of scope when the block is exited.

Within control statements, the local scope of variables to the containing block is useful as it can allow the reuse of variable names. Occasionally it is useful to create a block that isn't part of a control statement within a program for exactly that reason. For example, if you have a section of code that is giving problems you can run it with slight variations by copying it and pasting it back into the program and surrounding it with curly brackets to be sure that it has no effect on other variables already in the program.

## Final Word

The way that the stack works in exactly the way that fits with function call and return is pleasing. The way that it makes automatic local variables easy and natural is very surprising and not to make use of it would be to "look a gift horse in the mouth" – it is why local variables behave in the way that they do.

C takes this idea one stage further and allows you to declare blocks that are not functions. This is such a natural part of C programming you quickly forget that it is special and yet knowing exactly what is going on means you can be creative. If you are creative with blocks, remember to include some comments explaining what you are up to – share the creativity.
