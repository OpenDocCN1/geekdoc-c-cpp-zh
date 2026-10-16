```
{ // for loop in C++, Java, and 1999 ISO C
e1; // may contain local declarations
while (e2)
{  S;
    e3;
}
}
```

Many languages severely restrict the format of the for-loop (which, as noted, is just syntactic sugar in C), so that it can only be used for indexing situations. For example, in Ada the for-loop can only be written as a process controlled by a single local index variable, which is implicitly defined by the loop. Thus, the previous C for-loop would be written in Ada as:

```
for i in 0 .. size - 1 loop
    sum := sum + a(i);
end loop;
```

and i is implicitly defined and is local to the code of the loop. Even more, i is viewed as a constant within the body of the loop, so assignments to i are illegal (because this would disrupt the normal loop progression):

```
for i in 0 .. size - 1 loop
    sum := sum + a(i);
    if sum > 42 then i := size; -- illegal in Ada
    end if;
end loop;
```

This form of loop is often included in languages because it can be more effectively optimized than other loop constructs. For example, the control variable (and perhaps the final bound) can be put into registers, allowing extremely fast operations. Also, many processors have a single instruction that can increment a register, test it, and branch, so that the loop control and increment can occur in a single machine instruction. To gain this efficiency, however, many restrictions must be enforced, such as those for Ada mentioned above. Most of the restrictions involve the control variable i. Typical restrictions are the following:

+   - The value of i cannot be changed within the body of the loop.

+   - The value of i is undefined after the loop terminates.

+   - i must be of restricted type and may not be declared in certain ways, for example, as a parameter to a procedure, or as a record field, or perhaps it must even be a local variable.

Further questions about the behavior of loops include:

+   - Are the bounds evaluated only once? If so, then the bounds may not change after execution begins.