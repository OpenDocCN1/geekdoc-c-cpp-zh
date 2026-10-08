# 204 Control Structures

![](bbox=[0.258, 0.093, 0.814, 0.502])

Figure 4.5 Nested selection branching structure

The flowchart in Figure 4.5 illustrates a case structure.
For example, if data contains three measurements x, y, and z that must be positive, then the data can be validated by the following code:

```
if(x <= 0)
    printf("Invalid value for x");
else if(y <= 0)
    printf("Invalid value for y");
else if (z <= 0)
    printf("Invalid value for z");
else
    printf("The values are:", func(x, y, x));
```

Exactly one of the four statements will be executed regardless of the number of conditions that may be true.
Notice that the default is the else clause. If all the conditions are false it automatically defaults to the else clause. If there is more than one sequence statement in any of the branches, the sequence must be blocked with braces.