returned from longjmp
// main() returns 1

jmp_buf is an opaque struct that will hold the execution context of the program.
setjmp(env) saves the execution context of the program in env. setjmp always returns 0.
The execution context that is saved is the state of the program after setjmp() is executed before the return value 0 is assigned to ret.

The program now executes the setjmp, evaluates ret == 0 and continues running. It then calls the jumper function with the env argument. Inside jumper, longjmp(env, retvalue) restores the program’s execution context. The longjmp will return. If this argument is 0 then longjmp will return 1. Now it evaluates ret == 0 again and continues running.

Note: In C++ setjmp and longjmp have been largely replaced by exceptions.

# The goto Statement

The C and C++ goto keyword is implemented with setjmp and longjmp. goto allows us to jump to a program label:

```
#include <setjmp.h>
#include <stdio.h>

int main() {

    printf("hello world\n");
    goto foo_label;
    printf("1+1=2\n");

foo_label:
    printf("goodbye\n");
    return 0;
}
```

output
hello world
goodbye