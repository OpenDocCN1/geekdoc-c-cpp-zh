# 6.2 Storage Classes in a Single File 363

value when the data file is opened and needs to retain that value between calls.
The variables y and flag do not need to be static as they are initialized before they are used.

# 6.2.4 Storage Class register

There is a set of general purpose processor registers within the central processing unit of a computer. The access speed of register is much faster than that of memory. A programmer may request these registers as storage for variables such as counters and accumulators that are used frequently, for computational efficiency. But the compiler has the privilege of honoring the request or not honoring the request. If the registers are all assigned at the time the request is made, then the compiler will not assign a register to the variable requesting the register. It will automatically assign the storage class auto. Register storage class defaults to auto storage class if a register cannot be assigned to the variable. In general a register class is declared as follows.

```
{ register int count; }
```

The register storage class variables are local to the functions and the local blocks. Their scope follows the same rules as auto variables. The register storage class is only needed when a brute force algorithm is being used and there are many cases to check. In general, it is better to avoid that kind of algorithm.

The following table shows the scope, initialization, retention status, speed of access, and declaration of the auto, extern, static, and register storage classes.

| Scope | Initialization | Retains value between function calls | Speed of access | Declaration |
| --- | --- | --- | --- | --- | --- |
| auto | local | explicit | no | normal | default class in block |
| extern | global | 0 default | yes | normal | default class outside all blocks |
| static | local/global | 0 /explicit | yes | normal | explicit |
| register | local/global | explicit | no | fast | explicit |