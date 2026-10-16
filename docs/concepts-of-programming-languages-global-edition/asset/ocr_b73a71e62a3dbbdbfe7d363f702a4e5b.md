```
    ...
} // end of c
    ...
a(true);
    ...
} // end of bigsub
```

The calling sequence for this program for execution to reach d is

+   bigsub calls a
+   a calls b
+   b calls a
+   a calls c
+   c calls d

# 4. Show the stack with all activation record instances, including static and dynamic chains, when execution reaches position 1 in the following skeletal program. This program uses the deep-access method to implement dynamic scoping.

```
void fun1() {
    float a;
    ...
}
```

```
void fun2() {
    int b, c;
    ... <-- 1
}
```

```
void fun3() {
    float d;
    ...
}
```

```
void main() {
    char e, f, g;
    ...
}
```

The calling sequence for this program for execution to reach fun3 is

+   main calls fun1
+   fun1 calls fun3
+   fun3 calls fun2

# 5. Assume that the program of Problem 4 is implemented using the shallow-access method using a stack for each variable name. Show the stacks for the time of the execution of fun3, assuming execution found its way to that point through the sequence of calls shown in Problem 4.